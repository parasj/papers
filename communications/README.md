# Communications and RPC

## Why use stubs for RPC?
Stubs enable consistency of semantics. Calls look just like local calls for both the server and the client. Clients and servers could use different formats (little or big endian) for example. Stubs convert arguments to standard serialized wire formats to ensure consistency. This also systems to communicate across multiple languages. Protobuf is an example of a serialization/deserialization format across languages.

## Latency vs bandwidth for RPC; RPC needs low latency
Low latency is critical for good RPC performance. Projects like Active Messages and Cedar (PARC) demonstrate attention paid to optimizing latency for small messages. These needs sometimes bypass conventional networking stack.
