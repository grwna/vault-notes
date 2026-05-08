# Legend
```c
int MPI_Send(
	void* msg_buf_p, 
	int msg_size, 
	MPI_Datatype msg_type, 
	int dest, 
	int tag, 
	MPI_Comm communicator);
```
```C
int MPI_Recv(
	void* msg_buf_p, 
	int buf_size, 
	MPI_Datatype buf_type, 
	int source, 
	int tag, 
	MPI_Comm communicator, 
	MPI_Status* status_p);
```
# Point-to-Point Comm
Uses Send-Receive, and usually uses **SPMD**

- `MPI_Recv` is blocking, wait until receive
- `MPI_Send` can be blocking or not based on available buffers/ implementation
	- Eager protocol - non blocking
	- Rendezvous protocol - blocking
Other non-blocking implementation includes `MPI_Isend` or `MPI_I*` 
 ![[Pasted image 20251018152419.png]]

# Practical Application
**Steps:**
1. **Partition (Partisi)** 
2. **Communication (Komunikasi)**
3. **Aggregation (Agregasi)**
4. **Mapping (Pemetaan)**

# Collective Communication
## Keywords
- point-to-point alternative
- tree-structured communication
- `MPI_Reduce`
- `MPI_Allreduce`
- `MPI_Bcast`

## Concepts
### Aggregation

```C
int MPI_Reduce(
	void* input_data_p, 
	void* output_data_p, 
	int count, 
	MPI_Datatype datatype, 
	MPI_Op operator, 
	int dest_process, 
	MPI_Comm comm);
```
- `input_data_p`: Pointer ke data lokal yang akan dikontribusikan setiap proses.
- `output_data_p`: Hanya signifikan di `dest_process`. Pointer ke memori untuk menyimpan hasil akhir.
- `count`: Jumlah elemen data.
- `operator`: Operasi yang akan dilakukan, misalnya `MPI_SUM`, `MPI_MAX`, `MPI_MIN`.
- `dest_process`: Rank dari proses yang akan menyimpan hasil akhir.

Receive data from all process, then operate on it, which results in one data (aggregation) then send to one process.

**Important Stuff**
- Order-based matching - match based on the order of calls
- Synchronization Point
- Communication Tag - MPI uses implicit tag based on orders
- **Implication**: all process should have the same call orders

### Aggregation & Distribution
`MPI_Allreduce` works the same as `MPI_Reduce`, but the result is send to **all process**

### Distribution
`MPI_Bcast` - does not aggregate, just distribute. Take data from one process, **send to all**.
```C
int MPI_Bcast(
	void* data_p, 
	int count, 
	MPI_Datatype datatype, 
	int source_proc, 
	MPI_Comm comm);
```
- `data_p`: Pada `source_proc`, ini adalah data yang akan dikirim. Pada proses lain, ini adalah buffer untuk menerima data.
- `source_proc`: Rank dari proses yang menjadi sumber data.

## Other
**Rules of Collective Communication**
- Every process needs to call the same collective function, else **deadlock**
- Arguments should be compatible
- Do not use tags

**Other Collective Functions**
- `MPI_Scan`
- `MPI_Scatter`
- etc.

# Data Distribution and Vectors
## Keywords
- Data partition strategy
- `MPI_Scatter`
- `MPI_Gather`
- `MPI_Allgather`
- Parallel Matrix-Vector Multiplicaiton
## Concepts
**Vector Partition Strategy**
- Block partitioning - per block (1, 2 ,3)
- Cyclic partitioning- round robin (1, 4, 7)
- Block-Cyclic partitioning - data blocks are round robin'd

**`MPI_Scatter`**
Takes an array and send it to all process
```c
int MPI_Scatter(
	void* send_buf_p, 
	int send_count, 
	…, 
	void* recv_buf_p, 
	int recv_count, …, 
	int src_proc, 
	MPI_Comm comm);
```
- `send_buf_p`: Hanya signifikan di `src_proc`. Pointer ke array lengkap yang akan disebar.
- `send_count`: Jumlah elemen yang dikirim **ke setiap proses**.
- `recv_buf_p`: Pointer ke buffer di setiap proses untuk menerima bagian datanya.
- `recv_count`: Jumlah elemen yang diterima oleh setiap proses (biasanya sama dengan `send_count`).
- `src_proc`: Rank dari proses yang memiliki data awal.

**`MPI_Gather`**
Reverse of scatter, will send an array to destination process, `MPI_Allgather` will send to all process. However, `Allgather` is expensive
```c
int MPI_Gather(
	void* send_buf_p, 
	int send_count, 
	…, 
	void* recv_buf_p, 
	int recv_count, 
	…, 
	int dest_proc, 
	MPI_Comm comm);
```
- `send_buf_p`: Pointer ke data lokal di setiap proses yang akan dikirim.
- `recv_buf_p`: Hanya signifikan di `dest_proc`. Pointer ke array untuk menampung semua data yang terkumpul.
- `dest_proc`: Rank dari proses yang akan mengumpulkan data.

`MPI_Scatterv` and `MPI_Gatherv` - vectors, allows the adjustments  of the size of data being sent.