# Bigtable: a Distributed storage sysetm for structured data

Big table stores data as a sparse table indexed by string rows and columns. It can store byte data. This allows it to be used by many applications (perhaps suboptimally).

Data is sorted by row key. Data is partitioned across rows. They reverse domain names to exploit this design so pages on the same website are stored together. Data is timestamped but no mention is made to how this is made consistent.

My main criticism of this work is that the data model seems quite unoptimized for many workloads other than storage, search engine indexing, etc. for example, it just stores string row and col names wiht byte data which precludes it from doing any form of query optimization. So this seems like a good solution for binary data stores but not for many other workloads. It seems optimized to the web page storage problem.
