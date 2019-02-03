# Readings in Database Systems
## Background
* Why do systems fail?
  * Excessive complexity
  * No compelling use case
* Databases have encountered that one-size-fits-all is no longer true

## Traditinoal RDBMS
* System R => transaction manager and cost-based optimizer
* Postgres => user defined ADT
* As memory and disk gets cheaper, DBMS may go back to no-overwrite storage and time-travel

## Techniques everyone should know
### Query optimization
* System R introduced cost-based optimization (Sellinger)
  * Key subproblems: cost estimation, defining a search space and cost-based search
  * DBMS estimates cardinality (size) of output using heuristics
  * Then DBMS makes a best-effort cost plan

### Concurrency control
* Gray's "Granularity of Locks and Degrees of Consistency in a Shared Data Base"
 * Detailed notes on [paper review](https://github.com/parasj/papers/blob/master/databases/gray_granularity_of_locks.md)
 * Multi-granularity locking
  * Problem: how to perform locking given hierarchical structure of the database
  * Idea: hierarchical locking with exclusive or shared locks
  * Intention locks allow for coordination between clients
 * Degrees of consistency
  * Degree 1 Read Uncommitted: Transaction does not write data until transaction commit
  * Degree 2 Read Comitted: Transaction does not read otehr transaction's dirty data
  * Degree 3 Repeatable Read: Data read does not change during transaction

### Database recovery
* ARIES paper is the standard here
 * No force = does not need to write dirty pages to disk at commit time
 * Steal = DB can flush pages to disk at any time
 * Complicates the design
 * Logging with redo and undo records
 * Recovery occurs through three phases
  * First read log to determine in progress transactions (find transactions that haven't committed yet)
  * Second play log forwards and apply redo records to database 
  * Third play log backwards to undo records that were not committed
  
