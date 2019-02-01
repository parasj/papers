# Using Crash Hoare Logic for Certifying the FSCQ File System

**Key Idea**: Verify filesystem in layers starting with a log at the bottom and then each layer above. Crash hoare logic extends hoare logic (precondition, postcondition) with recovery procedures and logical address spaces. This ensures state after repeated crashes anywhere during execution. FSCQ is safe under several assumptions (compiler, hardware, etc).

* FSCQ uses an asynchronous model of disk writes since batching writes is important for good performance.
* seL4 does not have a verified file system and no persistent state.

Chen et al. detail their formal proof of a filesystem that retains integrety under fail-stop conditions. This means that the system can retain consistent data structures under reboots and crashes. It will provide a transactional ability for the filesystem to accomplish this. The authors prove their system using the Coq proof system. They achieve their finaly result with a comparable performance to an educational file system (which I feel is a poor benchmark) and they have a 0.5 slowdown compared to a real Unix filesystem.

They extend Hoare logic with a crash condition that allows the system to prove that the system retains integrity on a crash. This contains the states a system can enter in a crash. These crash conditions are most useful for proving the log. In a crash in the filesystem, the log record is simply rolled back. The proof was drastically simplified by proving the core logging mechanism, upon which safe transactions can be assumed. Then in a crash, one simply states there is an incomplete transaction which upon reboot is rolled back.

This paper was very interesting. I think it is quite a feat the authors went through to implement this system. My main criticism of this work is that I feel they should have extended their proof to potentially consider multithreaded systems, as is more realistic and key to good performance. But this would complicate the proof.
