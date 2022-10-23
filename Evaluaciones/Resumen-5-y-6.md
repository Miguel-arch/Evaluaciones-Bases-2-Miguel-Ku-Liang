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


### DIstributed query compilation



### Distributed Execution


### Distributed joins


### Query distribution APIs


## Query Range Extraction


### Problem statement


### Compile-time rewriting


### Filter tree


## Query Restarts


### Usage scenarios and benefits


### Contract and requirements


## Common SQL Dialect


## Blockwise-columnar storage


## Lessons learned and challenges


## Conclusions