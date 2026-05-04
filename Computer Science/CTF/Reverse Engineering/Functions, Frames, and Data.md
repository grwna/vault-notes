- [[#Modules|Modules]]
- [[#Functions|Functions]]
- [[#Data|Data]]

A **program**...
- consists of **modules**...
- that are made up of **functions**...
- that contain **blocks**...
- of **instructions**...
- that operate on **variables** and **data structures**...
# Modules
Libraries that developers often rely on

# Functions
Functions can be represented as a **control flow graph**, that defines how different functions are called based on conditional jumps.
> [!note]
> Most functions have a well defined goal, that can be reverse engineered in isolation, but often times you need to understand how they **work together**.

## Stack
The stack is a region in memory used to store local variables and call contexts. The stack grows **downwards** in memory. 
### Layout
#### Initial Layout
Initially, the stack will store `argv` and `envp`. With `rsp` pointing to the top, and `rbp` pointing to the actual bottom.
![[Pasted image 20250713132600.png|Stack Initial Layout]]

x86 Stack Frame with arguments
![[x86 stack frame.png]]

#### Function Frame
If a function is called, the return address (next instruction after the function call) is pushed to the stack, and pop after function is completed.
The current `rsp` becomes a "new" `rbp` that points to the caller's saved `rbp` which points to the bottom of the stack frame, and the `rsp` will grow (subtracted) as the function runs to create "space" for the function.
![[Pasted image 20250713133046.png|Frame]]
after the function is completed, `rsp` will go back to `rbp` for "cleanup". However, data written to the frame does not disappear, moving `rsp` only **logically** cleans up the space.
>[!info]
>The process of changing `rsp` back to `rbp` is done by the code:
>`mov rsp, rbp`

>[!note]
>`-fomit-frame-pointer` flag in compilers disables frame pointers, allowing the use of `rbp`as a general purpose register

# Data
Programs operate on data. Data can be stored in sections (`.rodata`,`.data`,`.bss`), in the stack or the heap.
[[Introduction to Reverse Engineering#Headers|Sections Explanation]]

Type information is lost in the compilation process, meaning reverse engineering through code is required to see how data is used by code.
## Data Access
### Stack
![[Pasted image 20250713143807.png | 600]]
### ELF Sections
Data in ELF sections are stored at known offsets in the binary, it is accessed via `rip`-relative instructions.
![[Pasted image 20250713144158.png]]

### Heap
Pointers to heap are generally stored in memory or on the stack. Mind the difference between
![[Pasted image 20250713144449.png|500]]

## Data Structures
### Union
```
typedef struct
{
    union
    {
        char data[24];
        struct term_str_st
        {
            char color_set[7];   // \x1b[38;2;
            char r[3];          // 255
            char s1;            // ;
            char g[3];          // 255
            char s2;            // ;
            char b[3];          // 255
            char m;            // m
            char c;             // X
            char color_reset[4];     // \x1b[0m
        } str;
    };
} term_pixel_t;
```
How is this data stored? the size of `term_pixel_t` is 24 bytes. The data and the `term_str_st` struct is stored at the same place (it is the same one thing) it is just two different way of presenting (and accessing) data. 
