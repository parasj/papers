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
