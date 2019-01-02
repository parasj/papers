# Working Sets Past and Present
Key points
* Denning introduces the concept of a working set, the memory that needs to be resident for a process to operate with minimal page faults.
* Why is cache eviction hard? We don't know the next arriving read. So we have to guess.
  * Two types of locality, temporal locality and spatial locality
  * Also phase-transition models where processes switch between distinct phases of small and large working sets
  * WS takes advantage of temporal locality
* For each process, we keep track of virtual time (ordered by memory access count)
* Then W(t, ω) is the set of pages accessed in the last ω memory accesses => this is the working set
* Thus, working set policy attempts to keep W(t, ω) in memory 
* It is hard to calculate W(t, ω) and is fairly expensive. But it performs very well for a non-lookahead memory policy.
* Key heuristic: L = S heuristic says to increase multi-programming rate until mean page-replacement time is equal to mean-time between page-faults