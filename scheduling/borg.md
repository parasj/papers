# Borg, Omega and Kubernetes

* Article details some lessons in cluster scheduling
* Initial motivation for containers was isolation to improve utilization
* Omega removes the single-point-of-failure in the centralized master
* Why use containers? Not just isolation. Containers are an application-oriented environment rather than machine-oriented
* How to communicate state from tasks back to scheduler? Expose HTTP endpoint
* Pods allow for co-scheduling to decouple isolation from resource mangement. A complex application can be broken down into separate isolated containers but be co-scheduled on the same machine with the same set of resources
* Some takeways:
  * Separate container management from network management (hard to manage ports)
  * Give tasks labels, not IDs
  * Don't expose state, instead gate it with a flexible interface
* Configuration and dependency management at scale are hard problems still
