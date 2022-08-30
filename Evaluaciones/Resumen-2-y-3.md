> Bases de Datos 2, Resumen 2 y 3: Bigtable: A Distributed Storage System for Structured Data  
> Miguel Ku Liang - 2019061913

## Introduction

Bigtable is designed to reliably scale to petabytes of data and thousands of machines, achieving wide applicability, scalability, high performance and high availability. Bigtable resembles a database. It does not support a full relational data model, but provides clients with a simple data model that supports dynamic control over data layout and format and allows clients to reason about the locality properties of the data represented in the underlying storage. Data is indexed using row and column names. It treats data as uninterpreted strings. Clients can control the locality of their data through choices in their schemas. Bigtable schema parameters let clients dynamically control to bring data out of memory or from disk.

## Data Model

A Bigtable is a sparse, distributed, persistent multidimensional sorted map. It is indexed by a row key, column key and a timestamp. Each value is an uninterpreted array of bytes. A **Webtable** is a Bigtable-like system to keep large collections of web pages and related information that could be used in many projects. 

### Rows

The row keys are arbitrary strings. Every read or write of data under a single row key is atomic. 

Bigtable maintains data in lexicographic order by row key. The row range is dynamically partitioned. Each row range is called a **tablet**. It is the unit of distribution and load balancing, so reads of short row range are efficient and only needs to communicate with a small amount of machines. 

### Column Families

Column keys are grouped in sets called **column families**. They form the basic unit of access control. All data stored in a column family is usually of the same type. A column family must be created before storing data. A table may have an unbounded number of columns. 

A column key is named in the form of ***family:qualifier***. Family names must be printable and qualifiers may be arbitrary strings. 

Access control and disk and memory accounting are performed at the column-family level. 

### Timestamps

Each cell in a Bigtable can contain multiple versions of the same data indexed by timestamps. They are 64-bit integers. They can be assigned by Bigtable, representing real time in microseconds or explicitly assigned by client applications. Applications that need to avoid collisions must generate unique timestamps themselves. Different versions of a cell are sotred in decreasing timestamp order so that the most recent versions can be read first. 

To manage versioned data, it has two per-column-family settings that tell Bigtable to collect cell versions automatically. 

## API

The Bigtable API provides functions for creating and deleting tables and column families. It provides functions for changing cluster, table, and column family metadata. 

Client applications can write or delete values in Bigtable, look up values from individual rows or iterate over a subset of the data in a table. 

Bigtable supports other features that allow the user to manipulate data in more complex ways. It supports single-row transactions that are used to perform atomic read-modify-write sequenceson data stored under a single row key. Bigtable does not support general transactions across row keys, but it provides an interfacce for batching writes across row keys at the clients. It allows cells to be used as integer counters. Bigtable supports the execution of client-supplied scripts in the address spaces of the servers. The scripts are written in a language developed at Google for processing data called **Sawzall**. 

Bigtable can be used with MapReduce, a framework for running large-scale parallel computations developed at Google. 

## Building Blocks


## Implementation


### Tablet Location


### Tablet Assignment


### Tablet Serving


### Compactions


## Refinements


### Locality groups


### Compression


### Caching for read performance


### Bloom filters


### Commit-log implementation


### Speeding up tablet recovery


### Exploiting immutability


## Performance Evaluation


### Single tablet-server performance


### Scaling


## Real Applications


### Google Analytics


### Google Earth


### Personalized Search


## Lessons


## Related Work


## Conclusions