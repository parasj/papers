# Extensibility, safety and performance in the SPIN operating system
## Key ideas
* SPIN allows for imported extensions by dynamically linking new functionality into the kernel. 
* Type safe language is used to write extensions to provide assurance that no protected instructions or memory regions are used. Compile-time checking prevents pointer forgery or illegal dereferencing.
* They note three way tension between extensibility, safety and performance in OS

## Key principles
* Colocation in same address space
* Enforced modularity
* Local protection domains in kernel (resolved at link time)
* Dynamic call binding with event handlers

## Mechanics
* Extensions are handlers for events in the kernel. Extensions can watch and respond to events in the kernel.
* Memory
  * SPIN decomposes memory into storage, naming and translation.
  * Clients can raise the `Allocate` event to requires memory and the kernel installs these mappings into the MMU.
* Threads
  * Scheduler activations shows how kernel threads should evolve with user-level threads, but it is high overhead due to context switches
  * Two events `Block` and `Unblock` while strands can be checkpointed or resumed 

## SPIN vs exokernel
SPIN view OS as mostly good for common case and may have minor modifications for performance or drivers. Exokernel sees OS as something that requires major modifications in practice. SPIN claims that exokernel does not provide an extension model for people writing extensions while SPIN provides event-based architecture.

See Hakim's slides at http://www.cs.cornell.edu/courses/cs6410/2010fa/lectures/08-extensible-kernels.pdf.

## SPIN vs microkernel
Microkernel is not focused on extensibility as much as it has mostly fixed abstractions compared to SPIN and exokernel.
