# Distributed Snapshots: Determining Global States of Distributed Systems
**Key idea**:
* A process will initiate snapshotting and save it's own state. Then it sends a snapshot request message to all other nodes. Other nodes will snapshot their current state and then send a snapshot message to all links other than the one where the message came from. If a node already snapshotted it's state and recieves a message without the snapshot request, then it saves the message as an in-flight message that was queued before the snapshot was initiated.
