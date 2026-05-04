# Introduction
## Keywords
- Lock
- Lock-based Protocol
- Lock-S
- Lock-X
- Lock Compatibility
- Lock Upgrade

## What and Why
**Data Inconsistencies**
- Lost Update

**Lock-Based Protocol**
Approach that uses lock on data like mutex, to ensure *serializable* transactions. There are different types of locks based on whether the data is `read` or `written` to:
1. **Shared lock**
	- Only for reading
	- Can be shared by multiple transactions
2. **Exclusive lock**
	- For reading and writing
	- If a data $d$ is X-locked, it can't be `read` or `written` to, except for the X-lock holder
	- Can only be hold by one transaction at one time

>[!note]
>If a transaction holds S lock first, X lock holder has to wait until the S lock holder finishes reading to write.

**Lock Compatibility Matrix**

| (T1 holds) | T2 - S  | T2 - X |
| ---------- | ------- | ------ |
| S          | Allowed | Wait   |
| X          | Wait    | Wait   |
## Locking Protocol
**Lock Conversion**
- Lock Upgrade (S $\rightarrow$ X)
	- T1 can upgrade the key, if it is the **only** holder of an **S-lock**
- Lock Downgrade (X $\rightarrow$ S)

# Locking Protocol
## Keywords
- Two-Phase Locking (2PL)
- Growing Phase
- Shrinking Phase
- Lock Point
- Cascading Rollback
- Strict 2PL
- Rigorous 2PL

## What and Why
Just locking and unlocking arbitrarily is not good enough to eliminate data inconsistencies.

# Two-Phase Locking
## What and Why
Rule:
"All transactions must do *lock* and *unlock* in two separate phases"

**Phase 1**: Growing
- The first phase of transaction
- Transactions can only acquire keys
- They cannot release keys
- They can *lock-S*, *lock-X*, and *upgrade*
**Phase 2**: Shrinking
- Starts soon after transactions release their first key
- Transactions can only release keys, and not allowed to azquire them
- Transactions can *unlock* and *downgrade*

**Lock Point**
The point at which transactions acquired their last key (end of growing phase).
The order of **serializability** of transactions depends on their lock point.

**2PL Pros and Cons**
- Guarantees **Conflict Serializability**
- Can still cause deadlocks
- Can cause Cascading Rollback

## Cascading Rollback
Failure of one transaction causes the failure of other transactions, with cascading consequences.
**Solution: Strict 2PL** & **Rigorous 2PL**

## Variation of 2PL
**Strict 2PL**
A special variation of 2PL with added rule:
- Transactions cannot release **lock-X** until it **commits** or **aborts**.
- Stops cascading rollback

**Rigorous 2PL**
Added rule:
- Transactions cannot release ALL locks (S or X) until it commits or aborts
- Simpler to implement cause you just release all keys when commiting/aborting

**Relationship**
Rigorous 2PL $\in$ Strict 2PL $\in$ 2PL


