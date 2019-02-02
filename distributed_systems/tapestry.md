# Tapestry: A resilient global-scale overlay for service deployment

**Key idea**: Tapestry implements Paxton's routing protocol for `O(log n)` lookups without centralization. Network topology bounds the "stretch" of the network.

* DOLR protocol abstracts routing to objects
* Key difference from Chord is that Tapestry utilizes network delays in order to optimize lookup speed
* Algorithm
  * DOLR operates by routing in orders of digits e.g. `4*** => 42** => 42A* => 42AD`
  * Objects match to nodes by prefixes. Thus DOLR can route by closest prefix in order to get closer to an object.
  * Optimization during lookup is that objects deposit location pointers across the network that accelerate lookups.
    * As routing progresses, if the route intersects the publish path for an object, the route will follow the publish path to the final destination, almost like a Hansel and Gretel breadcrumb trail.
  * Fault tolerance is added though redundant routing paths. Backup links can allow routing around failure.
  
## Review
This paper also covers a DHT. However, I notice the difference in both testing methodology as well as goal for the project. I will keep this summary short and cover key differences. 1) Tapestry uses network distances to minimize total network movement. There is an initialization phase for these routing tables, and a mechanism to keep them live. 2) Tapestry assigns node IDs using a random process, instead of hashing an IP address. 3) Tapestry shares one larger DHT among multiple applications to achieve a sort of economy-of-scale.

Overall, Tapestry appears more complex than Chord. It provides richer functionality but is harder to compose with applications that do not require the additional complexity of features such as DHT multi-tenancy and other features. I think the network-aware optimizations make a lot of sense but I would be curious to see if there was a simpler solution that would involve nodes swapping positions with other nodes until a well-formed ring is completed at the fix-point.
