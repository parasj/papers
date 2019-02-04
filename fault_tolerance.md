# The Transaction Concept: Virtues and Limitations
**Key ideas**:
* This paper gives an overview of the goals of transactions
  * atomicity (all or nothing)
  * consistency (maintain DB invariants)
  * durability (effects survive failure)
* Isolation was added later to represent how transactions affect other transactions (read uncommitted, read committed, repeated read)
* Even with a near perfect system (like NonStop), transactions are still needed to protect against user failiures or programming errors. Resillient designs fail-fast.
* Key principle in accounting is to never modify accounting books => time domain addressing
* Logging and locking is another way to accomplish these techniques.
  * Deadlocks can be dealt with by forcing a running transaction to revert
