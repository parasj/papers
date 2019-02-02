## Practical Byzantine Fault Tolerance

Liskov presents a practical asynchronous implementation of a replicated state machine that can tolerate failiures. She notes that the system requires $3f+1$ nodes to ensure resiliency to $f$ failiures. This is because $f+1$ trustworthy nodes are required to ensure a correct quorum when $f$ nodes have failed. The algorithm is again a 3 phase commit protocol (1. primary recieves request, 2. primary has each replica apply the change and then "accept", 3. primary awaits replicas to have $f+1$ accepts.

Liskov presents a few key optimizations. First, digests are used to "summarize" updates instead of sending whole updates. Second, replicas can optimistically write changes to their state. Third, read requests are multi-casted to all replicas and can await $2f+1$ replies. MACs are used as fast ways to verify a digest. MACs have the downside that it can only be used by a single party, but this is OK since the nodes communicate with a primary. These optimizations allow their implementation to have a limited overhead compared to NFS.

My main criticism of the paper is that it assumes independent failiures. It seems difficult for a system designer to implement a different system for each replica.
