# Architecture
## ILP (Instruction Level Parallelism)

- Pipelining
- Multiple Issue (Embarassingly Parallel at Instruction Level)
	- Static - at compilation
	- Dynamic (superscalar) - at execution
## Hardware Multithreading
To minimize idle cores
- Fine-grained - switch threads on every instruction
- Coarse-grained - switch threads on long pauses (*stall*)
- Simultaneous Multithreading (SMT) - Hyperthreading, fine grained but multiple threads can operate at once

## Flynn's Taxonomy
- SISD
- SIMD - GPU, Vector processor
	SIMD are not flexible. In order to improve it, several modifications exist
	- Vector Processors
	- GPU 
		- Integrated
		- Discrete - comscmunicates with CPU through PCI bus (overhead)
- MISD
- MIMD
	- Shared memory
		Uniformity of memory access time
		- UMA - every core access any memory location in the same amount of time
		- NUMA - cores can access any memory location, but some faster than others
		Cache coherence - changes in shared data are propagated throughout the system
		Solution for cache coherence
		- Snooping - listening, good for small systems
		- Directory Based - central directory, goo dfor big systems (NUMA)
	- Distributed memory
		Requires communication

# Interconnection
## Network Performance
- Latency - amount of time for data to reach the destination
- Bandwidth - speed of data transfer
- Bisection Width - the higher the better


# Paradigma Software
Software needs to take advantage of hardware parallelism, but no compiler is smart enough to do it, programmers have to.

## Model Pemrograman
- Process-based - message passing, works like Distirbuted memory
- Thread-based - shared data, works like shared memory
- Vectorization
- Stream processing - GPU

**SPMD** - single program multiple data
- One program but threads can act differently based on conditionals

**Threads in Shared Memory**
- Dynamic - creating and destroying threads is significant overhead
- Static
- Think of preallocated disk

**Challenges of Parallel Programming**
- Distribute work evenly, minimize communication
- Synchronization
- Communication
- Nondeterminism
- Race Condition

**Communication**
- Message passing
- IO
	- Input - should be master rank only
	- Output - better to be gathered at master rank first then output
	- File - one file should not be accessed by multiple threads
# Analisis Performa

**Boundary Factors**
- Speed - FLOPS/FLOP per Second
- Feed - bandwidth, memory bound if bottleneck is bigger than computation

**Metrics**
- Speedup - Tserial / Tparalel
- Efficiency - Speedup / processes

**Amdahl's Law**
- speedup is limited by serial part
- With infinite processors, if 10% of program is serial, speedup **will not** exceed 10x
- applies only for same size

**Gustafson-Barsis Law**
- a counter to amdahl's law
- when we increase processor, we usually increase data
- this means amdahl's law dont really apply most of the time

**Scalability**
- Strong scaling - scale same data with more processors (Amdahl's Law applies)
- Weak scaling - size increases (Gustafosn's Law applies)

**Time** is measured by taking the highest duration stored by processes. Formula is:
$$T_{parallel} = \frac{T_{serial}}{p} + T_{overhead}$$
**Overhead Components**
- Communication
- Synchronization
- Extra steps