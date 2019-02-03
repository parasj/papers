# Live Migration of Virtual Machines

**Key idea**: We want to migrate VMs for load balancing and maintenence. Three ways to migrate: push (pre-copy), pull (residual dependencies) and stop-and-copy (downtime). By applying successive rounds of pre-copy with increasing bandwidth, then a short stop-and-copy, VM downtime is minimal.

This paper continues on the author's previous work on Xen, to investigate a *pre-copy* approach to VM migration. VM migration is a useful abstraction for cluster operators, and I buy their motivation for the problem of scheduled downtime and load balancing. Their approach migrates memory (including serialized CPU state).

There are 3 key concerns:
* First minimizing downtime, which they do by copying pages from the source machine to the target machine while the source continues to run. Then they have a short stop-and-copy phase to copy dirty pages.
* Second, is translation of network requests. They issue an ARP request to notify the network switch that the machine has changed on the L2 while also saving TCP state in memory.
* Third, they measure the impact of migration on server workloads (SPEC) so that they can assess the issue of detecting when to stop-and-copy.

I enjoyed this paper and it has a simple solution to VM migration. My main criticism of the work is that I am unsure if I buy the Writable Working Set Size analysis. It's not clear how to apply it to real workloads like a web server. And I can construct pathological applications that would delay stop-and-copy as much as possible.
