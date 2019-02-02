# Experience with Grapevine: The growth of a distributed system

* Grapevine was an internal email-like service
* Key components
  * Registration database (a la DNS) which provide nameserver lookups
  * Message servers which queue messages with duplicate elimination
  * Inbox which can be replicated
* Lessons
  * How to tradeoff consistency with scalability by resolving conflicting data
  * Use application to resolve inconsistency (like Dynamo!)
