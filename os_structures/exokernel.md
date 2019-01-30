# Exokernel: an operating system architecture for application-level resource management

**Key idea**: export machine functionality with secure bindings so that extensions can leverage those bindings to improve performance. Limited functionality was imported for performance like packet filters.

This paper details Exokernel, an approach to operating system design that improves performance of the operating system by enabling applications to link against library OS's that interface with basic primitives provided by the base OS. This approach is similar in a few ways to a VMM but it seems like it depends on close integration of applications with a library OS.

The problem motivating Exokernel is that the two-level protection mechanism in OS leads to large costs during syscalls and other functionality. Applications know their workloads best and therefore can tweak how the kernel operates in order to enable better performance. The key idea in the solution is to separate system protection from management. Aegis (base OS) handles protecting system intgrity (e.g. framebuffers and disks) while enabling the library OS to take control of management.

As an example, virtual memory is handled by having a pool of pages that applications can request from. The exokernel stores the context of all pages and then allocates the pages to library OS page tables. TLB faults are carefully routed to the library OS. Many kernel functions are simplified as it operates on unmapped data, and therefore does not need to be as careful when modifying structures.

The exokernel approach is interesting. Library OS's have become more popular recently with the rise of containers. My main criticism is that the system would seem to have poor optimization of tasks like scheduling and networking as it is sacrificing global control.

## Exokernel principles:
1) Separate protection from management (policy)
2) Expose names (access hardware directly)
3) Expose allocation
4) Expose revocation (politely ask for resources back, then forcibly)
5) Expose information

## Exokernel responsiblity
* IPC
* VM
* Scheduling
* Networking

## Exokernel vs microkernel
Exokernel's focus is similar to microkernel in many ways but takes a different stance as microkernels value primarily minimalism.
