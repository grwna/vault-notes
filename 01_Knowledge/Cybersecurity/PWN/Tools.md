
# ToC
- [Debugger](#debugger)
- [PWNTools](#pwntools)
# Debugger
## PWNDBG

# PWNTools
## Disabling ASLR
`pwn.process("./program", aslr=False)`

## Finding Offsets
In order to make it work, you need to make sure that the program **actually crashes**, and on top of that, the core-dump files is created inside the current working directory. 

## ELF Syntax
`exe = './{binary_path}'`
`elf = context.binary = ELF(exe, checksec=False)`
- `elf.symbols['{symbol_name}']` - used to find address of symbol
- `file = next(elf.search(b"GNU"))` next() is for finding the next (in this case the first) occurence of the address found for the string `GNU`. search is for looking for strings

### Use of symbols (libc)
when `libc.symbols["some_func"]` is used without setting the value of `libc.address`, it will get the offset of `some_func`. After the base address is set, it will add the base to the offsets.