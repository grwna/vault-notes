Recovery System is to guarantee Atomicity and Durability

Algorithms have two parts:
- Actions on normal operations
- Actions after failure

Two Phases of Recovery On Failure
**Redo-Phase**
- Scan forward from checkpoint to end
- Redo every operation
- If found `<Ti, start>` add to undo-list
- If found `<Ti, commit> or <Ti, abort>` remove  from undo-list (canceling the 3)

**Undo Phase**
- Scan log backwards
- If an operation is from Ti that is inside the undo-list, undo (with CRL)
- If found `<Ti, start>` of Ti in undo-list, add `<Ti, abort>`, then delete Ti from undo-list
- Repeat until undo-list empty

**Log Force**
Every commit will force Log buffer to flush to disk. 
**Write Ahead Logging**
Logs of transactions will always be written to disk before the transactions data, no matter what.

**Shadow Paging**
- non-log based recovery
- main idea: dont overwrite consistent data on disk, write new version somewhe else
- Uses page tables to map which version of data the current session is using
	- Shadow page table: permanent page table
	- Curent page table: the page table used for current session
- Inefficient (redundancy)
- After commiting, the current page table becomes the shadow page table, previous shadow page table is now garbage

**Recovery Process**
- After crash, just use back the persistent shadow page table
- No need for undo or redo
**Pros and Cons**
Pros
- No log overhead
- Trivial Recovery
- Fast Recovery
Cons
- Commit Overhead
- Data Fragmentation
- Garbage Collection
- Low Concurrency:
	- If Ti commits, Tj is forced to commit, even if its not done

**Disaster Recovery**
- One-Safe - data is commited if the log is written to primary site
- Two-Very-Safe - data is commited if the log is sent and copied to backup site
- Two-Safe
	- When backup is online, use Two-Very-Safe
	- When backup is offline, use One-Safe