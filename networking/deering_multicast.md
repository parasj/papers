# Multicast Routing in Internetworks and Extended LANs
## What problem does this paper address?
Multicast is prevalent in LAN networks but not in the internet. Multicast is more efficient and lower latency while also adapting to unknown or changing topology.  However challenges with latency and delivery probability make multicast somewhat harder than LAN.

## Do you believe the problem is/was important? Explain.
This problem is important for video streaming. AT&T has built a large business on multicasted video. After reading the second paper (comments included in other review), I feel that this functionality can be done as an overlay and not in the IP level. But unlike QoS, multicast seems like a very useful network primitive.

## What is the authors' main insight?
The authors demonstrate that a basic algorithm using bridges can be optimized with distance-vector routing and some additional iterative optimizations to integrate multicast into internetworks. This reminds me of many papers in systems where a simple algorithmic tweak can be composed with older approaches to make a new solution (like WSClock).

## Do you think the solution is a good one? Explain.
I like this solution as it starts from a simple solution and address key issues with algorithmic insights to improve the algorithm. But some of these calculations seem complex. This goes against E2E arguments.
