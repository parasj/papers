# Virtual memory
Overview: http://pages.cs.wisc.edu/~sschang/OS-Qual/memory/Memory.htm

## Segmentation vs Paging
Segmentation = variable user defined sizes for regions of memory. A segment is some linear portion of address space. Segment table contains the base and length of the segment as well as permissions. Address translation is very simple. Segments are convenient as they can be separately protected and can grow independently. Also, they can easily be shared between processes without significant issues.

However, segmentation suffers from issues of variable allocation. This leads to external fragmentation issues. Placement algorithms are more complex (software support). In Multics, a kind of hybrid approach is used which has significant complexity (variable sized segments with paging). Multics used a directory scheme to store segment lookups.

Paged memory is based on linear sequences of pages. Pages are fixed size so they are simple to allocate and manage. They also imply sending unused pages to disk or secondary storage. Each process has a separate page table within which a page refers to some entry which stores the hardware frame number.

Ultimately, segmentation is better as a logical unit of memory (thus better for protection and sharing) while pages are better as a physical unit of information as they simplify implementation. Both approaches are complementary, as Multics attempted. 

## Hardware support for virtual memory

Segmentation is very simple to support in hardware. One takes segment ID, looks it up in the table, checks permission, checks if the access is less than the length and then the address is `base + index`. However, segmentation has significant software support necessary due to implementation cost for placement.

It's critical in paging to increase performance using a TLB. This caches lookups at the page level. The TLB is split into a kernel section and user mode section. On context switch, the TLB is flushed. TLB is order 10x faster than main memory, so it makes accesses 2x faster.

## Memory vs compute
There is an interesting tradeoff between available memory and available compute. When memory is cheap, memory allocation should be fast even if it is not optimal. But when memory is relatively scarce, effort should be made to optimize allocation and paging. Working set theory provides a good upper bound for a reactive memory system. However, it is costly to implement. CLOCK style algorithms are cheap to implement and fast.

## Local vs Global allocation
Local estimates needs per process and allocates as such (WS) but global allocates without attending to per-process needs (CLOCK/FIFO). WSCLOCK is a mish-mash but in general would still perform worse than working set alone due to overcomitting memory in some cases. In VAX, local behavior could lead to thrashing with global policies so each process had a per-process page limit and page-replacement.

## Interactive vs batch system needs
Interactive systems often require far more memory than batch systems while keeping that memory around for longer. Interactive systems are latency sensitive but batch is often throughput oriented. In terms of memory, this can have some real impacts on systems that use secondary storage heavily. One issue is interactive systems that get paged out entirely. In VAX, they batch paging by program so as to avoid long migration times. Batching was also used for dirty writeback.
