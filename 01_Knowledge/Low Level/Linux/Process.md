# Lifecycle
## Creation
In Linux, processes propagate by mitosis. If you run `/bin/cat` in `bash`, the `bash` process copies itself so it becomes two: the original, and a new child. The child process will `execve` `/bin/cat` and become the new process. 
## Loading
If `execve` is successful, then the kernel will process the files according to its header and data (file formats). 
> [!note]
> The kernel knows how to handle custom file formats (or regular formats with custom loading) because of files stored at `/proc/sys/fs/binfmt_misc/`  

Each process is loaded into their own *virtual memory* space, where kernel code in the "upper half" of memory is inaccessible to the process. You can see the space by looking at `/proc/self/maps`
## Execution
libc calls `_libc_start_main()` which calls the `main` function you wrote, and passes the `argv` and `envp`. 
Syscalls are a way for programs to communicate with the OS, **Signals** provide a way for the OS to talk to programs. Programs have handlers for signals, EX. `SIGKILL` or `SIGINT`.
Another way to communicate to outside is using **shared memory** with other processes.

# Modification
## Patching
Binaries are run using an interpreter, which can be seen using `readelf -a {binary} | grep interpreter` or `ldd {binary}`. This interpreter can be changed by patching the binary using `patchelf` or `pwninit`.