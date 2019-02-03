# Dynamo: Amazon's highly available key-value store

**Key idea**:
* Reliability and availability are more important than consistency at scale for Amazon
* Dynamo is a DB designed for the edge cases in latency (p99) and availability under network partitions
* Add to cart example is pretty much a CRDT
* Key techniques:
  * Partitioning => Consistent hashing
  * Write availability => vector clocks with reconcillation on reads
  * Fault-tolerance to node failure => hinted handoff where only a subset of replica list needs to write data
  * Fast node synchonization => Merkle trees to quickly check stored keys
  * Detecting failed nodes => heartbeats to other nodes

## Overview
* Key design choices:
  * Who performs reconcillation? Application, not system
  * When to perform reconcillation? At read time so Dynamo is always writable
  * Scalability? Horizontal not vertical
  * No master node, all nodes are symmetric for ease of deployment
  * Not BFT
  * Zero-hop DHT as all nodes can route directly to the data

## Related work
### Dynamo vs Oceanstore
* Oceanstore is a global transactional persistant storage service.
* Oceanstore resolves conflicts by linearizing updates.
* It stores data on an untrusted infrastructure.

### Dynamo vs Bigtable
* Bigtable stores sparse multi-dimensional sorted maps while Dynamo only stores key-value pairs

### Dynamo vs GFS
* GFS is mainly designed for append-only writes

## Review

Amazon presents the design of a highly-available key-value store that relies on applications to resolve many consistency issues that have arisen with prior techniques to achieve large scalability with availability. Dynamo's core techniques include: 1) consistent hasing, 2) immutable object versioning and 3) gossip-based leader election and failover. The primary motivating example presented in the paper is their shopping cart application.

Amazon discusses the limitations for many relational stores as they introduce significant complexity for operations while limiting replication due to the focus on consistency. Instead, Dynamo prioritizes availability and instead offers weak consistency. The SLA for Dynamo is $\text{p999} < 300\text{ms}$ . It's interesting as this paper describes the concept of tail latency instead of medians or averages.

To achieve fault-tolerance of the data, Dynamo uses replication on the hash ring to ensure data doesn't disappear when nodes join and leave. Moreover, nodes maintain the routing table locally for the whole cluster so they do not need to route through other nodes. This bounds the tail latency.

Overall, I like the Dynamo paper a lot. However, my main criticism of the paper is that it is fairly complex and it's conflict resolution protocol only works with a few classes of data structures reliably. Moreover, the idea of applications resolving conflics seems unecessarily complex to me.
