# Chord: A scalable peer-to-peer lookup protocol for internet applications

**Key idea**: Chord is a DHT w/o centralization. It distributes the directory service so that key to host lookups occur without centralization. Chord does not take advantage of internet topology. It's key approach is A) consistent hashing, B) stabilization to add a new node to the ring with bounded key movement and C) use of fingers to speed up retrival. Each node stores `O(log n)` pointers and thereby resolve lookups in `O(log n)`.

* Chord can have poor performance under adversarial hash function distributions, thereby leading to hot-spots in the cluster
* Chord utilizes a stabilization protocol to ensure that successor node lists are complete
  * Step 1: node finds location in list where it belongs (lookup)
  * Step 2: new node points to desired successor
  * Step 3: new node copies relevant keys less than sucessor's position in the ring
  * Step 4: predecessor points to new node eventually
* Fault tolerance is achieved by a) storing multiple sucessors and b) replicating data as it is added to the ring

## Comparision to Tapestry
* Tapestry is topology aware which can accelerate lookups.
* Chord is a simpler protocol with simpler addition/removal of nodes.
* Both have `O(log n)` lookup costs.

## Review

This paper details a low-overhead DHT (distributed hash table) that has a $O(\log{N})$ storage requirement and messages lookup requirement in a stead state. This information requirement is also best-case to bound the amount of lookups needed to answer a DHT query. If there are less than $O(\log{N})$ pointers , then messages will still route (as long as any node can talk to another node. The algorithm has a nice correctness proof which demonstrates its efficacy. I find it interesting that Chord cites Tapestry (next paper) and then claims that it is much simpler.

Chord solves four problems: 1) load balancing, 2) decentralization, 3) scalability, 4) availability and 5) flexible mapping. Consistent hashing acts as the backbone for this algorithm (I will not cover as I am familiar with it). But it mitigates the need to maintain an index of all other nodes by keeping pointers to nodes approximately at the multiples of 2 around the hash ring.

My main criticism for this paper is that it makes various assuptions about the network. For the peer-to-peer file sharing use case that motivated many early works in DHT, links can be across several orders of magnitude of bandwidth. And network links are highly asymmetric between upload and download bandwidth. The paper also farily acknowledges that the proofs depend on uniform randomness of hashes. But clients near each other may be on the same subnet, etc., so hashing IP addresses may not be sufficient to ensure that machine identifiers are sufficiently uniformly distributed.
