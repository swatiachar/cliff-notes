This is a retelling for [BigTable WP](https://research.google/pubs/pub27898/)

Following the same sequence as the paper with simpler examples .

### What is BigTable 
In many ways, Bigtable resembles a database: it shares many implementation strategies with databases. Parallel databases and main-memory databases have achieved scalability and high performance, but Bigtable provides a different interface than such systems. Bigtable does not support a full relational data model; instead, it provides clients with a simple data model that supports dynamic control over data layout and format, and allows clients to reason about the locality properties of the data represented in the underlying storage. 

Schemaless :
Data is indexed using row and column names that can be arbitrary strings. Bigtable also treats data as uninterpreted strings, although clients often serialize various forms of structured and semi-structured data into these strings.

### Data Model 
A Bigtable is a sparse, distributed, persistent multidimensional sorted map. The map is indexed by a row key, column key, and a timestamp; each value in the map
is an uninterpreted array of bytes.

Note : 4 dimentional 
- Row Key: Uniquely identifies a row
- Column Family: Represents a group of columns
- Column Name: Uniquely identifies a column
- Timestamp: Each column cell can have different versions of a value, each identified by a timestamp

            ColumnFamily 
        ColumnName1,ColumnName2
Row Key TimeStamp1: Value1
        TimeStamp2: Value2
        
### API

Client applications can write or delete values in Bigtable, look up values from individual rows, or iterate over a subset of the data in a table.\\

1. Bigtable supports single-row transactions, which can be used to perform atomic read-modify-write sequences on data stored under a single row key. 
2. Bigtable does not currently support general transactions across row keys, although it provides an interface for batching writes across
row keys at the clients.
3. Bigtable allows cells to be used as integer counters. 
4. Bigtable supports the execution of client-supplied scripts in the address spaces of the servers. 


### Building Blocks 

GFS : Bigtable is built on several other pieces of Google infrastructure. Bigtable uses the distributed Google File System (GFS) [17] to store log and data files. 

Cluster : A Bigtable cluster typically operates in a shared pool of machines that run a wide variety of other distributed applications, and Bigtable processes often share the same machines with processes from other applications. 

Cluster management system : Bigtable depends on a cluster management system for scheduling jobs, managing resources on shared machines, dealing with machine failures, and monitoring machine status.

SSTables : The Google SSTable file format is used internally to store Bigtable data. An SSTable provides a persistent, ordered immutable map from keys to values, where both keys and values are arbitrary byte strings. 

Chubby : Bigtable relies on a highly-available and persistent distributed lock service called Chubby.

