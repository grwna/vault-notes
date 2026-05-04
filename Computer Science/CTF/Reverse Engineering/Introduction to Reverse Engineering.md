- [[#Philosophy|Philosophy]]
- [[#ELF File|ELF File]]
- [[#Endiannes|Endiannes]]
- [[#Process|Process]]
# Philosophy
In the compilation process, many symbols (comments, variable/function names, entire algorithms[^1]), can be stripped from the binary. In reverse engineering we have to get all those back.

# ELF File
## Headers
ELF files have program headers that tells useful information about the binary.

```
┌──(grwcha㉿grwna)-[~]
└─$ readelf -a /bin/cat
ELF Header:
  Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00
  Class:                             ELF64
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              DYN (Position-Independent Executable file)
  Machine:                           Advanced Micro Devices X86-64
  Version:                           0x1
  Entry point address:               0x3140
  Start of program headers:          64 (bytes into file)
  Start of section headers:          46160 (bytes into file)
  Flags:                             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           56 (bytes)
  Number of program headers:         13
  Size of section headers:           64 (bytes)
  Number of section headers:         31
  Section header string table index: 30
```
 The header also tells information about how the binary is loaded, you can use `readelf -f {binary}` to see the full data stored in ELF files. 
 
 >[!note]
 However, headers are optional. They are used only to make the ELF easier to read by humans

The ELF also contains section headers: 
- `.text`, executable code
- `.plt`, procedure linkage table - communicates with dynamic linker
- `.got` global offset table - "caches" the results of plt
- `.data`, pre-initialized data/variables
- `.rodata`, read-only data (constants, string literals, etc.)
- `.bss`, uninitialized data

## Tools for ELF
![[Pasted image 20250711110710.png]]

# Endiannes
On most modern CPU, bytes are stored in little endian, this means the integer `0x654d5c6d` (this integer corresponds to "eM\m") is actually stored as `6d 5c 4d 65`. So the comparison `var == 0x654d5c6d` is actually equivalent to `var == m]Me`

[^1]: In the case of compiler optimization
# Process
[[Process]]

# Reversing Tools
## Static Tools
Terminal
- [Kaitai Struct](https://kaitai.io)
- nm
- strings
- objump
- checkses

GUI
- IDA Pro
- Binary Ninja
- [Binary Ninja Cloud](https://cloud.binary.ninja)
- angr
- **ghidra**
- cutter
## Dynamic Tools
Tracing
- ltrace - libcalls
- strace - syscalls

Debugger
- gdb
- gdb scripting [tutorials](https://www.google.com/search?client=opera-gx&q=gdb+scripting+tutorial&sourceid=opera&ie=UTF-8&oe=UTF-8)

Timeless Debugging (go backwards in instruction)
- gdb
- qira
- rr