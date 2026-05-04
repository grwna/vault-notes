# Behaviour on Return
Remember how a stack frame is set up ([[Functions, Frames, and Data#Stack|read]]). After the `leave` instruction in a function the `rsp` will point to the **return address**.
>[!note]
>The `leave` instruction does two things, make `rsp` point to the saved `rbp` then `pop rbp` which moves the `rsp` to point after the saved `rbp` which we know as the return address.

When you craft a `rop`chain like this:
```
    pop_rdi,
    1,
    win,
```
`pop_rdi`becomes the new return address, after the `ret` instruction is done in the **main** function, it pops the return address. We know that this means `rsp` moves to the next value in the stack, which is 1, so `rsp`now points to 1. Inside `pop_rdi` there is a `pop rdi` instruction (ikr), which shifts the `rsp`to point to `win`address. 