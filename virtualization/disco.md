## Disco: Running Commodity Operating Systems on Scalable Multiprocessors

Bugnion et al show how virtualization can allow a single OS to run on a SMP without drastic changes to code. They demonstrate that multiple copies of the OS can run concurrently on a single resource and allow the user of the OS to utilize all resources on the machine. They mitigate performance issues w/r to core datastructure synchonization by sharing memory and buffers.

I buy the benefits of a VMM for OS resource management. As an OS is primarily responsible for fine-grained resource management and isolation, the VM allows the system controller to move memory as needed between hosts. Thus, some resource management functionality need not be globally shared in a single OS but instead be accomplished hierarchically. They note that VMMs introduce overheads and also acknowledge that less optimization is possible with local-information only.

As there is a VM, memory must be mapped still. As the kernel runs on the VMM, it must be relinked so that it runs in mapped regions. A software-TLB also smooths performance issues due to TLB contention. Disco also captures all device access requests and has a single trap interrupt handler. Networking for IPC is accelerated using COW so that data movement between kernels need only happen though remapping. 

Simulation demonstrates poor performance in applications with high memory contention. The TLB is a significant bottleneck still. My main criticism of this paper is that I think memory performance issues are the largest factor limiting the speed of VMMs and microkernels. Also, it appears there is still a non-trivial amount of kernel changes needed to accomplish good performance (a la paravirtualization).
