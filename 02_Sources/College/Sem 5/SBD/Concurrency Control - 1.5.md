# Graph-based Protocol
- Tree Protocol
- Guarantees Serializability?
- Deadlock Free?
- Pros & Cons

Unlike 2PL, this protocol has a deadlock avoidance "*builtin*". 
Assumes that data items can be mapped as nodes for a tree or a DAG.

## Tree Protocol
Simplest Graph-based protocol
How it works:
- Only `lock-x`
- First lock: can be given to any random node in tree
- Next locks: In order to hold a `lock-x(Q)` for data `Q`, a transaction needs to have held the `lock-x` for the parent of `Q`
- Unlocking: a lock can be released at any time (different to *shrinking phase*)
	- However, once T releases a lock for `Q`, T cannot request any lock for `Q` or any nodes in the subtrees under `Q`

**Guarantees**
- Conflict Serializability
- Deadlock Free 
	- Because every transaction is forced to request lock in a certain order (no cycle)

**Pros & Cons** (compared to 2PL)
Pros
- Deadlock Free
- Better concurrency (can unlock anytime)
Cons
- Not flexible, depends on tree structure
- Random orders data access

# Multiple Granularity
- trade-offs
- Intention Lock
- Intention Shared (IS)
- Intention Exclusive (IX)
- Shared Intention Exclusive (SIX)
- Compatibility Matrix
- Hierarchical Protocol

## Granularity
Granularity is the size of data items that we can lock.
The Hierarchy:
- Database
- Tables
- Pages (Physical Blocks)
- Rows (Tuples)
- Attributes (Fields)

## Trade-Offs
Choosing granularity level is a trade-off between overhead and concurrency:
1. **Coarse Granularity**
	- Lock tables
	- Low Overhead
	- Low Concurrency
2. **Fine Granularity**
	- Lock Tuples
	- High Overhead
	- High Concurrency

**Solution**: Multiple Granularity (lock at any granularity levels for maximum efficiency)

## Intention Locks
Lock at higher granularity to mark that lower granularity has a lock.
**Implication**: This makes it so that a transaction that needs to lock a table does not have to iterate all rows to see if a lock is applied to any rows

**Types of Locks in MG Protocol**
- Shared
- Exclusive
- Intention Shared - intention to apply lock-S in a lower level
- Intention Exclusive - intention to apply lock-X in a lower level
- Shared Intention Exclusive
	- Strong Hybrid Lock (equivalent to S), very specific but very efficient for its use case
	- Read all sub-hierarchy, then update some items under it (equivalent to IX)

## Compatibility Matrix

| T1 Holds | IS      | IX      | S       | SIX     | X    |
| -------- | ------- | ------- | ------- | ------- | ---- |
| **IS**   | Allowed | Allowed | Allowed | Allowed | Wait |
| **IX**   | Allowed | Allowed | Wait    | Wait    | Wait |
| **S**    | Allowed | Wait    | Allowed | Wait    | Wait |
| **SIX**  | Allowed | Wait    | Wait    | Wait    | Wait |
| **X**    | Wait    | Wait    | Wait    | Wait    | Wait |
- Lock request have to be **top-down**
- Lock releases have to be **bottom-up**

**Aturan Request (Top-Down):**
- Untuk mendapat `lock-S` atau `IS` pada node N, transaksi harus _sudah memegang_ `IS` atau `IX` pada `parent(N)`.
- Untuk mendapat `lock-X`, `IX`, atau `SIX` pada node N, transaksi harus _sudah memegang_ `IX` atau `SIX` pada `parent(N)`.