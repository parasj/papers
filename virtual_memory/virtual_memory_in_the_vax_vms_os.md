# Virtual memory in the VAX/VMS Operating System

This paper covers key design points of a virtual machine system pretty clearly.

Some relevant takeaways:
* The paper mentions that memory was cheaper than processors so it chose to make quick paging decisions at the cost of memory cycles. This is true again with the end of Moore's law so perhaps we can throw more memory at parts of the OS stack.
* Key design requirements are useful in general. They cover using batching for throughput limitations and also describe how to balance fairness in systems.
* With recent security vulnrabilities in the virtual memory system, how can we design a safer memory system?
* How is this impacted by 3D XPoint? Latency of lookups become expensive but we should be able to store more information per page. Should we use XPoint as another layer in the memory hierarchy or to replace memory altogether?

Key points:
* System has three key components: (1) design of the virtual address space, (2) design of the pager system that serves page faults and (3) design of the inactive program swapper.
* Key design requirements:
  * limit impact of a single process that makes heavy use of the paging system (solved with per-process page replacement)
  * high cost of programs slowly faulting their way back into main memory (solved by moving programs in batch with swapping)
  * increased disk workload due to paging (solved with clustering dirty write-backs)
  * cost of processor time searching page lists (solved with the TLB)
* Virtual address space design
  * Half for kernel (protected with bit) and half for each program
  * Program space is divided into program and the stacks
  * Each lookup takes two accesses, one to find the process page table and one to then look up within the process page table
  * There are elements of a trap vector, where pointers to shared routines are stored in a table so that they can be relocated without modifying programs.
  * The first page in program space is unmapped to lead to a fault upon uninitialized pointer errors (fail-fast).
  * *Page sizes were set to be too small in the PDP-11 due to latency-throughput requirements, which became obsolete quickly.*
* Pager system
  * Each process has a limited pool of pages and all page replacement occurs in this per-process pool
  * FIFO is used since process time is relatively more valuable than memory
  * Pages are moved to free and modified lists. Free lists avoid searching the page table and modified lists allow for batched writeback (and sometimes avoid work upon program termination).
  * Whenever pages are loaded or written back, operations are clustered. Additional extra pages are read into memory during a fault due to low marginal cost to load the extra pages. 
  * Page table entries count as part of a process's page limit.
* Swapper
  * Programs can be swapped to disk as a whole unit. This avoids the large cost of slowly faulting programs slowly.
  * This reminds me of VM migration - it's almost like how pre-copy is usually better than post-copy.