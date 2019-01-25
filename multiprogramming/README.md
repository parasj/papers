# Multiprogramming

Overview: running processes on multicore systems requires coordination, conflict resolution, etc. How to design systems for these multicore systems? How should OS manage memory and schedule tasks?

## Message passing vs shared memory
Message passing and virtual memory are both duals of each other. Functionality in one can easily be implemented with the other. Moreover, it seems empirical performance is similar.

Mach initially explored this dual and showed similar performance through complementary use of virtual memory and message passing. 
