# Paxos made simple

**Key idea**: Two phase commit has issues with failure (system can lock up). Paxos is a three-phase commit protocol with unique proposal numbers to break ties. It is not directly Byzantine fault-tolerant.

* Algorithm:
  * Phase 1, prepare
    * Proposer selects a unique sequence number `n` and sends a prepare message to a majority of acceptors
    * If an acceptor recieves a request with `n` greater than any other request, it promises not to accept anything with a sequence number less than `n`
    * Acceptor replies with value it has last accepted
  * Phase 2, accept
    * If the proposer recieves a response from a majority of acceptors, then it sends a commit response to each acceptor
    * The proposer commits the value of the highest sequence number it recieved back from proposers (may not be its own value)
    * Acceptors will accept proposal `n` unless it has responded to a prepare request for a value greater than `n` already.
* Honestly this paper is not super simple still and took some noodling to understand. This blog is a great resource to understand it http://harry.me/blog/2014/12/27/neat-algorithms-paxos
