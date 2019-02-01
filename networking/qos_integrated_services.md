# RFC 1633 - Integrated Services

## What problem does this paper address?
 Branden et al. propose a mechanism for QoS on the internet. The specific problem emerging is that voice, video and music applications require fine guarantees on latency. Latencies are not controlled on the internet today due to queueing delays and congestion losses. Traffic management is another concern addressed by the paper as bandwidth may need to be shared among multiple classes of traffic. Some applications require a minimum bandwidth under load.

## Do you believe the problem is/was important? Explain.
 QoS appears useful to enable interactive applications. However, QoS has not been as successful as must have been anticipated. This paper proposes a particularly intensive approach to the problem of QoS that would require modification throughout the internet. And ultimately, voice and video applications appear to have adapted to best-effort delivery. These applications already tolerate packet loss.

I think this application is actually useful for a different application -- robotics require low latency control over the internet and guaranteed service is something that could be safety critical. For example, a surgeon could use the internet to control a DaVinci robot reliably if latency was controlled tightly.

## What is the authors' main insight?
 Integrated services proposes admission control and reservations for the internet. Four specific components: packet scheduler (FIFO), admission control, classifier and reservation setup control (RSVP). Reservations are defined with flowspec and RSVP is a protocol to reserve the actual resources. These components provide guaranteed service.

## Do you think the solution is a good one? Explain.
 Applications seem to have adapted to best-effort delivery. Voice and video application in particular are not actually too sensitive to interruption in service. I think it is always better to introduce bounds on systems, and there are likely customers who would pay for such guaranteed service (e.g. autonomous vehicles). But this solution requires very drastic modifications to the internet. Much of the variability in latency comes from the last mile of the network, not the backbone. So a more incremental solution could be deployed at the edge of the network, not the core.

## Did you enjoy reading this paper?
 This paper was clearly written and easy to read. But it was very long (understandable for a RFC).
