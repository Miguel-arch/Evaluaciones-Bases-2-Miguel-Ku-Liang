> Bases de Datos 2, Resumen 5 y 6  
> Miguel Ku Liang - 2019061913

## Introduction

Google's Spanner started as a key-value store offering multi-row trnsactions, external consistency and transparent failover across datacenters. It has evolved into a relational database system. The desire to make it behave like a traditional databse has forced the system to evolve:
* The architecture of the storage stack has driven fundamental changes in our query compilation and execution
* The demands of the query processor have driven fundamental changes in the way we store and manage data

Spanner is used as an OLTP database management system for structured data at Google and is available in beta as Cloud Spanner on the Google Cloud Platform. 

The Spanner query processor implements a dialect of SQL called **Standard SQL**. It is based on standard ANSI SQL, fully using standard features like ARRAY and row type called STRUCT to support nested data as a first class citizen. 

Spanner's query processor is built to serve a mix of transactional and analytical workloads and to support low-latency and long-running queries.

## Background

Spanner is a sharded, geo-replicated relational database system. Spanner's transactions use a replicated write-ahead redo log, and the Paxos consensus algorithm is used to get replicas to agree on the contents of each log entry. Each shard of the database is assigned exactly one Paxos group. A group may be assigned multiple shards. All transactions that involve data in a group write to a logical Paxos write-ahead log. Paxos can make progress as long as a majority of replicas are up, achieving high availability despite failures.

Concurrency control uses a combination of pessimistic locking and timestamps. For blind write and read-modify-write transactions, strict two-phase locking ensures serializability within a given Paxos group, while two-phase commits ensure serializability across the database. 

Spanner provides a special RPC framework called the **coprocessor framework**, to hide the complexity of locating data. Read and write requests are addressed to a key or key range, not to a particular server. The coprocessor framework determines which Paxos group owns the data being addressed and finds the nearest replica of that group that is sufficiently up-to-date for the specified concurrency mode. 

A replica stores data in an append-only distributed filesystem called **Colossus**. The storage is based on log-structured merge trees which support high write throughput and fit well with the append-only nature of the filesystem. The original file format was a sorted map called **SSTables**.

## Query Distribution

### Distributed query compilation

The Spanner SQL query compiler uses the traditional approach of building a relational algebra operator tree and optimizing it using equivalent rewrites. Query distribution is represented using operators in the query algebra tree. One distribution operator is **Distributed Union**. It is used to ship a subquery to each shard of the underlying persistent or temporary data and to concatenate the results. Distributed Union is a fundamental operation in Spanner, because the sharding of a table may change during query execution and after a query restart.

### Distributed Execution

Distributed Union minimizes latency by using the Spanner coprocessor framework to route a subquery request addressed to a shard to one of the nearest replicas that can serve the request. Shard pruning is used to avoid querying irrelevant shards. Shard pruning leverages the range keys of the shards and depends on pushing down conditions on sharding keys of tables to the underlying scans.

### Distributed joins

The **batched apply join**'s primary use case is to join a secondary index and its independently distributed base table. It is also used for executing Inner/Left/Semi-joins with predicates involving the keys of the remote table. Spanner implements a Distributed Apply operator by extending Distributed Union and implementing Apply style join in a batched manner.

Distributed Apply allows Spanner to minimize the number of cross-machine calls for key-based joins and parallelize the execution. It allows turning full table scans into a series of minimal range scans.

Distributed Apply can execute its subquery in parallel on multiple shards. On each shard, seek range extraction takes care of scanning a minimal amount of data from the shard to answer the query.

### Query distribution APIs

Spanner exposes two kinds of APIs for issuing queries and consuming results. The **single-consumer API** is used when a single client process consumes the results of a query. The **parallel-consumer API** is used for consuming query results in parallel from multiple processes running on multiple machines. This API is designed for data processing pipelines and map-reduce type systems that use multiple machines to join Spanner data with data from other systems or to perform data transformation outside of Spanner.

## Query Range Extraction

### Problem statement

Query range extraction refers to the process of analyzing a query and determining what portions of tables are referenced by the query. Spanner employs several flavors of range extraction:
* Distribution range extraction: knowing what table shards are referenced by the query is essential for routing the query to the servers hosting those shards
* Seek range extraction: once the query arrives at a Spanner server, we figure out what fragments of the relevant shard to read from the underlying storage stack.
* Lock range extraction: the extracted key ranges determine what fragments of the table are to be locked or checked for potential pending modifications.

### Compile-time rewriting

The implementation of range extraction in Spanner relies on two main techniques. At compile time, we normalize and rewrite a filtered scan expression into a tree of correlated self-joins that extract the ranges for successive key columns. At runtime, we use a special data structure called a **filter tree** for both computing the ranges via bottom-up interval arithmetic and for efficient evaluation of post-filtering conditions. 

Compile-time rewriting performs a number of expression normalization steps:
* NOT is pushed to the leaf predicates. This transformation is linear in the size of the expression.
* the leaves of the predicate tree that reference key columns are normalized by isolating the key reference.
* small integer intervals are discretized.
* complex conditions that contain subqueries or expensive library functions are eliminated for the purposes of range extraction.

### Filter tree

The filter tree is a runtime data structure that is simultaneously used for extracting the key ranges via bottom-up intersection or union of intervals, and for post-filtering the rows emitted by the correlated self-joins. The tree memoizes the results of predicates whose values have not changed and prunes the interval computation.

## Query Restarts


### Usage scenarios and benefits


### Contract and requirements


## Common SQL Dialect


## Blockwise-columnar storage


## Lessons learned and challenges


## Conclusions