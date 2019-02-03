## Spark: cluster computing with working sets

**Key idea**: Spark represents computation functionally where Scala code represents transformations on RDDs (Resillient Distributed Data). Lineage tracing allows for fault-tolerance while caching (key insight) allows for faster performance. 

Spark is a library for in-memory data analysis that relies on storing data lineage instead of the data itself. Data is then lazily materialized for a specific query. This allows data to be cached if desired but recreated if cluster memory pressure is high. The system appears to be heavily influenced by DryadLINQ.

Spark defines a narrow set of functional operators and then embeds them into the Scala programming language. This provides a terse way to express common data processing tasks. All datasets are partitioned by default which allows data-parallel computation to occur. The key speedups appear to occur from the fact that data can be cached in memory. This prevents the need for data to be fetched from disk repeatedly. 

This paper is a good paper and presents a practical system that combines a reasonable insight (caching data in memory) with a programmer interface that satisfies many needs for application builders that are poorly served by map reduce but may not need a full database. My main criticism of this paper is that it appears to focus on interactive workloads where the tool seems most practical for batch workloads. Moreover, I think that it lacks an estimate of common working sets for top data science workloads.
