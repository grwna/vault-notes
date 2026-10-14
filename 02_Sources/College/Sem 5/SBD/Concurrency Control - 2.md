# Deadlock Concept
## Keywords
- 4 Conditions of Deadlock
- Deadlock Prevention
- Pre Declaration
- Total Order

## What and Why
Deadlock is when two operations is waiting for eachother, making no progress.

**4 Conditions**
- Mutual Exclusion
- Hold and Wait
- No Preemption
- Circular Wait

## Deadlock Prevention
The strategy is to "attack" or eliminate one of the 4 conditions

**Attack "Hold and Wait"**
Pre-declaration
- All transactions must acquire **ALL** locks that it requires in the beginning. If all locks are can be acquired, transaction run. Otherwise it cannot hold any locks and must wait.

Weakness
- **Difficult**: transactions often not know ALL the locks it need
- **Wasteful**: will hold locks for way longer than it needs
- **Low Concurrency**: makes transactions more serialized than concurrent

**Attack "Circular Wait"**
Impose Total Order
- Assign ordered numbers to data items (ex. A=1, B=2, C=3)
- Transactions can only request for locks in ascending order
- This makes $T1(\text{hold A}, \text{request B})$ and then $T_{2}(\text{hold B}, \text{request A})$ **impossible**

Weakness
- Not flexible, the order of allowed data access may not be the same as the transactions requirement order.

# Deadlock Avoidance
## Keywords
- Prevention vs Avoidance
- Transaction Timestamp
- Wait-Die
- Wound-Wait
- Preemptive

## What and Why
Deadlock Avoidance is a dynamic approach to handle deadlocks.
- Different from prevention which applies static rules at the beginning
- Avoidance checks each lock request at runtime
- If a lock request potentially causes deadlock later, the system will postpone it or rollback some transactions.  

**Timestamp**
Avoidance is most commonly implemented using Timestamp (TS)
1. Each transaction given unique TS when it starts
2. System uses TS to decide which should wait and which should be rolled back
3. Assumption: $TS(Ti) <TS(Tj)$ means $Ti$ is older.

## Schemas
**Schema 1: Wait-Die**
Non-preemptive

Mechanism:
Assume $Ti$ requests lock that $Tj$ holds:
1. if $Ti$ is older:
	- $Ti$ waits
2. If $Ti$ is younger:
	- $Ti$ dies and rolled back
	- Younger trx is not allowed to wait for older trx because this can be the start of a cycle

**Schema 2: Wound-Wait**
Preemptive
Assume $Ti$ requests lock that $Tj$ holds:
1. if $Ti$ is older:
	- $Ti$ wounds $Tj$
	- This forces $Tj$ to rollback and release its lock.
2. If $Ti$ is younger:
	- $Ti$ waits

**Wait-Die**: the lock requester dies
**Wound-Wait**: the lock holder dies

**Both** can cause starvation 

# Deadlock Detection and Recovery
## Keywords
- Wait-for Graph (WFG)
- Deadlock Recovery
- Step 1: Victim Selection
- Step 2: Rollback
- Total Rollback
- Partial Rollback
- Starvation

## Deadlock Detection
Let deadlock happens, detect, then recover it at the end.
- **Pros**: no overhead for each request
- **Cons**: Deadlock can stall sistem for a while before detected

**Wait-for Graph**
Most common detection method:
1. Node: Active transactions
2. Edge: directed edge from *requester/waiter* to *holder*

**Deadlock** happens when there's a cycle in the WFG.
The WFG cycle finder can be run:
- Periodically
- Every time there is a wait

## Deadlock Recovery
Cycles have to be broken by *rolling back* one or more transaction in the cycle

**Step 1: Victim Selection**
Which transaction should be *rolled back*?
Factors:
- Priority: dont roll back important transactions
- Cost of rollback
- Transaction elapsed runtime
- How many locks are held?
- How much data has been modified?
- How many other transactions have to also be rolled back?

**Step 2: Rollback**
- Total Rollback: abort transaction so it starts over
- Partial Rollback: abort only needed operations within the transactions. More efficient but difficult to implement (require ***savepoint***)

**Starvation**
Sisyphus transaction

Solution: track rollback amount, and add as a factor for **victim selection**

>[!note] Endnote
> Detection is more commonly used because deadlock are rare, and the cost of avoidance/prevention is quite costly.,