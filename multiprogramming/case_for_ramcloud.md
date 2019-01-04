# The case for RAMClouds: Scalable high-performance storage entirely in DRAM

*Key point*: Disc bandwidth is too low to support huge capacities today, thus relegating them to archival purposes. Instead, services should be built on scalable storage that is in-memory. This provides high throughputs (1M qps) and low latencies (10 microseconds). Fault-tolerance can be provided through replication. These systems simplify much of large-scale system design (like databases) and avoid building ad-hoc scalability techniques.

**Summary:**
* Motivating example (Facebook)
  * 4k MySQL servers, but 2k memcached servers (storing 25% of data).
  * Total memory used by all DB servers was ~75% of all data stored.
  * Why not just store all data in RAM then?
  * Caching is imprecise and sensitive; 1% increased miss rate results in 10x perf. hit for DRAM
* Why RAM if latency is good enough now?
  * System designers have mostly accepted the state-of-the-art, but a single web hit to FB results in 130 internal RPCs.
  * Databases have also been highly optimized for disks (indexes, columnar stores, etc). Stonebraker predicts end of one-size-fits-all for databses due to disks.
  * RAM could provide one-size-fits-all again for DBMS.
* Why not flash memory?
  * Key advantage is that memory access is faster than going through OS drivers and interrupt handlers.
  * DRAM is getting cheaper cost-per-bit
* Open research questions for RAMClouds
  * Low-latency RPC
    * Ethernet switches can cost 500 usec RTT
      * Cut-through routing can get down to 1 usec, where packets are immediately routed as soon as header is read
    * Interrupts cannot sustain low latencies - networking stacks will likely need to move to using dedicated cores that poll network interfaces
    * VMM adds a lot of latency, even with IO rings. We will want to see more user-space networking to bypass kernel
    * TCP is not latency-optimized; retransmission windows are >100ms, flows are not as important for RAMClouds and acknowledgement overheads are significant at the packet level versus object level.
  * Reliability and fault-tolerance
    * To manage single-system failure (not power)
      * Writes can be sent to two other servers to replicate in memory
      * Asynchronously, each replica can log to disk
      * Log-structured file system approaches of log cleaning can compress logs over time
      * To resume operation quickly, files can be sharded across many servers to quickly read snapshots in parallel.
    * To manage power failure:
      * Servers could be notified of impending shutdowns (e.g. by a generator)
      * Application support for truncated logs
      * Compromise on write-latency in order to write data to disk
      * ? could non-volatile memory be used to avoid this issue?
  * Transactions in distributed systems
    * BigTable only supports single-row transactions
    * Dynamo provides eventual consistency
    * Authors suggest ACID maybe is feasible since concurrent transactions will be reduced due to faster commit times (but throughput increases?)
      * With less concurrent transactions, then optimistic concurrency control can be efficient