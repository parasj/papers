# Basics of file systems

* **Blocks**: FS is divided into fixed size blocks. There is a tradeoff between block size for small files and efficiency. FFS key innovation for performance was to increase the block size.
* **inodes**: inodes are on disk metadata that store pointers to data, folders, etc. Contains permissions, size, block pointers, access times, etc. Often multi-level to allow larger files and larger directories. 
* **Allocation lists**: store free data lists (free-list or bitmap)
* **Superblock**: Meta-information about file-system like number of blocks, etc.

## Interface
* `open` and `close`
* `read` and `write`
* `fsync`
