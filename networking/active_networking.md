# Towards an Active Networking Architecture

## What problem does this paper address?
 This problem notes a changing "pull" -- more programmability is appearing in the middle of the network (firewalls, proxies, etc). Given these trends, the paper describes a radical position of capsules, packets with programs, in order to enable new applications.

## Do you believe the problem is/was important? Explain.
 This problem is important given the rise of middleboxes. But I disagree with its extreme position; I think the network should not be able to run arbitrary programs nor do I think that packets should be able to route themselves. A more moderate view that I agree with is closer to RFC 1633.

But we see active networks emerging today (e.g. programmable switches) so this problem has remained relevant.

This whole paper goes against the end to end argument; much of the functionality implemented in the network would likely need to be implemented at the endpoints (eg firewalls) and also adds significant complexity for the common cases today.

## What is the authors' main insight?
 The authors note that secure execution of programs is easier than ever ("push") so they propose capsule programs to run on an active network. They also propose an Active Storage mechanism that seems promising. They advocate for a Java-like ISA.

## Do you think the solution is a good one? Explain.
 I think the ideas are interesting but while the authors make no claims to security in this work, I believe this is a critical issue when running code on network infrastructure. Active Networks have a place in datacenters and intranets, but I do the core internet should not have any active components.

## Any other comments/thoughts?
 Follow-on works cite significant slowdowns. And the impact of active networks may be even greater as many network functions are offloaded onto ASICs. It takes a radical stance on how a network should be architected and seems like it was a fun paper.

## Did you enjoy reading this paper?
 Yes-- I enjoyed this paper
