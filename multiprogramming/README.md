# Multiprogramming

Overview: running processes on multicore systems requires coordination, conflict resolution, etc. How to design systems for these multicore systems? How should OS manage memory and schedule tasks?

## Message passing vs shared memory
Message passing and virtual memory are both duals of each other. Functionality in one can easily be implemented with the other. Moreover, it seems empirical performance is similar.

Mach initially explored this dual and showed similar performance through complementary use of virtual memory and message passing. 

## User threads vs kernel threads
[StackOverflow post](https://stackoverflow.com/questions/15983872/difference-between-user-level-and-kernel-supported-threads)
Summary is that user level threads are cheaper but make sub-optimial scheduling decisions and also have issues with blocking user calls. Kernel threads provide that functionality. Green-threading systems make this work by convering blocking calls to asynchronous calls. Scheduler Activations has a hybrid approach where resources are provided and revoked with explicit communication.

## Fine-grained vs coarse-grained processing
Fine-grained parallelism has less implementation cost but a large scheduling overhead which makes it less efficient. Coarse-grained is more efficient but is more complex overall. One guiding principle is to aggregate composed fine-grained paralleism into coarse blocks that are efficiently scheduled (see Kubernetes pods, Lithe threading library, GPU architecture, etc.)

## Local vs global scheduling
Global scheduling has better overall performance since scheduler can make inter-system decisions. But it has issues like starvation or convoying. Local systems may have worse overall performance but achieve better optimizations at the local level. But local scheduling does not lead to overprosioning.

### Economic scarcity as a way to avoid overcomitting resources
This relates closely with scheduling. But Lithe and Scheduler Activations treat resources as scarce objects that are granted and revoked from processes. Visible recovation is a useful technique to ensure that local optimizers perform collaboratively. Similarly, the VAX virtual memory system performs page replacement per-process which avoids issues with processes allocating and deallocating pages to quickly.

## Read heavy? or write heavy?
Read-copy update demonstrates that workload asymmetry can influence system design. They reduced locking overhead to zero for reads with limited cost on writing.
