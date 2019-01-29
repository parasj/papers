# A case for redundant arrays of inexpensive disks (RAID)
**Key idea**: Increase I/O performance and reliability by partitioning data across multiple disks with extra error correction codes (parity bits).

## Motivation
* I/O improvements is slower than CPU speedups
  * "Each CPU instruction requires one byte of main memory"
  * Amdahl's law states that IO is a growing bottleneck
* Commodity disks have similar performance to enterprise equipment, but much cheaper!
  * Commodity IOPS per actuator is similar (within 2x) of enterprise drives

## RAID levels
* RAID 0 = striping
* RAID 1 = mirroring
* RAID 2 = hamming codes for ECC
* RAID 3 = single check disk per group
* RAID 4 = isolate reads and writes
* RAID 5 = rotate check disk per block
