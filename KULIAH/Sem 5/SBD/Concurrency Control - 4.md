# Multiversion Timestamp Ordering
## Main Idea: Multiversion Schemes
MVCC is an approach where systems keeps multiple versions of data items.
Ideas:
- Each writes will create a copy of a data item, old data will be kept temporarily
- Each version will be labeled (e.g. with timestamps)

**Benefits**
Biggest benefit: reads do not ever wait for writes
- When reading, the sytem will find the best version of Q, for example the one that was written before other transactions write to it
- Increases concurrency drastically

## Multiversion Timestamp Ordering (MVTO)
MVCC implementation using timestamps. Similar to timestamp based protocol, but with versions.
**Timestamps**:
- `TS(Ti)`
- For each version of Q:
	- `W-TS(Qk)`
	- `R-TS(Qk)`

**MVTO Read Rule**
Ti wants to read Q
- System finds `Qk` such that `W-TS(Qk) <= TS(Ti)`
- Return `Qk` to `Ti`
- Update: `R-TS(Qk) = max(R-TS(Qk), TS(Ti))`

**MVTO Write Rule**
Ti wants to write Q
- Ti has to read Q (subject to read rule)
- Validation test 1: `TS(Ti) < R-TS(Qk)`
	- Ti (older) wants to write, but Qk has been read by a younger Tj
	- Violates *serializability* Abort Ti
- Validation test 2: `TS(Ti) = W-TS(Qk)`
	- Rollback
- If passed validation test 
	- Create a new version `Q_new`
	- `W-TS(Q_new) = TS(Tj)` and `R-TS(Q_new) = TS(Ti)`


# Multiversion 2PL
Combine MV with 2PL. 
Main idea: divide transactions to two types:
- Update Transactions: *may* require read and writes 
- Read-Only Transactions: only does read, will never do writes

**Rule for Update Transactions**
- Uses rigorous 2PL
- Obtain lock-S for reads, lock-X for writes, hold all locks until commit or abort
- When updating write(Q) create a new version, which will be locked with lock-X until commit

**Rule for Read-only Transactions**
**No locks at all**, only uses timestamps and multiversion
-  When Ti starts, give unique timestamp
- Read:
	- Read Qk such that `W-TS(Qk) <= TS(Ti)`
- Commit (without validation)

**Pros and Cons**
**Pros**
- Guarantees Conflict Serializability
- No waiting:
	- RO dont wait for lock from update (no locking)
	- Update dont wait for lock from RO (RO no locking)


# Snapshot Isolation
**Main Idea**
Each transaction Ti takes snapshots of a database when it starts.

**Why**?
The need for a new level of isolation: *Serializability* is the strongest guarantee, but can be too strict or expensive.

*Snapshot Isolation* is a level of isolation:
- Weaker than *serializability*
- Stronger than *read commited*
- High performance (especially for reads)

**Execution Rule**
1. Read
	- Read the version of Q that is in Ti's *snapshot*
	- This Q is the latest version that is committed when Start(Ti)
	- Read operations are never blocked
2. Write
	- When writing, Ti writes to a private version
3. Commit (Validation)
	- When Ti wants to commit, it has to pass a test: *First Committer Wins*

**First Commiter Wins**
Ti's validations fails and will be rolled back if $\exists T_{j}$ such that all conditions are satisfied:
- Tj is concurrent with Ti (overlap)
- Tj commits before Ti
- Tj writes at least one data items that Ti also writes
In other words: in the case of a Write-Write conflict, first committer wins

**Snapshot Isolation Anomaly: Write Skew**
See example at the bottom of the page: [Snapshot Installation](https://if-notes.naufarrel.tech/02.-Catatan/IF3140-Sistem-Basis-Data/UAS/Snapshot-Isolation)


# Other Phenomenons and Weak Concistency
**Phantom Problem**
Standard locking on rows are not enough to handle INSERT or DELETE operations.
T1 runs the same query multiple times, but getting different results.
The results from T1's query is non-repeatable.

**Solution: Index-Range Locking**
Locks not just on rows but on index ranges, other transactions will have to wait until T1 commits or aborts.

**Weak Levels of Consistency**
Isolation Level is the trade-offs for concistency vs concurrency:

| Isolation Level | Dirty Read (Uncommited Reads) | Non-repeatable Read | Phantom Read |
| --------------- | ----------------------------- | ------------------- | ------------ |
| Serializable    | Not Allowed                   | Not Allowed         | Not Allowed  |
| Repeatable Read | Not Allowed                   | Not Allowed         | Allowed      |
| Read Committed  | Not Allowed                   | Allowed             | Allowed      |
| Read Uncommited | Allowed                       | Allowed             | Allowed      |
