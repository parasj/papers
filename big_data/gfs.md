# The Google File System

* Master operations are logged and replicated to a failover master node
* Consistency is that data will be written atomically at least once even during concurrent mutations
* Data is replicated to the nearest replica so that replication occures as a chain. Data forwarding is also pipelined for efficiency

This paper details Google's design of a large-file distributed file-system. It stores data according to the following assumptions: 1) large files, 2) immutable when written and append-only, 3) tolerant to inconsistent state. Google File System is used to store Google's search indexes. and appears to be highly optimized for the batch processing workload (MapReduce?).

Google File System contains a single master that maintains state + metadata for the system. Each chunk server stores blocks on its disk in a linux FS. The master updates chunk availability by polling the chunk servers. The master maintains a fault-tolerant metadata store though logging and replication to secondaries.

Google File System appears to be highly tuned for the network topology inside Google. It sends data to the nearest replica in the network and also pipelines the loading of chunk data from a client (replicas copy data as soon as they recieve it).

My main criticism for this paper is that it has an unclear consistency model. Even after reading it twice, I cannot make sense of what guarantees it provides. It seems GFS provides little to no consistency? And on node failure, it seems that it can have different instances of a chunk on different replicas.
