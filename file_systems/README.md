# File systems

## Performance vs persistence tradeoff
In many file systems, there is a trade off between durability and performance. High performance can be achieved by batching/buffering writes but that decreases durability. This leads to the fault-tolerance vs latency vs throughput tradeoff in some ways.

## Small file vs large file performance
A key design point for file-systems is if they are mainly optimized for large numbers of small files or a few number of large files. Decisions like block size, number of inodes, batching etc affect this.

## Read-only, write-only, immutable, mutable, append-only
Some systems improve performance by restricting the model for modifying data. GFS is optimized for append-only data. DynamoDB optimizes mutable data. Haystack optimizes photo storage using large log index structures.
