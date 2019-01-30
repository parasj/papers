# Disconnected Operation in the Coda File System

Coda is a successor to AFS that explores the design of a distributed FS that can operate in weakly connected and disconnected situations. It notes that caching can improve availability as well as performance.

**Key methods**:
* Hoarding, where clients hoard manually specified and recent files locally on their disk
* Whole file caching which simplifies implementation of consistency.
* Consistency managed with callbacks for files where server notifies parties when a file is dirtied.

## Replication
* Serverside replication; volumes can have read-write replicas on more than one server (VSG)
* Clientside replication; clients can hoard files locally
* Callbacks ensure that data remains consistent. Clients are notified when their cached copies are no longer the latest copy.
* Disconnected operation will use local cache and propogate modifications upon reconnection.

## Scalability
* Need to tradeoff consistency availability. When system is unavailable, enter reduced consistency operation
* AFS hit scalability limits, so Coda needs to address it directly
* Scalability through whole-file caching and through callback cache coherence
* Put as much functionality on clients as compared to servers

## Optimistic vs pessimistic replica control
* Pessimistic
  * Pro: Always consistent
  * Con: Unavailability. A single client could lock up entire file or directory.
* Optimistic
  * Pro: High availability
  * Pro: High throughput
  * Con: Danger of conflicting writes, relies on resolution protocol
* Leases
  * Pro: avoids issue of an offline client locking the system indefinitely
  * Con: when lease expires, disconnected client loses access to a cached object even if it is still available

## Client structure
* Most complexity is in Venus, a user-space client library
* Built on vnode interface. Venus is called to open or close a file but reads and writes proceed direcly to the local cached file.
* A small in-kernel MiniCache decreases number of context switches
* Venus is in one of three states
  * Hoarding
    * hoard database stores paths for items that should be caches
    * can put priorities and reference to entire directories
    * hoard walk periodically restores equillibrium between recent and explicit cache
    * refetch purged cache object upon next hoard walk
    * directories allowed to become inconsistent as most operations are adding or removing items
  * Emulation
    * replace the function of the server
    * logging for fault-tolerance
      * save replay log locally
      * compact entries to log to limit cache growth
    * RVM (camelot) keeps integrity of metadata during disconnected operation
  * Reintegration
    * Replay log is executed at each volume in parallel
    * On conflicts, users use a debugging program to replay selectively
