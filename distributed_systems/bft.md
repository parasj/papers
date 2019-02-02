## The Byzantine Generals Problem

**Key ideas**: BFT = resiliance to a traitor, and without signing, you need 2/3 loyalty. BFT requires 5 nodes at minimum.

Lamport presents a simple problem that is a conceptually simple way to think about fault tolerance in distributed systems. The crux of the paper is a system of generals that communicate with messengers with the goal of reaching a consistent decision among all loyal generals while remaining true to the majority decision.

The first interesting conclusion is that without message verifiability, then there must be at least $\frac{2}{3}$ of the generals that are loyal. Lamport shows that for 3 generals, it is impossible to distiguish between a compromised general or a compromised liutenant. Basically, this means you need at least 5 nodes to ensure a good solution that is resilient to a traitor.

This paper is a good paper but is a little dense. They present an algorithm for BFT that also presumes authenticatable messages.
