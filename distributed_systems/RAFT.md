# In search of an understandable consensus algorithm

The authors note that the Paxos protocol, while popular and correct, is very difficult to understand. It also is difficult to implement correctly and requires large changes to systems built on top of it. They introduce Raft with the goal of creating a practical consensus algorithm that also is understandable. Raft has three key differences: 1) leadership is stronger than in other protocols, 2) they use randomization to resolve ties in leader election and 3) they describe a joint-consensus protocol.

Instead of a consistent log, the authors describe a system as a distributed state machine. A consistent log is the underlying primitive that enables the state machine. This state machine ensures: a) safety meaning consistency under non-Byzantine faults, b) availability under loss of a minority of the cluster and c) do not require strong clocks.

Raft has three phases: 1) leader election again, 2) log replication and 3) safety property. This separates each of the three functionalities which can be implemented independently. Leader election is based around the concept of terms, after which another election occurs. A heartbeat mechanism allows the followers to begin the process of leader election independently. The candidate leader with a majority vote wins the contest for a term. Randomization resolves the issue of ties in elections. 

My main criticism of this work is that leader election appears to be quite slow. Given longer terms, this may not be an issue. But I can imagine that this system would not perform well in scenarios with high-churn of clients. This would make it less useful for distributed systems like serverless computing or mobile edge devices.
