# Delay Scheduling: A Simple Technique for Achieving Locality and Fairness in Cluster Scheduling

**Key idea**: Authors note conflict in fairness and locality. Their technique relaxes fairness in order to improve locality. When a node wants to schedule a new task, it can skip the head-of-list task in favor of another task that has locality. But if a job has been delayed for enough time, it will be launched non-locally to avoid starvation.
