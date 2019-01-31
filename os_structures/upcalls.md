# The structuring of systems using upcalls

**Key idea**: Asynchronous communication comes from a too-strict depends-upon layering principle. By allowing synchronous calls between layers, performance is greatly enhanced. This paper is similar in idea to Active Messages

* Most systems don't allow upward calls
* Networking is a classic example where this hurts performance -- asnychonous communication leads to significant latency overhead
* Instead, allow kernel to make synchronous call into client
* Key wins:
  * Efficiency
  * Simplicity (procedure call simpler than ring buffers)
  * Procedure call interface is easier to understand for programmers
  * Reduces temptation to make systemwide fixed formats for messages
* Applications to networking and IO (and later on, multiprogramming scheduling in Scheduler Activations
