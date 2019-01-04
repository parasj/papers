# ARC: A self-tuning, low overhead replacement cache

Key idea: ARC is cache that balances between frequency and recency. These two properties are slowly adjusted automatically during execution (adding points between recent cache and frequent cache).

Key points:
* Caching only makes sense for a resource that is significantly faster yet significantly more expensive. If it's cheap, why not use lots of it? If it is not 10x faster, then the cache has limited benefit. The cache also need not store a large portion of the underlying data to get good speedups due to frequency effects.
* ARC has high hit ratio while maintaining simple implementation
* ARC is composed of recent cache (pages only read once) and frequent cache (pages read more than once). Based on the recent history of cache reads, it adjusts the relative sizes of these two caches.
* One model of virtual memory is that applications cycle between phases of high IO and low IO. Adaptive systems are useful generally.

Notes:
* Background
  * LRU alone doesn't work well - it depends on queries that are "recent" based on a stack model of computation and lookup
  * LFU is optimal but is expensive to implement and does not adapt to changing workload.
  * LRU-2 approximates LFU but has tunable parameters (general theme in systems?)
* Approach
  * Key ideas:
    * Promote items from recent to frequent when read twice
    * If recent is full, then replace from recent. Else, replace from frequent.
    * Store values for the top values of each of RECENT and FREQUENT. Number of elements is controlled by `p`.
    * Store keys for recently evicted items in a "ghost list".
  * Cache replacement policy
    * When reading, if there is a hit on any item in RECENT_TOP or FREQUENT_TOP, move item to most recent position in FREQUENT_TOP.
    * If there is a miss and key is in RECENT_GHOST, then put the value in RECENT_TOP. Also increment `p`.
    * If there is a miss and key is in FREQUENT_GHOST, then put the value in FREQUENT_TOP Also decrement `p`.
    * Else, put it in the RECENT_TOP
  * Adapting `p`
    * When pages get moved, adjust `p` by some number of points up or down. Number of points for tuning is a hyperparameter.