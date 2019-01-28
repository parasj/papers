# The design and implementation of a log-structured file system

**Key idea**: Structure FS entirely as a log instead of a FFS random structure. This batches writes into fast sequential bandwidth. Intelligently clean FS segments to recleaim free segments. Results in 10x higher bandwidth.

## Motivating trends
* Increasing sizes of memory makes caching more viable
* Disk improvements are cost/byte not performance
* FFS speed is limited for small files due to overhead of metadata (5 writes)

## Log-structured FS
* Buffer sequences of file operations in order to max write bandwidth
* Key subtleties: how to read data? and how to free space?

## Reading data off file-system
* Index structures similar to FFS. inodes written to the log.
* In order to randomly access files, there is an inode map that stores pointers to inodes.
  * inode map is written to the log
  * In order to track inode maps, there is an inode map of maps
  * This map of maps is small enough to keep in memory

## Segments
* Segments keep free space bundled so cleaning applies at the segment level
* Segments are fixed size and large. Segments are either full, empty or partially full.
* Segments are chosen to be cleaned with the goal of packing multiple segments into a smaller set
* Segment cleaning performance depends on bimodal distribution of mostly full and mostly empty segments

## Fault-tolerance
* Checkpoints define consistent metadata states (inodes etc) and roll-forward defines inter-checkpoint state
