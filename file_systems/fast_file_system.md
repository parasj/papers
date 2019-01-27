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
