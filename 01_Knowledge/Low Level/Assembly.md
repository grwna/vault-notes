
# ASM Syntax
## Dereferencing
You can dereference using brackets, i.e. `[rax]`, which changes the value pointed to by `rax`.
The value in `rax` itself does not change.

## Specifying Size
- 1 byte - `mov [rax], al`
- 2 byte - `mov [rax], ax`
- 4 byte - `mov [rax], eax`
- 8 byte - `mov [rax], rax`
OR
- `mov BYTE PTR [rax], 5`
- `mov WORD PTR [rax], 5`
- `mov DWORD PTR [rax], 5`
- `mov QWORD PTR [rax], 5`

>[!warning]
>When using sized register instructions, ensure that the registers are zeroed (xor'd) first. Because `mov al, 1` only change the least significant byte of `rax`,  keeping the rest intact
## **Calling** Conventions
### x64 vs x86

| INFO           | x86        | x64       |
| -------------- | ---------- | --------- |
| Invocation     | `int 0x80` | `syscall` |
| Syscall number | `eax`      | `rax`     |
| 1st            | `ebx`      | `rdi`     |
| 2nd            | `ecx`      | `rsi`     |
| 3rd            | `edx`      | `rdx`     |
| 4rth           | `esi`      | `r10`     |
| 5th            | `edi`      | `r8`      |
| 6th            | `ebp`      | `r9`      |
| Return value   | `eax`      | `rax`     |

**x86**

>[!warning] Important
>System V ABI[^1] is different than direct kernel (syscalls) convention
>System V ABI - 4th is `rcx`
>Syscall - 4th is `r10`
>
>As for x86, C calling convention uses the stack while syscalls uses the registers

# Tricks
Instead of `mov rdi, rsp`, you can do `push rsp, pop rdi`
[^1]: C calling convention
	
