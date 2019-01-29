# Caching in the Sprite Network File System
Sprite is a network OS that caches data in-memory across many machines. It's cache consistency protocol enables sequential writes (write then write) consistently. It also has a simple mechasism to balance FS cache with VM cache by attempting to match the oldest items in each.

## Concurrent write sharing
If a file is open by multiple parties, then all caching (read and writes) is disabled. The server notifies all parties that caching is disabled and flush dirty pages.

## Sequential write sharing
If there is only one writer, then each client can cache data. Version numbers for files are checked upon opening a file. Dirty blocks are also copied over from the last writer lazily upon read by another client (unless a repeating 30s write flushing period has passed).

## Balancing page cache with VM allocation
When there is a page fault, each LRU cache compares the oldest entry. The one with an older entry is made to evict an item.
