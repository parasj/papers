# Summary

Mach is an early microkernel, an operating system design where most functionality. Key motivation was to design operating systems for multiprocessing where there is UMA, NUMA and no shared memory. It demonstrates that a message passing interface can be used to manage memory objects. Overall, communication and virtual memory management are complementary. Mach has good performance as it can pass communication through pointers to mapped memory.

Single level store is synonymous with virtual memory, that is that DRAM acts as a cache for secondary storage. By paging in files into memory, it avoids extra intermediate buffers that are allocated during copying. Mach adds support for memory objects that represent bytes with an action. This object oriented interface allows the programmer to implement file systems and other functionality. This is likely part of the reason that Camelot and Coda were implemented on top of Mach. Interesting ideas carry over to FUSE and user-space filesystems.

Basic primitives include a task, thread, port, message and a memory object. File systems are managed through memory objects. The kernel pretty much deals with protection, page lookup, shadow paging or CoW support and IPC.
