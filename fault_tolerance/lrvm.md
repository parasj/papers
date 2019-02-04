# Lightweight Recoverable Virtual Memory

**Key idea**: E2E argument, what is the simplest way to add recoverable memory (transactions) to an application? Link LRVM with application and it will maintain a per-application log on disk for recovery. This provides better performance and captures the most important subset of the goals of Camelot.

* Technique:
  * Store segments on disk where applications can mirror in memory.
  * Applications explicitly map segments into memory and edit them, then commit.
  * API makes LRVM's job simple as users explicitly set transaction regions.
  * Logs are occasionally truncated to save space.
  * Logs are no-undo redo as uncommitted changes are not written to external data segments. This assumes that old values can be kept in memory comfortably.

This paper ultimately presents an efficient implementation of the idea that most applications just need redo-only recoverability mechanics without the heft of a full DBMS recovery system. These RVM transactions are low-overhead and are conceptually simple. As LRVM can be linked in userspace, it remains fast even while it doesn't rely on OS support.

Camelot was an older crash recovery scheme in the Mach microkernel. However,when developing Coda, the authors found it to be overkill. RVM is a useful abstraction that simplified implementation, but Camelot was high overead and difficult to maintain (sounds a bit like gradware...). So they wanted to integrate similar RVM concepts while preserving simplicity over generality (meaning less features w/r to parallelism, media failure, etc). It uses simple Unix primatives makign it portable. And it is a userland library which allows each library to manage their own state, which is overall more efficient. LRVM maps segments into the process's VM. Users explicitly call `set_range` which lets LRVM know what was modified. The paper doesn't store undos because it always writes to the log first.

I like this paper. It takes a good idea and makes a fast implementation of it. And as is classic in systems papers, it demonstrates the idea using real-world testing. In the end, it got the fault-tolerence the application desired with better performance than Camelot. I'm not sure how much impact it has seen in the DB world but I see interesting applications for LRVM in distributed computing.
