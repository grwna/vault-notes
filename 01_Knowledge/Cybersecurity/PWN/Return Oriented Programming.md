# Philosophy
In the absence of code injection (No eXecute), we turn to Code Reuse. Using code that already exists in the `.text` of the  binary to perform attack operations.

>[!tip]
ROP is basically shellcode, but you dont need to write the shellcode. (read: [Weird Machine](https://en.wikipedia.org/wiki/Weird_machine))
# x86
Back in x86 where arguments are passed on the stack, it was possible to return to libc using just a simple buffer overflow due to the nature of the stack frame ([[Functions, Frames, and Data#Layout|read]]), discovered by Solar Designer.

# x64
Using jit spraying you can jump to the middle of functions. When overwriting return address, the address does not have to be the start of a function.

On the basic level, ROP can be used to set up arguments for a function. But later in the more advanced challenges, ROP can be use for anything. You can set up ROP chains that do basically the same thing as what shellcodes do.
>[!example]
>Craft a long rop chain that uses `open` to open the flag, then set up arguments and call `sendfile` to print it.
>

Also, you don't have to get a `pop rdi; ret`, you can use the address of a line in the middle of a function to only use what you need from that function. 
>[!important]
>When you overwrite return addresses, remember that in the payload each part of the payload that uses `ret` will return to the next part of the payload (need to study more about this).
>
>By next part of the payload i mean after an 8-byte value that gets popped to `rbp` by the previous function. Read ([[Stack#Behaviour on Return]])

# Characteristics
## Stack Pivoting
ROP chains require space on the stack. We cannot write an infinitely long ROP chains, because there is a limit to how long the code is after current RIP. In order to bypass this limit, we can do stack pivoting (read: [ir0nstone](https://ir0nstone.gitbook.io/notes/binexp/stack/stack-pivoting)).

In short, stack pivoting is a way to "fake" a stack by making RSP point to a controllable memory. This can be used to bypass DEP/NX.

## Libc
 GOT is way more important than PLT in terms of theory, but both play a crucial role in exploit.
