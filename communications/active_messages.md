# Active messages: a Mechanism for Integrated Communication and Computation

The paper discussed how to improve network and computation utilization by modeling the network as a pipeline. Messagers include a pointer to code that is shared on all machines. Messages are sent ASAP with minimal buffering and servers execute code as soon as they recieve a message. This asynchonously frees up the client to continue computing without the overhead of buffering along the network stack. 
