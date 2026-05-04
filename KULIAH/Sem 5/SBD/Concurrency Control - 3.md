# Timestamp-based Protocol
## Main Idea
Lock based is *pessimistic* meaning it has to ask for permissions. Time-based uses *serializability* order that is determined from the start.
- Every transaction is given timestamp when starting
- Guaranteed each concurrent execution is equivalent to serial execution in the timestamp's order.
- Any operations that violates timestamp ordering will be rejected and aborted (rollback)

## Types of Timestamps
- Transaction Timestamp (Ti) - given for transactions
- Write Timestamp (W-TS(Q)) - given for data items
- Read Timestamp (R-TS(Q)) - given for data items

## How it Works
### `read(Q)` by transaction Ti
**Case 1** `TS(Ti) < W-TS(Q)`
- Logic: Ti (older) tries to read Q, but Q is already **written** by a younger Tj
- Problem: The new value is Q is 'too new' in Ti's world, this violates serial order
- Consequence: Reject `read`, rollback Ti

**Case 2**`TS(Ti) >= W-TS(Q)`
- Logic: Ti (older) tries to read Q, but Q is already **written** by an equal or older Tj
- Consequence: accept read
- Update: `R-TS(Q) = max(R-TS(Q), TS(Ti))`

### `write(Q)` by transaction Ti
**Case 1** `TS(Ti) < R-TS(Q)`
- Logic: Ti (older) tries to write Q, but Q is already **read** by a younger Tj
- Problem: The write will make the value read by Tj be invalid, this violates serial order
- Consequence: Reject `write`, rollback Ti

**Case 2**`TS(Ti) < W-TS(Q)`
- Logic: Ti (older) tries to write Q, but Q is already **written** by a younger Tj
- Problem: Ti's write is invalid.
- Consequence: Reject `write`, rollback Ti
	- Note: Thomas's Write Rule has a different handling

**Case 3** `TS(Ti) >= R-TS(Q) and TS(Ti) >= W-TS(Q)`
- Logic: Ti is young, any older reads or writes can be written by a new transaction
- Consequence: allowed
- Update: `W-TS(Q) = TS(Ti)`

>[!summary] 
> - You can read on older data 
> - You can write on older data, or you can write if youre the youngest to write.

## Thomas's Write Rule
Specifically for Case 2 of write rule:
- `write` from Ti is ignored, and Ti can continue (no rollback)
- Logic: since Ti is older, Tj (younger)'s write will overwrite it anyway, so pretend it never happened
- Results: more concurrency, but only guarantees *View Serializability* not *Conflict*

## Guarantees and Problems
**Guarantees**
- Conflict serializability
- Deadlock free
	- Because no circular wait since there are no waiting
**Problem**
- Cascading Rollback still possible
	- Rollbacks are expensive
- Overhead (checking and updating timestamping)
- Starvation Possible (rollback repeatedly)


# Validation-based Protocol
- Optimistic & Pessimistic
- Three phases of execution
	- *Read Phase*
	- *Validation Phase*
	- *Write Phase*
- Read set and Write set
- Three timestamps
	- Start (Ti)
	- Validation (Ti)
	- Finish (Ti)
- Validation Testing

## Main Idea: Optimistic Concurrency Control
**Optimistic**
- Optimistic Assumption: Transaction's Conflicts are **rare**
- No locking, let transactions work freely
- Before commit, do a *validation test* to see whether conflicts actually happens

**Pessimistic**
- Assume conflicts happen often

## Three Phases 
1. Read Phase
	- Ti reads the database
	- Any writes are saved to a local variable (not written to database yet)
	- System keeps track of the Read Set (`RS(Ti)`) and Write Sets (`WS(Ti)`), which are all the data items that is read and *will* be written
2. Validation Phase
	- Starts when Ti is ready to commit
	- Checks if Ti violates *serializability* with any commited transactions
	- If it does, rollback Ti
	- Else, go to phase 3
3. Write Phase
	- Write write sets permanently to the database

## Timestamp for Validation
The timestamps used are different from Timestamp-based protocol.
- `Start(Ti)` - When Ti starts *Read Phase*
- `Validation(Ti)` - When Ti starts *Validation Phase*
- `Finish(Ti)` - When Ti starts *Write Phase*
*Serializabilty orders* are determined from `Validation(Ti)`

## Rules of Validation Testing
When validating compare Ti with all Tj such that `Validation(Tj) < Validation(Ti)`.
Ti's validation succeeds if for all Tj, one of these condition is satisfied:
1. Condition 1: `Finish(Tj) < Start(Ti)`
2. Condition 2: `Write Set(Tj)` $\cap$ `Read Set(Ti)` = $\varnothing$
	- No dirty reads

## Pros and Cons
**Pros**
- High concurrency
- Deadlock free
- Good for read heavy systems
**Cons**
- Expensive rollbacks
- Starvation
- Validation Overhead
