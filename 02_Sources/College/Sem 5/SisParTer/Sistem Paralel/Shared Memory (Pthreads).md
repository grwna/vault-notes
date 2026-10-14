# Keywords
**Intro**
- Proccess vs Thread
- Pthreads
**Race Condition & Critical Section**
- Race Condition
- Critical Section
- Busy Waiting
**Mutex Synchronization**
- Mutex
- Mutex in Pthreads
**Producer-Consumer & Semaphore**
- Limits of mutex
- Producer-Consumer
- Semaphore
- Mutex vs Semaphore
# Intro
**Process vs Thread**
- Process
	- Isolated
	- Each has its own memory space, data, and state
- Thread
	- Many threads in a process
	- **Share the memory space**
	- Each threads have its own stack and instruction pointer

**POSIX threads** (Pthreads)
- Create threads using `pthread_create`
- `pthread_join` waits until all threads finishes
```c
int pthread_create(
    pthread_t *thread, -> will store the id of new thread
    const pthread_attr_t *attr, -> attributes, NULL for default
    void *(*start_routine)(void *), -> procedure for thread to run
    void *arg -> arg to procedure only one
);
```
```c
int pthread_join(
    pthread_t thread,
    void **retval
);
```

# Race Condition & Critical Section
- Race Condition
	- *Lost update*
- Critical Section
	Solution
	- Busy-Waiting
	- Mutex

Core problem of race condition is **operation atomicity**. 
Operations like `sum += val` is **not atomic**, it is made up of three instructions:
- LOAD
- ADD
- STORE
In the middle of this, thread can be interrupted so other instruction is done before all three instructions finish.

Solutions (like **mutex**) is done to make the three instructions act like **one uninterruptuble** instructions (Atomic).

# Mutual Exclusion
**Mutex in Pthreads**
- `pthread_mutex_init`
- `pthread_mutex_destroy`
- `pthread_mutex_lock`
- `pthread_mutex_unlock`

**Improvement**
In busy waiting, while waiting, threads can "steal" CPU time that should be given to the working thread. This makes cases where `threads` > `core` significantly worse for busy waiting, but mutex is stable.

**Tips**
- Critical section should be short (dont include slow ops like I/O)
- Always unlock what was locked

# Producer-Consumer & Semaphore
**Mutex Weakness**
 - Does not care which order threads enters CritSec

**Producer-Consumer**
- Producer produces data and store in **buffer**
- Consumer takes data from **buffer** and proccesses it
- The problem:
	- Producers cant store if buffer is full
	- Consumer has to wait for buffer to have data

**Semaphore**
Mutex that can count.
Semaphores are not native in pthreads.
Semaphores funcitons operations are atomic.

Semaphores uses counters as **quota**, if counter reaches zero threads have to wait, otherwise threads enters critical section and decrement the counter.

- **`sem_t my_sem;`**: Mendeklarasikan variabel semaphore.
- **`sem_init(&my_sem, 0, initial_value);`**: Menginisialisasi semaphore.
    - `0`: Menandakan semaphore ini hanya dipakai oleh thread dalam proses yang sama.
    - `initial_value`: Nilai awal dari penghitung semaphore.        
- **`sem_wait(&my_sem);`**: Menunggu atau mengurangi nilai.
- **`sem_post(&my_sem);`**: Memberi sinyal atau menaikkan nilai.
- **`sem_destroy(&my_sem);`**: Membersihkan semaphore setelah selesai.