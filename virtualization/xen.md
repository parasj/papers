# Xen and the Art of Virtualization

**Key idea**

* Machine resources are greater than individual OS needs. Virtualization is useful but need to provide functionality and performance.
* Xen uses paravirtualization where a guest OS runs on a host OS.
* Why paravirtualization instead of full virtualization?
  * Efficiency
    * Full virtualization has issues aroind efficiency since x86 was not designed for virtualization. VMWare ESX has a high performance cost for update-heavy workloads.
  * Time and other capabilities
    * Time virtualization can support real-time workloads
    * Page coloring and superpages can be implemented
  * Can balance local and global optimization as information can flow from VM to host
* Interface
  * Virtual memory
    * Guests have read access to page tables but must update them through VMM
    * Hypervisor lives in top 64MB of virtual memory so that it can reuse the TLB
    * Ballooning in the guest VM can reclaim memory
  * CPU
    * Guest OS runs at a lower ring than host
    * Guest registers trap vector table with VMM
    * System calls utilize handlers for faster operation
    * Interrupts are virtualized as events
    * Guests are aware of virtual and real time
  * IO: Access is through synchronous IO rings

## Review

Xen is a classic paper with a lot of impact. It proposes a practical design for a paravirtualized VMM. They argue that the technique in VMWare ESX leads to large complexity and a performance penalty (due to dynamic rewriting). Instead, Xen modifies the OS in small ways to interact with primitives provided by the Xen VMM.

Xen presents 3 classes of resources that need to have interfaces: Memory, CPU, and IO. Memory should support segmentation (in safe manner) and paging. The CPU should support lightweight interfaces to interrupts and syscalls while still supporting standard interrupts. Time should also be properly handled. Finally, IO is supported using asynchonous IO rings. Of all concerns, memory is the most difficult provision to guarantee safe and performant isolation. This is due to an "uncooperative x86" which does not support software virtualization of the MMU + TLB. x86 forces a TLB flush on address space switch. Xen lives in a fixed portion of address space so that no TLB flush is needed when it runs. Moreover, the guest OS manages it's own PT on hardware for performance. CPU is then virtualized using timeslicing.

The authors demonstrate that paravirutalization incurs minimal cost of changes - <2% LOC. this is better than other work in the paravirtualization space. I like this paper a lot, but my main criticism for the paper is that I think the paper should have instructed computer architects on how they can modify future designs to better support virtualization. Intel ended up implementing multi-level page-table mechanisms for performance, but I think the authors could have proposed better mechanisms and have discussed the implications of those architectural changes on their system.
