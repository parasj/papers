## Database Cracking

The core problem that this paper is trying to solve is the issue of performance optimization for DBMS. It seems that DB administrators need to tune many parameters in order to achieve good performance. Instead, this paper reorganizes the database according to query loads.

As each query comes in, the indexes are sorted at query time. Whenever a query touches some data, it reogranizes that data in the form of a crack index. This allows future queries to take advantage of the sorted index. An example is a where query which will automatically split the data in to multiple pieces. 

I didn't really like this paper to be honest. It seems very complex and these ideas sound reminent of the same issues Spark encountered with working sets and caching.
