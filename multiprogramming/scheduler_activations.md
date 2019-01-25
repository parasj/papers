# Scheduler activations: effective kernel support for the user-level management of parallelism
This paper primary compares user-level threads with kernel-level threads. It proposes a modification to the kernel-thread interface to have efficient user-level threads with the correctness of kernel-level threads. It achieves this by changing the system interface to one with a "virtual multiprocessor" interface where the system can preempt or grand new multiprocessors to some address space. This creates consistent performance under blocking (e.g. I/O or syscalls).

Kernel-level threads have about 10x faster context switching than processes. This is attractive for tasks with rapid sequences of I/O and other operations. They operate pretty much the same way as processes (Linux schedules threads I believe, not processes). However, thread creation cost is cheaper than process creation costs. Threads allow multiple parallel programs to share the same address space.

User-level threads are more efficient (10x) than kernel-level threads but they can make suboptimal scheduling decisions in some situations. When the user thread scheduled on a kernel thread blocks, it will idle the CPU that it was running on. This leads to wastage and poor performance. _Go avoids these issues by replacing system calls and IO with custom shims that avoid the issue of blocking in a green thread._

Scheduler Activations proposes a hybrid approach where the kernel thread 

## Key takeaways:
* *User-level management of parallelism is more efficient than system-wide*
* Coarse-grained parallelism is more efficient than fine-grained parallelism. It's hard to schedule fine-grained parallelism directly.
* Local vs global? Pluggable global seems to be more efficient but industry has adopted more of a local approach.
