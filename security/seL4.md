## seL4: Formal Verification of an OS Kernel

L4 is a high-performance microkernel and this paper attempts to prove certain properties about the system formally. Microkernels are small simple OS's that minimize the amount of priviledged code that runs. seL4 is small enough that it is possible to formally verify it's correctness. They assume that the compiler, assembly codes, boot sequence, cache managment and the hardware.

The authors implement the OS first in Haskell to prototype proofs and refine the spec. Then, they implemented it in C and then used the spec to verify their C implementation. This enables high performance while ensuring correctness. Some parts of the verification steps seem to be manual. But it seems to ensure confidence that correctness is preserved.

In order to verify seL4, the authors focused on a subset of C99. This allowed them to restrict the scope of what they needed to verify. Some constructs like `goto` make verification very difficult and are therefore removed. In order to provide some assurances about the hardware, the authors abstracted the machine interface to a short set of functions (e.g. `invalidateTLB`).

This paper is an interesting work. I think it's approach is more interesting than the final artifact (seL4). The guidelines for formally verifying a realtime and complex system could be applied to other systems like RTOS. For these systems, formal verification could be a big boon. My main criticism of the work is that the paper didn't adequately describe what correctness guarantees it attempted to provide. It seems like there were only ~80 invariants specified.
