# Spectre Attacks: Exploiting Speculative Execution
**Key idea**: Side-channel where attacker poisons branch predictor so that it branches true. Then CPU will take a branch into a conditional and execute a lookup then cache access in the attacker's memory. Even though the CPU clears state on branch mispredict, it doesn't flush the cache. Thus latency can determine the contents of some data.

Spectre is a class of attacks that depends on speculative execution using branches. The CPU speculatively executes a prohibited lookup elsewhere in RAM. And this lookup can be checked similarly to Meltdown. What is different though is that it relies on retraining the branch predictor in order to call the poisoned array lookup. 

Spectre can be implemented in Javascript using high resolution timers. A crude enough timer can be implemented using a spinning thread in a webworker. This is a very surprising result. Moreover, the attack can be used to call into code anywhere else, which is quite dangerous. This attack affects ARM processors as well which is worrisome due to the large number of mobile devices that are deployed.

This paper is overall a good paper but is less clear than the Meltdown paper. Both are similar attacks in many ways. It does address more steps for computer architects to consider in future designs.

# Meltdown: Reading Kernel Memory from User Space
**Key idea**: The key to meltdown is basically that an attacker raises a trap exception and immediately after performs the protected value lookup then cache access. Thus, it can reliably detect secured data. There is a mitigation through KASLR called KAISER. Browsers also rate-limit syscalls as well.

Meltdown is an attack on x86 systems that takes advantage of a side channel attack. It has a mitigation based on kernel space address randomization that relies on placing a minimal set of datastructures in user space. Thus, there is a user space and kernel space page table. This hurts performance, however. The core of meltdown attack, annotated (simpler than to describe in text):

```assembly
1 ; rcx = kernel address, rbx = probe array
2 xor rax, rax                     ; zero target
3 retry:                          
4 mov al, byte [rcx]               ; probe kernel memory
5 shl rax, 0xc                     ; select part of the kernel memory bits
6 jz retry
7 mov rbx, qword [rbx + rax]       ; based on kern. mem., map to memory region
```

Then, the attacker checks all locations in `rbx` in order to check which items are fresh in the cache and which are not. This will demonstrate what kernel address has been accessed. Then, cache is flushed and this is retried.

My main criticism of the paper is that while it is heavy with the doom and the gloom, it doesn't propose what steps CPU vendors should take to improve performance.
