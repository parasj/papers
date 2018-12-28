# System R & DBMS

Links:
* Brewer's notes: https://people.eecs.berkeley.edu/~brewer/cs262/systemr.html
* Ion's slides: https://ucbrise.github.io/cs262a-spring2018/notes/02-SystemR.pdf

* Databases designed to make business applications easier to write (like CRM, HR applications, ERP, SCM)
* Three phases of DBMS:
  * 60's Hierarchical (IMS) and network (CODASYL) DBMSes were low-level where users wrote algorithms directly
  * 70's Codd wrote his paper on set-theory for DBMS with **data independence**. 
    * Data independence useful where environments change faster than applications
* Key design points for DBMS
  * Modules
    * parser
    * query rewrite
    * optimizer
    * query executor
    * access methods
    * buffer manager
    * lock manager
    * log/recovery manager
  * Disk management
    * 1 file per relation
    * 1 big binary file
    * raw device access
  * Process management
    * process per user
    * single server w/ thread pool
    * multi server
  * Hardware model
    * shared nothing (only networked)
    * shared memory
    * shared disk (e.g. SAN or NAS)
  * Fault-tolerance
    * Shadow pages versus write-ahead logging
* Learnings from System R
  * Throw out V1 of a system. V1 often addresses complexity, V2 should aim for simplicity
  * Expose as many internals of a system through standardized inferfaces
  * Optimize the fast path
  * Interpretation vs compilation vs IR
  * Consider component failures
* System R key design goals
  * Ease of use
  * Unified abstraction (between batch and ad-hoc)
  * Support updates to underlying DBMS
  * Concurrency between multiple users
  * Fault-tolerance
  * Access control
  * Performance