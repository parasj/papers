# Lightweight Remote Procedure Call

This paper isn't quite a "RPC" as per the traditional context. It's closer to a local procedure call made efficient. Through a profiling-based approach, they identified that most RPC in distributed operating systems was 1) local and 2) small size. They optimized this common happy case to increase performance. This whole paper is an application of the end to end argument in a way.

## Why lightweight (local) RPC

Many RPC calls are on the same machine and RPC presents a convenient semantic abstration for procedure calls. The paper notes that crossing-domains and crossing-machines both utilize RPC before the paper and while the semantics are similar, single machine can be optimized.

Monolithic operating systems are more efficient but are sometimes insecure and brittle. Changes can affect a wide range of other functionality. Instead, operating systems can be broken into smaller protection domains (capability systems or microkernels) but then communcation costs can be expensive.

## What does LRPC do?
1. *Simplify control transfer* as the client thread is run directly in the target's protection domain
2. *Simplify data transfer* as data ps passed through a shared argument stack instead of copied
3. *Simple stubs* as syibs are optimized in assembly for common cases
4. *Caching domains on multiprocessors* as idle cores can be used to cache top protection domains

## LRPC implementation
1. Client calls procedure = kernel trap
    - Argument stack is writable by both client and server
2. Kernel validates caller
3. Binds to server
    - Writes arguments to shared argument stack
4. Dispatches client code in server domain (client runs in server's address space with a shared argument stack)

## Performances
3x faster for uniprocessor and on multiprocessors
Remaining performance gap comes from:
  * flushing TLB
  * bringing page table back into memory
