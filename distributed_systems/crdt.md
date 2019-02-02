# CRDTs: Consistency without concurrency control
**Key idea**: If concurrent updates are commutative, then the replicas converge. Thus commutative replicated data type. This is one way around the CAP theorem through eventual consistency as it provides almost strong consistency under AP.

* CRDT provide conflict-free eventual consistency under availability-partition tolerance.
* Simple CRDT:
  * A set - to add, add an item to the set and to delete, add it to a second set
  * Issue is that this datastructure grows without bound, but some people have solved this issue
* CRDT introduces a "treedoc" datastructure that allows storing text using a tree.
  * Operations: insert at position and delete
  * Implemented as a tree there text is stored at the root. Text is added by via a globally unique TID.
  * Ties can be broken by ordering different concurrent editors
  * Delete can be implemented via tombstoning
  * To compact the tree, occasional flattening can occur
    * As flatten is not a commutative operation, if there were any modifications, the flatten command will fail.
 
