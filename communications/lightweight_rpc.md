# Lightweight Remote Procedure Call

This paper isn't quite a "RPC" as per the traditional context. It's closer to a local procedure call made efficient. Through a profiling-based approach, they identified that most RPC in distributed operating systems was 1) local and 2) small size. They optimized this common happy case to increase performance.

## Why lightweight (local) RPC

Many RPC calls are on the same machine and RPC presents a convenient semantic abstration for procedure calls. The paper notes that crossing-domains and crossing-machines both utilize RPC before the paper and while the semantics are similar, single machine can be optimized.

Monolithic operating systems are more efficient but are sometimes insecure and brittle. Changes can affect a wide range of other functionality. Instead, operating systems can be broken into smaller protection domains (capability systems or microkernels) but then communcation costs can be expensive.

## LRPC implementation
