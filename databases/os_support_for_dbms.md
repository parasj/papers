# Operating System Support for Database Management
**Key idea**: OS provides support for all applications which leads to generally high overheads. Instead, OS should be slow and take advice on some decisions from the applications.
 
## Buffer pool management
* While page cache can make applications faster, it requires syscall overhead. DBMS manage buffers in user-space to avoid context switch overhead.
* LRU is sometimes the opposite of optimal for a DBMS (10-15% miss rate opportunity gap). Instead, OS should take advice from the application.
* OS prefetches sequentially but DBMS reads somewhat randomly. But the DBMS know what is the next page it wants to read is.

## File systems
* Character array FS is not a great abstraction for DBMS
* Can DBMS be oriented as a tree-structured FS?

## Scheduling and IPC
* Server oriented models of DBMS and the process-per-user model are not ideal for either system. Instead, can there be a fast path function for DBMS consumers?
* Task switch overheads are too high in general
