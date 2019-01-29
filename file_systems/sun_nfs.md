# The Sun Network File System: Design, Implementatino and Experience

NFS is a simple stateless protocol for a distributed filesystem. Key design goals are (1) portability, (2) crash recovery (stateless), and (3) transparent access. Secondary goals are performance and UNIX semantics. NFS is implemented with the VFS and vnode interfaces added to UNIX.

## NFS API
The key call is:
`read(fh, offset, count)` and `write(fh, offset, count, data)`. The file handle is per server so no state is stored. If the server goes down, the client can retry writes.

**Consistency**: As UNIX provides no transactions or atomicity outside a single operation, consistency is easy to maintain. The server commits any modifications to stable storage immediately.

**Pathname lookups**: Pathname traversal must be done recursively per directory as there could be other mountpoints.

**Authentication**: Standard UNIX permissions are used for authentication. Therefore, all servers and clients must have shared uid space.

**Locking**: No locking support due to lack of file locking protocol consensus.

**Performance optimizations**: read-ahead and write-behind buffers on both the client and the server. Client-side metadata caching for file attributes and directory names.
