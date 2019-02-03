# MapReduce: simplified data processing on large clusters

**Key idea**: MapReduce handles failures gracefully as intermediate mapper state is stored on disk. It parallelises trivially and allows for a simple programming abstraction. MapReduce is still liable to master failure. MapReduce attempts to schedule on GFS nodes with data locally. Backup tasks are used to avoid stragglers.

* MapReduce exposes a simple abstraction
  * flatMap: `(key, value)` => one or more `(out_key, out_value)`
    * data is saved on disk grouped by `out_key`
  * reduce: `(key, [value, ...])` => `(key, [value, ...])`
    * Data is shuffled to the reducers
* Fault tolerance for worker failure is simple as the maser works a master as failed and reruns any map tasks for the failed worker, and any relevant reduce workers are restarted as well
* Fault tolerance for the master node is not discussed
* The master tries to schedule map tasks on the same node on a nearby node (e.g. same rack) to the GFS node where the data is stored
* Some nodes may not fail-stop but may instead just be slow. When a MapReduce tasks is nearing completion, MR launches duplicate backup tasks for the remaining in-progress tasks. This can reduce overall latency by up to 44% in some cases.
