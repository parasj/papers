# Efficient software-based fault isolation

**Key idea**: The paper implements fault-isolation for distrusting applications in a single address space. Address space is segmented into multiple domains with the upper-most bits. Most writes and control flow can be statically verified, and jumps can be checked with a few instructions.

## Motivation
Microkernels motivate OS that is pluggable. But security concerns with multiple protection domains leads to high cost (trap into OS, TLB flush, register save/reload, and trap back into user-space). 

## Sandboxing
Modify object code to prevent writes or jumps outside fault domain. Increases execution time for reduced RPC cost. Most writes and pc-relative jumps are verifiable statically. Otherwise, the compiler or a binary patcher modifies source in order to check jump instructions (either with a precise fault on mismatch or by casting upper bits into the fault domain).

## Performance
Improves RPC to ~1μs with a 4% slowdown on average.
