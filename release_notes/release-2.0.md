# StarRocks version 2.0

## 2.0.0

Release date: january 5, 2022

### New Feature

- External Table
  - [Experimental Function]Support for Hive external table on S3
  - DecimalV3 support for external table [#425](https://github.com/StarRocks/starrocks/pull/425)
- Implement complex expressions to be pushed down to the storage layer for computation, thus gaining performance gains
- Primary Key is officially released, which supports Stream Load, Broker Load, Routine Load, and also provides a second-level synchronization tool for MySQL data based on Flink-cdc

### Improvement

- Arithmetic operators optimization
  - Optimize the performance of dictionary with low cardinality [#791](https://github.com/StarRocks/starrocks/pull/791)
  - Optimize the scan performance of int for single table [#273](https://github.com/StarRocks/starrocks/issues/273)
  - Optimize the performance of `count(distinct int)` with high cardinality  [#139](https://github.com/StarRocks/starrocks/pull/139) [#250](https://github.com/StarRocks/starrocks/pull/250)  [#544](https://github.com/StarRocks/starrocks/pull/544)[#570](https://github.com/StarRocks/starrocks/pull/570)
  - Optimize `Group by int` / `limit` / `case when` / `not equa`l in implementation-level
- Memory management optimization
  - Refactor the memory statistics and control framework to accurately count memory usage and completely solve OOM
  - Optimize metadata memory usage
  - Solve the problem of large memory release stuck in execution threads for a long time
  - Add process graceful exit mechanism and support memory leak check [#1093](https://github.com/StarRocks/starrocks/pull/1093)

### Bugfix

- Fix the problem that the Hive external table is timeout to get metadata in a large amount.
- Fix the problem of unclear error message of materialized view creation.
- Fix the implementation of like in vectorization engine [#722](https://github.com/StarRocks/starrocks/pull/722)
- Repair the error of parsing the predicate is in `alter table`[#725](https://github.com/StarRocks/starrocks/pull/725)
- Fix the problem that the `curdate` function can not format the date

## 2.0.1

Release date: january 21, 2022

### Improvement

- Hive's implicit_cast operations can be read when StarRocks uses external tables to query Hive data. [#2829](https://github.com/StarRocks/starrocks/pull/2829)
- The read/write lock is used to fix high CPU usage when StarRocks CBO collects statistics to support high-concurrency queries. [#2901](https://github.com/StarRocks/starrocks/pull/2901)
- CBO statistics gathering and UNION operator are optimized.

### Bugfix

- The query error that is caused by inconsistent global dictionaries of replicas is fixed. [#2700](https://github.com/StarRocks/starrocks/pull/2700) [#2765](https://github.com/StarRocks/starrocks/pull/2765)
- The error that the parameter `exec_mem_limit` during data loading does not take effect is fixed. [#2693](https://github.com/StarRocks/starrocks/pull/2693)
  > The parameter `exec_mem_limit` specifies each BE node's memory limit during data loading.
- The OOM error that occurs when data is imported to the Primary Key Model is fixed. [#2743](https://github.com/StarRocks/starrocks/pull/2743) [#2777](https://github.com/StarRocks/starrocks/pull/2777)
- The error that the BE node stops responding when StarRocks uses external tables to query large MySQL tables is fixed. [#2881](https://github.com/StarRocks/starrocks/pull/2881)

### Behavior Change

StarRocks can use external tables to access Hive and its AWS S3-based external tables. However, the jar file that is used to access S3 data is too large and the binary package of StarRocks does not contain this jar file. If you want to use this jar file, you can download it from [Hive_s3_lib](https://cdn-thirdparty.starrocks.com/hive_s3_jar.tar.gz).

## 2.1.0

Release date: February 24, 2022

### New Features

- [Preview] StarRocks now supports Iceberg external tables.
- [Preview] The pipeline engine is now available. It is a new execution engine designed for multicore scheduling. The query parallelism can be adaptively adjusted without the need to set the parallel_fragment_exec_instance_num parameter. This also improves performance in high concurrency scenarios.
- The CTAS (Create Table As Select) function is supported, making ETL and table creation easier.
- SQL fingerprint is supported. SQL fingerprint is generated in audit.log, which facilitates the location of slow queries.

### Improvements

- Compaction is optimized. A flat table can contain up to 10,000 columns.
- The performance of first-time scan and page cache is optimized. Random I/O is reduced to improve first-time scan performance. The improvement is more noticeable if first-time scan occurs on SATA disks. StarRocks' page cache can store original data, which eliminates the need for bitshuffle encoding and unnecessary decoding. This improves the cache hit rate and query efficiency.
- Schema change is supported in the primary key model. You can add, delete, and modify bitmap indexes by using `Alter table`.
- [Preview] The size of a string can be up to 1 MB.
- JSON load performance is optimized. You can load more than 100 MB JSON data in a single file.
- Bitmap index performance is optimized.
- The performance of StarRocks Hive external tables is optimized. Data in the CSV format can be read.
- DEFAULT CURRENT_TIMESTAMP is supported in the `create table` statement.
- StarRocks supports the loading of CSV files with multiple delimiters.

### BugFix

The following bugs are fixed:

- Auto __op  mapping does not take effect if jsonpaths is specified in the command used for loading JSON data.
- BE nodes fail because the source data changes during data loading using Broker Load.
- Some SQL statements report errors after materialized views are created.
- The routine load does not work due to quoted jsonpaths.
- Query concurrency decreases sharply when the number of columns to query exceeds 200.

### Behavior Change

