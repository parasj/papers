# Unikernels: library operating systems for the cloud

## Key ideas
* Instead of OS on top of VMM, use simple library kernel that get's optimized into a application specific binary
* Dead code elimination so code size is smaller and simpler
* Strongly typed library OS leads to fewer bugs and increased security
* Faster overall since system calls become procedure calls over the VMM abstraction
* Result: faster OS with less code and 50ms boot times
