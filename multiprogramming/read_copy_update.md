# Read-Copy Update: using execution history to solve concurrency problems

As CPU execution rates increase relative to latencies, locking becomes relatively more expensive. Due to this, locking should become less common. Decreasing locking also avoids deadlocking.

Asymmetric locking is useful for many workloads as it improves read performance where write performance may be low. RCU makes reads completely lock-free. However, this requires care to avoid synchronization issues. Thus, it basically ensures `Any reading thread that starts its access after an update completes is guarenteed to see the new data`. This condition may mean some processes see stale data but this is acceptable for many use-cases like networking.

The high level idea is to copy the data structure and modify another copy of the data structure. When all readers leave the old copy, the old item can be garbage collected. The proposed algorithm is simpler than garbage collection based algorithms and is more efficient.
