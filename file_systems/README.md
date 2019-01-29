# File systems

|Local FS|Distributed FS|
|---|---|
|[Basics](https://github.com/parasj/papers/blob/master/file_systems/basics.md)|[NFS](https://github.com/parasj/papers/blob/master/file_systems/sun_nfs.md)|
|[Unix Fast File System](https://github.com/parasj/papers/blob/master/file_systems/fast_file_system.md)||
|[Log structured FS](https://github.com/parasj/papers/blob/master/file_systems/log_structured_file_system.md)||
|[Comparision of journaling approaches](https://github.com/parasj/papers/blob/master/file_systems/journaling_file_systems.md)||
|[Case for RAID](https://github.com/parasj/papers/blob/master/file_systems/case_for_raid.md)||
|[HP AutoRAID](https://github.com/parasj/papers/blob/master/file_systems/hp_autoraid.md)||


## Performance vs persistence tradeoff
In many file systems, there is a trade off between durability and performance. High performance can be achieved by batching/buffering writes but that decreases durability. This leads to the fault-tolerance vs latency vs throughput tradeoff in some ways.

## Small file vs large file performance
A key design point for file-systems is if they are mainly optimized for large numbers of small files or a few number of large files. Decisions like block size, number of inodes, batching etc affect this.

## Read-only, write-only, immutable, mutable, append-only
Some systems improve performance by restricting the model for modifying data. GFS is optimized for append-only data. DynamoDB optimizes mutable data. Haystack optimizes photo storage using large log index structures.

## Erasure coding vs replication
Erasure coding increases storage overhead moderately but increases overall write throughput and read throughput. However, replication is simpler and requires less CPU overhead. E.g. OceanStore uses parity while Chord uses replication
