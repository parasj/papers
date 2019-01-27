# A Fast File System for UNIX

_Motivation_: Unix filesystem performance was very poor (<2% of overall throughput).

## Key optimizations
* Improve locality of data structures near data blocks
  * Use disk block _groups_ to keep files within consecutive blocks
  * Keep files in a single directory together (with exception for large files)
* Reduce fragmentation of disk blocks by allocating contiguously from the bit vector
* Increase block size to improve performance
  * To mitigate internal fragmentation, FFS uses sub-blocks
  
## Usability enhancements
* Long file names
* Symbolic links
* Renaming files

## Long-form summary
McKusick et al present a series of optimizations to the UNIX file system in as implemented in the BSD fork. They note that only 2% of a disk's peak throughput was achieved with the previous implementation of the file system. However, they determine block sizes are the a key reason for why throughput is low. Thus, they increase the block size from the original 512B to 4KB. Then, they determine that the free list, when full, would distribute blocks across the filesystem thereby slowing reads down by forcing seeks. They replace the free-list with a bitset that allows scanning for sequential blocks. Finally, they identify a way to reduce internal fragmentation with small files by dividing each block up into smaller "fragments" which can be used by small files.

The remainder of the paper then covers other miscellaneous changes to the UNIX filesystem, incuding the advisorial locks, longer file names, symbolic links, faster renaming, and user-based quotas.

Overall, it seems like this paper achieves good results. However, the performance focus of the first section and the functionality focus of the second seem to be somewhat unrelated. Also, it is not mentioned how one should choose the block sizes in the future as disks improve. Finally, it seems like there is a CPU tradeoff to these changes, implying some kind of bottleneck.
