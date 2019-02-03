# Containers overview

* Containers provide lightweight resource management separately from strict isolation.
* Effectively is like fine-grain access controls on resources vs virtualization
* Mechanisms of namespacing and cgroups
  * cgroups limit and prioritize CPU, memory, block I/O, network etc
  * namespaces isolate process trees, networking, user IDs, mounts
* Shared kernel with host which reduces RAM needs
  * System container and per-application containers
* Low overhead as processes are isolated but run directly on the host which is close to native performance
* KVM overheads are closing in on docker and and can beat docker in networking
