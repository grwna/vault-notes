# Keywords
**Intro**
- OpenMP
- Pragma
- Team, master, slave
- Portable Code
- `#pragma omp parallel`
**Parallel Loop**
- `#pragma omp parallel for`
- Loop partition
**Management and Syncronization**
- Variable scope in OpenMP
- *shared* vs *private*
- `reduction`
- `default(none)`
- Data Dependency
**Loop Scheduling and Explicity**
- load imbalance
- `schedule`
- `static, dynamic, guided`
- `#pragma omp barrier`
- `critical, atomic, lock`
**Advanced Parallelism**
- Parallelism on different tasks
- `#pragma omp sections`
- `#pragma omp task`
- `#pragma omp taskwait`
**Optimization and Extra Directives**


# Intro
Pragmase are **compiler directives**. OpenMP is portable, since pragmas are ignored if not recognized (no errors). There are other things that makes OpenMP portable.

`#pragma omp parallel`
- Separates block into a **team** of threads
- Uses **fork-join** with master and slaves
# Parallel Loop
`#pragma omp parallel for`
- Automatically partition `for loop` into a team by the amount of threads used

There are some rules that makes loops **unparallelable**, this shouldnt be hard to identify
# Management and Syncronization
**Scope**
- Shared - all threads can modify, default for variables declared outside pragma loop
- Private - isolated per thread, no race condition, default for var declared inside (iterators as well)

**Reduction**
`global_sum += private_sum`
Race conditions can happen. use `reduction`, which work similarly to `MPI_Reduce`

**Syntax** `reduction(<operator>:<variable>)`
**Operators** `min, max, +, -, *, &, |, ^, $$, ||`

Reduction is only for associative and commutative.
- Associative - because aggregation does not take into account orders
	- Nondeterministic
	- No division in reduce
- Commutative - same as associativity

**default(none)**
this causes OpenMP to not assign variables with default scope.
Every variabel have to be assigned in either `shared()` or `private()`
# Loop Scheduling and Explicity
**Load Imbalance**
When OpenMP distribute loop iterations to threads, every iterations are not guaranteed to be equal in load. Some iterations can be slower/longer than others. Solution: **`schedule`**

`**schedule**`
Syntax: `schedule(<type>, <chunk_size>)`
>[!note]
>The default chunk size is $\frac{data}{threads}$ for static. For dynamic and guided, it is 1. 
>

Types:
- `static` - lowest overhead, assigns iterations with round robin
- `dynamic` - iterations are divided into chunks, each thread asks for new chunk if previous chunk is completed
- `guided` - like dynamic but chunk sizes decrease overtime. this is done to minimize overhead in the beginning

**Explicit Synchronization**
- `#pragma omp barrier` - threads can not go past barrier until all threads reaches it
- `#pragma omp critical(<name>)` - critical section declaration for mutual exclusion
- `#pragma omp atomic` - lightweight version of critical, makes a **single statement** atomic
- `omp_lock_t`
	- `omp_init_lock`
	- `omp_destroy_lock`
	- `omp_set_lock`
	- `omp_unset_lock`
>[!warning]
>Explicit synchronization can cause deadlocks

# Advanced Parallelism
**Functional Parallelism**
Threads not on one loop, but different tasks
Example: Thread 1 reads file, Threads 2 process data, Threads 3 writes to different file.
This can be parallelized with pipelineing. In OpenMP with `$pragma omp sections`

**`omp parallel sections` and `omp section`**
Sections are independent, each threads work on each section. If sections > threads, one thread can do multiple sections sequentially.

**`pragma omp task`**
Works on blocks of code, and wrap that block into a virtual queue, which idle threads can work on. This is good for unpredictable, unstructured, or dynamic workload like recursive functions.

**`pragma omp taskwait`**
Works like barrier that blocks tasks until all child tasks finishes
# Optimization and Extra Directives