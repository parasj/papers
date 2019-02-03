## Granularity of locks and degrees of consistency in a shared database

**Top points:** 1) size of critical regions/objects demonstrates tradeoff between concurrency and overhead, 2) introduction of "dynamic" or adjustable lock sizes, 3) consistency can be traded off according to user's needs, 4) these compromises by the user allow DB to unlock more performance.

*1) Tradeoffs between overhead of locks and concurrency, determined by size of locks*: The granularity of locks can unlock more potential concurrency but it also can introduce increased overhad (e.g. if we lock each row, a large query now is more expensive). 

2) *Dynamically variable lock sizes:* Gray et al note the hierarchy within databases and outline a tree-based locking protocol. In order to allow for concurrency, locks are requested and unlocked in a consistent order, root to leaf and visa versa.

3) Gray et al note several degrees of transactions (each layer includes the previous conditions): *Degree 0*: T1 does not overwrite T2's dirty data, *Degree 1:* T1 does not commit before it's done, *Degree 2:* T1 does not read T2's dirty data, *Degree 3:* T2 does not write dirty data for any read by T1 before commit. Gray then outlines various ways to implement each degree of consistency using combinations of long and short read + write locks.

This is overall a good paper but, like most systems papers of the time, it has no discussion about performance implications about the degrees of granularity on a real system. This makes it difficult to determine the magnitute of performance change in these solutions
