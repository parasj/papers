# Finding a needle in Haystack: Facebook's photo storage

Haystack was motivated by their photo storage and serving system. It consists of many small files that were served off of an NFS store. As NFS is inefficient for small files due to the metadata overhead, a new system was desired. The key goals for the system were A) high-throughput + low-latency, B) fault-tolerance, C) cost-effectiveness, and D) simplicity. They architected the system hierarchy around URLs which serve as a simple way of tracing the content retrival within the HTTP request.

They note an interesing justification for using a cache for only write-enabled shard. Users access recent photos often after uploads, but it's important to shield write-enabled shards from read traffic. Thus, the cache protects those servers.

The store itself stores photos in a large log-structured file. This allows the system to retrive data with one seek as it just needs a pointer to disk (which can be stored in memory). Relevant metadata is stored in a header so no extra seeks are required, while reducing the need for redundant metadata.

I do like this paper, but I think various concepts would be updated in the modern day. Algorithms like consistent hashing I think would be relevant. My biggest criticism of the paper is that it's no longer as relevant in an age where SSDs are prevalant and cheap. File system metadata could easily be stored on flash while the files are stored on disk, a setup that is easily accomplished using ZFS these days.
