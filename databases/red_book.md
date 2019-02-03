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
* Gray's multi-granularity locking paper
* Issue is 
