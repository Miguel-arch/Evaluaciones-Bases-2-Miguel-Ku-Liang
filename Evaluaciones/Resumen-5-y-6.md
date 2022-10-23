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