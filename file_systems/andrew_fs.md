# Scale and Performance in a Distributed File System

AFS is a distributed file-system that underwent large scale in a prototype, motivating developments in caching and other areas. AFS runs a server called _Vice_ that minimum state needed for security and integrity and user-space clients called _Venus_ that relay requests to _Vice_. Reading and writing files occur on locally cached files on the FS. Thus, RPCs are only necessary on file open or close.

**Why are large-scale FS hard to build?**: A) large scale degrades performance, B) complicates day-to-day operation.

## Performance evaluation
**Key metric for cache systems**: Hit ratio
Optimization beyond hit ratio evaluated the distribution of RPC calls

## Cache management
Modifications are done locally and synchronized when file is closed. Directory modifications are made directly on the server, however.

**Callback interface**: Rather than checking with the server on every open, AFS instead assumes cache entries are valid until the server notifies it of external modification. This is almost like the cache invalidation protocol on CPUs. But notifications occur before the server accepts a write.

## Conclusions
AFS has become much-used infrastructure at CMU and availability has become more important (motivating Coda). Monitoring, fault-isolation and diagnostic tools are important infrastructure for future work. Decentralized administration as well as physical distribution of servers are other important research directions.
