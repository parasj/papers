# Systems
## Key systems design principles
* Isolate the common case [Lampson 84]
  * *Prioritize a single use case*
  * Identify read versus write workloads and optimize accordingly
  * Identify need for distributed computing versus single node (LRPC)
ecure
* Think about consistency requirements carefully. Relaxing consistency can provide increased availability (Coda) or better performance
* Indirection can simplify design and decouple evolution of upper and lower layers of a stack
  * Examples: IP, OS, VMM, LLVM IR, SQL
* End-to-end arguments
  * Carefully think about implementing functionality at a lower layer if it must be implemented at a higher layer as well
  * Add it at a lower level if performance improves and does not compromise performance for other workloads that don't need it
  * RISC, IP, exokernels
* Specialization
  * Hold other dimensions of design constant while improving single attribute
  * Leverage semantics for one key workload (common case)
  * SQL focuses on structured data
  * CRDT focuses on a few commutative operations
  * Google FS optimizes append-only workloads
* Simplicity (Occam's)
  * easier to add complexity later, but hard to remove it
  * allows for fast iteration
* Get correctness first and then optimize later

## Systems tradeoffs
* Functionality vs performance vs `x` 
  * `x` can be usability, consistency, safety, security
* Performance vs portability
* Latency vs bandwidth vs fault-tolerance requirements [Clark 95]
* Fine-grained vs coarse-grained
  * coarse-grained provides performance but is more complex and less s
* Hardware vs software support
* Interactive vs batch systems

## Ballpark latency numbers (from Jeff Dean)
```
L1 cache reference ......................... 0.5 ns
Branch mispredict ............................ 5 ns
L2 cache reference ........................... 7 ns
Mutex lock/unlock ........................... 25 ns
Main memory reference ...................... 100 ns             
Compress 1K bytes with Zippy ............. 3,000 ns  =   3 µs
Send 2K bytes over 1 Gbps network ....... 20,000 ns  =  20 µs
SSD random read ........................ 150,000 ns  = 150 µs
Read 1 MB sequentially from memory ..... 250,000 ns  = 250 µs
Round trip within same datacenter ...... 500,000 ns  = 0.5 ms
Read 1 MB sequentially from SSD* ..... 1,000,000 ns  =   1 ms
Disk seek ........................... 10,000,000 ns  =  10 ms
Read 1 MB sequentially from disk .... 20,000,000 ns  =  20 ms
Send packet CA->Netherlands->CA .... 150,000,000 ns  = 150 ms
```
