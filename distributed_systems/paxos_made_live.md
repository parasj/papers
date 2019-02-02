# Paxos made live

This paper describes the practical challenges encountered when implementing the Paxos protocol by Google in their Chubby lock service. Paxos provides a basic algorithmic subsystem that ensures consistency in the presense of node failures. Paxos alone describes a system for a single value, but a more complex multi-paxos describes a system for many key-value pairs.

Issues the authors address include: 1) code complexity (KLOCs), 2) difficulty in proving correctness of a long codebase and 3) real-world errors not covered in the papers.

Paxos operates as a three-phase-lock: 1) leader election, 2) broadcast value to all replicas and wait for majority acknowledgement and 3) commit. If a minority of non-leader nodes fail, then consistency is preserved. If the leader dies, then a new leader can emerge and join the cluster by using a GUID monotonically increasing sequence number. This will force out future updates from a stale leader. *I do not quite understand what happens if a leader dies in between stage 3 (some nodes commit and some do not)*. Multi-paxos extends single value Paxos in order to run multiple Paxos instances for each node. It seems that a key challenge in multi-paxos is that catching up lagging nodes leads to slow load times due to the need to flush to disk. Disk seek times are therefore a key challenge (NVM seems like a potentially new technology with applicability here).

I like this paper a lot. But it would have been great if the authors released the open source code to their Paxos implementation after such arduous work. This is technology that would have huge impact if more broadly released.
