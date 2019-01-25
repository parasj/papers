### Composing Parallel Software Efficiently with Lithe

This paper (out Krste's own lab), demonstrates the idea of multi-level scheduling. It demonstrates how parallel computations, which each locally optimize for their execution, end up interfering when the system as a whole is run. Pan et al demonstrate "Harts" which represent the real cores on a machine. By scheduling directly to cores, the CPU cannot be overloaded with threads. This also allows for heterogenity among harts which also allows applications to share the resource more effectively.

## Criticisms
My main criticism of this work is that threads have useful behavior beyond accessing parallelism. For example, it is still very useful to use cores for IO bound work. Moreover, the hart concept is interesting but I wonder why common parallel libraries (they mention MKL and OpenMP) cannot implement behavior to determine if the CPU is oversuscribed.

## Key takeaways:
* Parallel software composes with other building blocks. So we must think about system performance / throughput instead of local behavior.
* Fate-sharing and aligning incentives is part of what helps systems like Lithe work; a sytem must share it's parallel computing resouces with child processes.
* Local optimization can have pitfalls like oversubscription. So care needs to be taken to avoid overcomitting resources.
