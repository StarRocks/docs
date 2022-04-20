# StarRocks version 2.2

## 2.2.0

Release date: April 22, 2022

## New Features

- [Preview] Resource groups are supported. By using resource groups to control CPU and memory usage, StarRocks can achieve resource isolation and rational use of resources when different tenants perform complex and simple queries in the same cluster.
- [Preview] Java UDFs (user-defined functions) are supported. StarRocks supports writing UDFs in Java, extending StarRocks' functions.
- Primary key model supports partial updates when data is loaded to the primary key model using Stream Load, Broker Load, and Routine Load.  In real-time data update scenarios such as updating orders and joining multiple streams, partial updates allow users to update only a few columns.
- [Preview] JSON data types and JSON functions are supported.
- External tables based on Apache Hudi are supported, which further improves data lake analytics experience and delivers a query performance **x** **times** **that of Trino.**
- The following functions are supported:
  - ARRAY functions, including array_agg, array_sort, array_distinct, array_join, reverse, array_slice, array_concat, array_difference, array_overlap, and array_intersect
  - BITMAP functions, including bitmap_max and bitmap_min
  - Other functions, including retention and square

## Improvement

- The performance of complex queries is optimized, such as those queries reusing common table expression (CTE). As TPC-DS results show, StarRocks delivers a performance up to x times that of Snowflake in complex queries.
- The query performance of object storage-based (AWS S3, Alibaba Cloud OSS) Apache Hive external table is optimized. After optimization, the performance of object storage-based queries is comparable to that of HDFS-based queries.
- When external tables are used to query Apache Hive, StarRocks supports automatic and incremental updating of cached metastore data by consuming Hive Metastore events, such as data changes and partition changes. Moreover, it also supports querying DECIMAL and ARRAY data in Apache Hive.
- The pipeline engine is released, which can adaptively adjust query parallelism. The pipeline engine's profile is optimized.

- StarRocks supports the loading of CSV files with multi-character row delimiters.

### Bug Fixes

The following bugs are fixed:

- Deadlocks occur when data is loaded and changes are committed into tables based on Primary Key model. [#4998](https://github.com/StarRocks/starrocks/pull/4998）

- Some FE (including BDBJE) stability issues. [#4428]([Master is crashed when adding new follower node](https://github.com/StarRocks/starrocks/issues/4426)) (https://github.com/StarRocks/starrocks/pull/4428)、[#4666] (https://github.com/StarRocks/starrocks/pull/4666)、[#2](https://github.com/StarRocks/bdb-je/pull/2)

- The return value overflows when the SUM function is used to calculate a large amount of data. [#3944](https://github.com/StarRocks/starrocks/pull/3944)

- The return values of ROUND and TRUNCATE functions have precision issues. [#4256](https://github.com/StarRocks/starrocks/pull/4256)

- Some SQLancer issues. Please see [SQLancer related issues](https://github.com/StarRocks/starrocks/issues?q=is%3Aissue++label%3Asqlancer++milestone%3A2.2).

### Others

- The Flink connector flink-connector-starrocks supports Flink 1.14.
