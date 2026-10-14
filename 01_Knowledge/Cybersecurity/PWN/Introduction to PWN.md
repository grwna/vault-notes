# Stack
[[Functions, Frames, and Data#Stack|Stack]]
## Return Address, RBP, and Canary
The layout of these trio is dependant on the compile flags used. But most comonly in CTFs they are stacked this way

| What           | Size      |
| -------------- | --------- |
| Return Address | 8 bytes   |
| Saved RBP      | 8 bytes   |
| Canary         | 8 bytes   |
| Other data     | ... bytes |
Also, in [[Ghidra]], canaries are usually at local_10. If our buffer is at local_30, then canary is $0x30-0x10=0x20$, which is 32 in decimal. This means the canary ends at 32 bytes after the buffer (starts at 24 bytes).

# ToC
- [ASLR](#aslr)
# ASLR
Pages are aligned to `0x1000` alignment, meaning the last three nibble[^1] of an address is never changed. So overwriting the 2 least significant bytes, only one nibble is required to be brute-forced.

>[!important]
>No PIE opens up opportunities for gdb inspection of the stack. Since the addresses never change, this opens up attack vectors.
# Printf Vuln
`printf()` starts reading from the stack frame **above** (higher memory address) its argument. In other words, downward through the stack, moving to the base pointer.

# NX Protection
The No-Execute protection dictates that addresses **on the stack** cannot be executed, otherwise instructions stored on the stack can be executed.

# Causes of Disclosure
Cause of disclosure of memory, or also known as a 'leak', is a vulnerability where a specific seciton of a program causes the accidental disclosure of **secret** information.
## Buffer Overread
A read larger than the buffer, causing the data beyond the buffer being read.
## Termination Problems
Off by one errors can cause strings not being properly null terminated, causing functions depending on such terminations to read beyond the erroneous buffer.

## Uninitialized Data
Or also called "Uncleaned Data", because C doesn't clean up for you, uninitialized data may contain data that was meant to be removed, causing it to print data you may not want to print/show.
>[!warning]
>In cryptography implementation, there is a vulnerability class, where `memset`, used for cleaning up data is removed by compilers for optimizations.

[^1]: half bytes

