# Communications and RPC

## Why use stubs for RPC?
Stubs enable consistency of semantics. Calls look just like local calls for both the server and the client. Clients and servers could use different formats (little or big endian) for example. Stubs convert arguments to standard serialized wire formats to ensure consistency. This also systems to communicate across multiple languages. Protobuf is an example of a serialization/deserialization format across languages.

## Latency vs bandwidth for RPC; RPC needs low latency
Low latency is critical for good RPC performance. Projects like Active Messages and Cedar (PARC) demonstrate attention paid to optimizing latency for small messages. These needs sometimes bypass conventional networking stack.

## Interleaved execution with communication is critical for good performance
Active Messages strived to interleave execution with communication. This disguises the latency of the network. In order to enable the processor to remain utilized, interleaving is important.

## Security tradeoffs with performance
Many RPC libraries make security tradeoffs to improve performance. For example, sandboxing enables sharing address spaces but at a security penalty (no ASLR). Another example is LRPC where clients execute code directly in the server's domain.
