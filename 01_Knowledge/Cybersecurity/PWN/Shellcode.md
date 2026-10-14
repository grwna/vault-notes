- [[#References|References]]
- [[#Code Injection|Code Injection]]
- [[#Prevention|Prevention]]

# References
- [amd64 opcode list](http://ref.x86asm.net/coder64.html)
- [Filippo Syscall List](https://filippo.io/linux-syscall-table/)
- [syscall.sh](https://x64.syscall.sh)
- [[Assembly | Assembly Notes]]

# Code Injection
## Stack
[[Stack]]
`rsp` always point to the top of the stack, meaning if you push arbitrary data, `rsp` will point **to that data**.

>[!example]
```
mov rbx, {0xff2345}        # arbitrary
push rbx
mov rdi, rsp
```

The code will pass `{data}` as the first argument of a function.  

>[!note] 
>why  push `rbx`? 
>`rdi` require a memory address for **strings**. Meaning data cannot be moved to `rdi` directly.
>By pushing to the stack, we have turned `rsp` as that **memory address** that we need. 

If, for example, i created a label `flag:`, the same code will look like this
```
lea rdi, [rip+flag]          # rip for position-independence
flag:
.string "/flag.txt"
```

---
## Common Challenges
### Size Restrictions
You need to keep in mind the size of what syscall youre using. `sendfile()` is more efficient than `read()` then `write()`, `chmod()` is very efficient but only if you have access already, etc.

>[!tip] Fun Fact
>`xor edi, edi` is only 2 bytes while `xor di, di` is 3 bytes. This is because 32 byte xor is optimized and the 'default' while all other sizes require a prefix. This is true for every register.
>
>This optimization also causes every instruction that writes to 32 bit registers to zero extends the result.


### Forbidden Bytes
Some functions will be problematic if a certain bytes are in the shellcode's machine code. Ex. `strcpy` will stop if it encounters a null byte `\x0`, or `scanf` with newlines `\x0a`.
Consequently, you need to be careful with how you construct the code:

![[asmnull.png.png]]

amd64 code has '**H**', a prefix added for compatibility with x86.
### Shellcode Mangling
The executed shellcode is processed (jumbled, compressed, encrypted). Strategy to solve this is to start from the final goal then work backwards.

### Flag Fetching
- Shell
- Read file
- Others, learn later.

>[!warning]
>The same binary can have different `root` **level access** depending on the shellcode.
>Specifically, the execution of `shell` using the flag `-p` as the parameter.
>Remember that an `argv` array will have the file/path name as the first argument. 

>[!warning]
>The directory where you executed the `.py` file matters on how you pass pathname arguments, this can make it easier to pass arguments.

### Multi-stage Shellcode
Sometimes programs require multiple shellcode sequence to run. For example, if there is a size limitation, you can make the first (limited shellcode) to set up a short syscall to `read()`, in which will be an opportunity to inject the **second stage** shellcode, which will be the one doing flag reading or shell executing.
# Prevention
No-eXecute bit, code on stack and heap not executable. The rise of the NX bit has caused shellcode injections to be very rare.

## Prevention Bypass
### De-Protecting Memory
Using the `mprotect()` syscall, we can trick program to `mprotect()` our shellcode to allow shellcode execution.
Most common way to do this is code reuse through [[Return Oriented Programming |ROP]]. Other ways to do this is situational, depending on what the program does.

### Just in Time
[[Language Theory#Just in Time|Just in Time]]
JIT compilers need to generate (and frequently re-generate code) that is executed. Which means pages need to be writable and executable. The safe thing to do is to use `mmap()` and `mprotect()` syscalls in between generation/execution.    
However, syscalls are slow which defeats the point of JIT.

Writable and executable pages are common. If a binary uses a library with writable+executable page, that page lives in your memory space.

**JIT Spraying**
Even if JIT uses `mprotect()`on its page, we can still inject shellcode.