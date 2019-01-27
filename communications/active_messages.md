# Active messages: a Mechanism for Integrated Communication and Computation

**Key idea**: Include code pointer in messages which avoids buffering latency. Code is run immediately on server, thus avoiding as much queueing as possible. Handlers must be fast. Get communication onto network ASAP and off the network into computation ASAP.

The paper discussed how to improve network and computation utilization by modeling the network as a pipeline. Messagers include a pointer to code that is shared on all machines. Messages are sent ASAP with minimal buffering and servers execute code as soon as they recieve a message. This asynchonously frees up the client to continue computing without the overhead of buffering along the network stack.

## Cost model; interleaved is faster than phases
Conventional model of programs is that they operate in distinct phases of computation and then communication (Batch Synchronous Parallel). This model programs means that execution time is strictly T<sub>compute</sub> + T<sub>communication</sub>. Interleaved execution with small communication (T<sub>compute</sub> >= 9 * T<sub>communication</sub>) means that total running time is effectively compute time.

## Programming models
Send and recieve is simple but isn't aligned with hardware. Blocking send-recieve is expensive due to three-phase protocol (handshake init, handshake confirmation, send data). Send-recieve can be asynchronous but it's difficult to utilize the network due to required parallelism. Async send-recieve introduces significant latency as well.

To avoid deadlocks, handlers must be fast and not busy-wait. Thus, the network can continue to recieve messages which allows it to remain deadlock free.

## Questions?
* How is congestion control handled?
* How is fault-tolerance handled?
