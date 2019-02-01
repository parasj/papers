# A Case for End-System Multicast

## What problem does this paper address?
 IP multicast is complex and violates basic design principles for the internet (E2E, stateless routers). A long-held assumption in multicast design is that performance wins would make low-level multicast a good design choice. This paper revisits that assumption and shows a 2x cost for high-level multicast.

## Do you believe the problem is/was important? Explain.
 Yes. This paper makes a convincing case that internet multicast can be scalably implemented as an overlay instead of at a low-level. Multicast is a very useful protocol for video broadcasting. The problem of complexity due to multicasting seems clear to me after reading Deering's paper. It seems that internet architects strived for simple and scalable designs which unicasted datagrams have served well. So it makes sense to rely on that principle for new designs.

## What is the authors' main insight?
 Very interesting method -- the authors use probabilistic algorithms to construct connected "meshes" and then calculate spanning trees in a somewhat decentralized fashion. I had to sketch out some diagrams of their protocol but it seems simple enough (at least simpler than Deering's paper) and provides robust multicasting.

## Do you think the solution is a good one? Explain.
 This solution still has a bootstrapping issue where the system has to know a set of servers to begin communicating with. Multicast can be used in situations where a party may not know the set of servers they would like to communicate with. This functionality is still missing.

Overall, this solution is a good one in the sense that it challenges a long-held belief regarding implementing multicast at a low vs high level. And the solution seems like it might be necessary for compatibility over internetworks with older unicast-only routers.

## Any other comments/thoughts?
 I would like to have seen if there were any bounds, if any, that could be placed on the algorithm e.g. time to integrate into mesh, maximum communication overhead, etc.

## Did you enjoy reading this paper?
 Yes. The paper reminded me a bit of Chord in that it is an overlay with some probabilistic algorithmic ideas.
