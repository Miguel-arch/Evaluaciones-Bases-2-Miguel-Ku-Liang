> Bases de Datos 2, Resumen 2 y 3: Bigtable: A Distributed Storage System for Structured Data  
> Miguel Ku Liang - 2019061913

## Introduction

Bigtable is designed to reliably scale to petabytes of data and thousands of machines, achieving wide applicability, scalability, high performance and high availability. Bigtable resembles a database. It does not support a full relational data model, but provides clients with a simple data model that supports dynamic control over data layout and format and allows clients to reason about the locality properties of the data represented in the underlying storage. Data is indexed using row and column names. It treats data as uninterpreted strings. Clients can control the locality of their data through choices in their schemas. Bigtable schema parameters let clients dynamically control bring data out of memoryu or from disk.

## Data Model


### Rows


### Column Families


### Timestamps


## API


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