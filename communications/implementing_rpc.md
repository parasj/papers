# Implementing Remote Procedure Calls

## Why use RPC?
1. *Semantics* Clear and easy to understand semantics
2. *Efficiency* RPC is simple enough to optimize
3. *Generality* Procedure calls are widely used

## Issues with RPC?
* What should be precise semantics?
* How to define interface (stubs)?
* How to handle failures (exceptions in Mesa)?
* How to handle arguments by reference (shared VM? or no)?
* How to handle binding + discovery (Grapevine distributed database)?
* Security concerns? Who can create services?

## Key goals for this project
* Usability to make distributed computing easy
* Handle faults either transparently or visibly (exceptions)

## Fundamental decisions
* No shared virutal memory space (could hurt efficiency and could add complexity to Mesa language)
* Why not message passing? It can have similar key constraints and performance, but procedure call is a fundamental abstraction for writing programs
* Match RPC semantics as closely to local procedure call as possible (this leads to some issues as this design leads to poor performance, and RPC is now managed more explicitly)

## Performance optimizations
* I skimmed most of this but they make significant changes to avoid latency from TCP
* RPC is latency sensitive, not bandwidth sensitive
* They optimize sending single packets for RPC
* They optimize acknowledgements
* They use Grapevine to avoid congestion in the network via broadcasting
