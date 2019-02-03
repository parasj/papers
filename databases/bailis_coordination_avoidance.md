## Coordination avoidance in Database Systems

This paper covers "invariant confluence" which can classify an application's consistency needs while preserving safe execution. Using invariants on the DB, the system determines if it is possible to structure updates in a coordination-free manner.

The authors describe a proof for invariant confluence being a necessary property for coordination-free updates. They provide a proof by contradiction. They then discuss proofs for various forms on invariants on a database along with whether they are invariant confluent. Equality and inequality are both common operations that are invariant confluent. I find it interesting how some operations would seem trivial (e.g. coordination is not needed for incrementing when the invariant is a greater-than relation).

This is a well written paper. My main criticism is that invariants have proven difficult for many progrmamers to write. Often, it's not intuitive how to write invariants on a system that are not trivial. The authors acknowledge this point in section 4.3.
