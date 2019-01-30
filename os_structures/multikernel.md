# The Multikernel: A new OS architecture for scalable multicore systems

**Key idea**: Increasing heterogenity in systems motivates modeling multicore systems as distributed systems. Three principles guide multikernel design (1) make all inter-core communication explicit, (2) make all OS structure hardware-neutral and (3) replicate state across cores instead of sharing state.

## Why OS is slow?
Ousterhout describes that core speed is increasing faster than disk and memory latency. So operating systems still block on memory and disk. Message passing is more efficient than shared memory at scale. So the multikernel embraces message passing (much like Mach).
