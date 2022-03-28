# Basics of Elasticsearch. 

---

## Elasticsearch 

 Elasticsearch is a distributed, free and open search and analytics engine for all types of data, including textual, numerical, geospatial, structured, and unstructured. Elasticsearch is built on Apache Lucene. Documented oriented(JSON) data saving like objects. 

---



## Why Elasticsearch?
+ Query 
    - It lets users perform and combine many types of searches like structured and unstructured, geo, metric etc data. 
+ Analyze 
    - Users can understand billions of log lines easily. It provides aggregations which help users to zoom out to explore trends and patterns in data.

## Index  
+ An index is  like a database in a relational database. It has a mapping which defines multiple types.
+ An index is a logical namespace which maps to one or more primary shards and can have zero or more replica shards.
---
Basic concept is that elasticsearch distributes data around the cluster.

## MySQL ⇒ Databases ⇒ Tables ⇒ Columns/Rows

## Elasticsearch ⇒ Indices ⇒ Types ⇒ Documents with properties.
---

+ Document 
- A document is a basic unit of information which can be indexed. It is expressed in JSON which is an ubiquitous internet data interchange format.

+ Shards 
- Elasticsearch provides the ability to subdivide the index into multiple pieces called shards. Each shard is in itself a fully-functional and independent “index” that can be hosted on any node within the cluster.

+ Replicas 
- Elasticsearch allows you to make one or more copies of your index’s shards which are called replica shards or replica.

+ Cluster 
- Group of multiple nodes of documents is a cluster.
+ Elasticsearch cluster is a collection of multiple indices(databases) which in turn contain multiple Types(tables). These types hold multiple documents(row) and each document has properties(columns.)


+ API Conventions 
- The elasticsearch REST APIs are accessed using JSON over HTTP. Elasticsearch uses following conventions throughout the REST API.
- Multiple Indices
start: 
Notations are used to perform operations in multiple indices
Comma separated notations (demo1, demo2, demo3)
Wildcard notations (*,+,-) - (demo*, demo2, +demo3, -demo3) for all indices.
URL query string parameters.
Ignore_unavialable
Allow_no_indices
expand_wildcards
Date Math Support in Index Name.
Elasticsearch is used to search indices according to date and time.
Specifying date and time in a specific format

Common Options
Pretty Result
Human Readable Output
Date Math
Response Filtering
Flat settings
Parameter
No Values
Time Units
Byte Size Units
Unit-less quantities
Distance Units
Fuzziness
Enabling Stack Traces
Request Body in Query String


URL based ACCESS CONTROL.
Users can use a proxy with URL-Based access control to secure access to the Elasticsearch indices
User has an option of specifying an index in the URL and on each individual request like:
Multi-search
Multi-get
Bulk


Types of APIs
Document APIs
Index API
Get API
Update API
Delete API
Search APIs - execute search query and get back search hits that match the query.
Multi Index 
It is used to search for the documents present in all the indices or in some specific indices
Multi-Type
It is used to search all the documents in an index across all types or in some specified type.
URI search
Various parameters can be passed in a search operation using Uniform Resource Identifier:
q (../_search?q=year:yyyy)
timeout
lenient
terminate_after
fields
from
sort
size


Aggregation
Aggregation collects all the data which is selected by the search query. This framework consists of many building blocks called aggregators, which help in building complex summaries of the data.
Types of Aggregation
Bucketing
Metric
Matrix
Pipeline

Index APIs - It is responsible for managing all the aspects of index like settings, aliases, mappings, indexes templates.
Create Index
Delete Index
Get Index
Index Exits
Open/Close Index API
Index Aliases
Index Settings
Index Template
Index Stats
Flush
Refresh
Analyze.

Cluster APIs - Cluster API is used for getting the information about the cluster and its nodes and making changes in them.
Cluster Health
Cluster State
Cluster Stats
Pending Cluster Task
Cluster Reroute
Node Stats
Nodes hot_threads.
Query DSL (Domain specific language)
Elasticsearch provides a full Query DSL based on JSON to define queries. Query DSL is an AST of queries, consisting of two types of clauses
Leaf Query Clauses.
Compound Query Clauses.


MAPPING  - Mapping is the process of defining how a document and the fields that it contains are stored and indexed.
Mapping Types 
Meta - fields
Fields or properties
Field Data Types
Core Data Types
Complex Data Types
Geo Data Types
Specialized Data Types

Analysis -  During a search operation when a query is processed, the content of any index is analyzed by the analysis module.
Analyzer 
Tokenizer
Token filter
Character filter

Modules - Elasticsearch is composed of a number of modules, which are mainly responsible for its functionality.
Types of settings:
Static setting -  These settings need to be configured on the config (elasticsearch.yml) file before starting the Elasticsearch.
Dynamic Setting - These settings can be set on live Elasticsearch.
Modules types - 

# Most common index patterns:

## Monolith Index:
These kinds of indices are created when external data is pushed into elasticsearch for indexing and aggregation of data. Data is spread out across multiple nodes in a cluster. 
Re-indexing can be better achieved by scaling out the number of shards.






Monolith indexes are generally used to optimize for search, for bulk updates occasionally. 
For example: If mapping needs to be changed in an index, it is necessary to re-create the index or reindex to ensure the consistency. 
In this situation, in terms of speed, may require more shards. Scaling out to handle the reindexing load. Thus, Sharding allows more than one node to participate in the reindexing. But numbers of shards cannot be changed when an index has been created.
But shards are mutable by the index shrinking.
Shrink the total number of shards.
Must be a factor of the original numbers of shards.
Shards should not be too big or too small to optimize search performance.
Rule of Thumb: 1 million docs per shard and a max of 5 to 10 GB on disk.
Index shrinking by example: If the number of shards count is prime number then, Its shard count can be reduced to value divisible by itself or 1.
Index shrinking lets you expand and contract shard count to better optimize performance and resource allocation.
Index shrinking != re-indexing.

