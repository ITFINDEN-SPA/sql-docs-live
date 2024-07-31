---
title: In-memory technologies
description: In-memory technologies greatly improve the performance of transactional and analytics workloads in Azure SQL Managed Instance.
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.reviewer: mathoma
ms.date: 12/13/2023
ms.service: sql-managed-instance
ms.subservice: performance
ms.topic: conceptual
ms.custom:
  - sqldbrb=2
monikerRange: "=azuresql||=azuresql-mi"
---
# Optimize performance by using in-memory technologies in Azure SQL Managed Instance
[!INCLUDE [appliesto-sqlmi](../includes/appliesto-sqlmi.md)]

> [!div class="op_single_selector"]
> * [Azure SQL Database](../database/in-memory-oltp-overview.md?view=azuresql-db&preserve-view=true)
> * [Azure SQL Managed Instance](in-memory-oltp-overview.md?view=azuresql-mi&preserve-view=true)

In-memory technologies enable you to improve performance of your application, and potentially reduce cost of your SQL managed instance. In-memory OLTP is available in the [Business Critical](resource-limits.md#service-tier-characteristics) service tier of Azure SQL Managed Instance.

## When to use in-memory technologies

By using in-memory technologies, you can achieve performance improvements with various workloads:

- **Transactional** (online transactional processing (OLTP)) where most of the requests read or update smaller set of data, for example, create/read/update/delete (CRUD) operations.
- **Analytic** (online analytical processing (OLAP)) where most of the queries have complex calculations for reporting purposes, and also regularly scheduled processes that perform load (or bulk load) operations and/or write data changes to existing tables. Often, OLAP workloads are updated periodically from OLTP workloads.
- **Mixed** (hybrid transaction/analytical processing (HTAP)) where both OLTP and OLAP queries are executed on the same set of data.

In-memory technologies can improve performance of these workloads by keeping the data that should be processed into the memory, using native compilation of the queries, or advanced processing such as batch processing and SIMD instructions that are available on the underlying hardware.

## Overview

Azure SQL Managed Instance supports the following in-memory technologies:

- [In-memory OLTP](/sql/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization?view=azuresqldb-mi-current&preserve-view=true) increases number of transactions per second and reduces latency for transaction processing. Scenarios that benefit from in-memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.
- [Clustered columnstore indexes](/sql/relational-databases/indexes/columnstore-indexes-overview?view=azuresqldb-mi-current&preserve-view=true#clustered-columnstore-index) reduce your storage footprint (up to 10 times) and improve performance for reporting and analytics queries. You can use it with fact tables in your data marts to fit more data in your database and improve performance. Also, you can use it with historical data in your operational database to archive and be able to query up to 10 times more data.
- [Nonclustered columnstore indexes](/sql/relational-databases/indexes/columnstore-indexes-overview?view=azuresqldb-mi-current&preserve-view=true#nonclustered-columnstore-index) for HTAP help you to gain real-time insights into your business through querying the operational database directly, without the need to run an expensive extract, transform, and load (ETL) process and wait for the data warehouse to be populated. Nonclustered columnstore indexes allow fast execution of analytics queries on the OLTP database, while reducing the impact on the operational workload.
- [Memory-optimized clustered columnstore indexes](/sql/relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics?view=azuresqldb-mi-current&preserve-view=true) for HTAP enables you to perform fast transaction processing, and to *concurrently* run analytics queries very quickly on the same data.

Columnstore indexes and in-memory OLTP were introduced to SQL Server in 2012 and 2014, respectively. Azure SQL Database, Azure SQL Managed Instance, and SQL Server share the same implementation of in-memory technologies.

> [!NOTE]
> For a detailed step-by-step tutorial to demonstrate the performance advantages of in-memory OLTP technology, using the `AdventureWorksLT` sample database and ostress.exe, see [In-memory sample in Azure SQL Managed Instance](in-memory-oltp-sample.md?view=azuresql-mi&preserve-view=true).

## Benefits of in-memory technology

Because of the more efficient query and transaction processing, in-memory technologies also help you to reduce cost. Once in the Business Critical service tier of Azure SQL Managed Instance, you typically don't need to upgrade the SQL managed instance to achieve performance gains. In some cases, you might even be able reduce the pricing tier, while still seeing performance improvements with in-memory technologies.

This article describes aspects of in-memory OLTP and columnstore indexes that are specific to Azure SQL Managed Instance, and also includes samples:

- You'll see the impact of these technologies on storage and data size limits.
- You'll see how to manage the movement of databases that use these technologies between the different pricing tiers.
- You'll see two samples that illustrate the use of in-memory OLTP, as well as columnstore indexes.

For more information about in-memory OLTP in SQL Server, see:

- [In-memory OLTP overview and usage scenarios](/sql/relational-databases/in-memory-oltp/overview-and-usage-scenarios?view=azuresqldb-mi-current&preserve-view=true) (includes references to customer case studies and information to get started)
- [Documentation for in-memory OLTP](/sql/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization?view=azuresqldb-mi-current&preserve-view=true)
- [Columnstore Indexes Guide](/sql/relational-databases/indexes/columnstore-indexes-overview?view=azuresqldb-mi-current&preserve-view=true)
- Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](/sql/relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics?view=azuresqldb-mi-current&preserve-view=true)

## In-memory OLTP

In-memory OLTP technology provides extremely fast data access operations by keeping all data in memory. It also uses specialized indexes, native compilation of queries, and latch-free data-access to improve performance of the OLTP workload. There are two ways to organize your in-memory OLTP data:

- **Memory-optimized rowstore** format where every row is a separate memory object. This is a classic in-memory OLTP format optimized for high-performance OLTP workloads. There are two types of memory-optimized tables that can be used in the memory-optimized rowstore format:

  - *Durable tables* (SCHEMA_AND_DATA) where the rows placed in memory are preserved after server restart. This type of tables behaves like a traditional rowstore table with the additional benefits of in-memory optimizations.
  - *Nondurable tables* (SCHEMA_ONLY) where the rows are not-preserved after restart. This type of table is designed for temporary data (for example, replacement of temp tables), or tables where you need to quickly load data before you move it to some persisted table (so called staging tables).

- **Memory-optimized columnstore** format where data is organized in a columnar format. This structure is designed for HTAP scenarios where you need to run analytic queries on the same data structure where your OLTP workload is running.

> [!NOTE]
> In-memory OLTP technology is designed for the data structures that can fully reside in memory. Since the In-memory data cannot be offloaded to disk, make sure that you are using SQL managed instance that has enough memory. For more information, see [Data size and storage cap for in-memory OLTP](#data-size-and-storage-cap-for-in-memory-oltp).

- A quick primer on in-memory OLTP: [Quickstart 1: In-memory OLTP Technologies for Faster T-SQL Performance](/sql/relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp?view=azuresqldb-mi-current&preserve-view=true).

### Data size and storage cap for in-memory OLTP

In-memory OLTP includes memory-optimized tables, which are used for storing user data. These tables are required to fit in memory. This idea is referred to as *in-memory OLTP storage*.

The Business Critical service tier includes a certain amount of **Max In-Memory OLTP memory**, [determined by the number of vCores](resource-limits.md?view=azuresql-mi&preserve-view=true).

The following items count toward your in-memory OLTP storage cap:

- Active user data rows in memory-optimized tables and table variables. Old row versions don't count toward the cap.
- Indexes on memory-optimized tables.
- Operational overhead of ALTER TABLE operations.

If you hit the cap, you receive an out-of-quota error, and you are no longer able to insert or update data. To mitigate this error, delete data or increase the pricing tier of the database or pool.

For details about monitoring in-memory OLTP storage utilization and configuring alerts when you almost hit the cap, see [Monitor in-memory storage](in-memory-oltp-monitor-space.md?view=azuresql-mi&preserve-view=true).

### Change hardware configuration or vCore count

Downgrading your hardware configuration or vCore count can negatively impact your SQL managed instance.

Data in memory-optimized tables must fit within the in-memory OLTP storage limit for your hardware configuration and vCore count. If you try to scale-down to a setting that doesn't have enough available in-memory OLTP storage, the operation fails.

#### Determine whether in-memory objects exist

There is a programmatic way to understand whether a given database in your SQL managed instance supports in-memory OLTP. You can execute the following Transact-SQL query:

```sql
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

If the query returns `1`, in-memory OLTP is supported in this database.

The following queries identify all objects using in-memory technology:

```sql
SELECT * FROM sys.tables WHERE is_memory_optimized=1
SELECT * FROM sys.table_types WHERE is_memory_optimized=1
SELECT * FROM sys.sql_modules WHERE uses_native_compilation=1
```

## In-memory columnstore

In-memory columnstore technology is enabling you to store and query a large amount of data in the tables. Columnstore technology uses column-based data storage format and batch query processing to achieve gain up to 10 times the query performance in OLAP workloads over traditional row-oriented storage. You can also achieve gains up to 10 times the data compression over the uncompressed data size.

There are two types of columnstore models that you can use to organize your data:

- **Clustered columnstore** where all data in the table is organized in the columnar format. In this model, all rows in the table are placed in columnar format that highly compresses the data and enables you to execute fast analytical queries and reports on the table. Depending on the nature of your data, the size of your data might be decreased 10x-100x. Clustered columnstore model also enables fast ingestion of large amount of data (bulk-load) since large batches of data greater than 100,000 rows are compressed before they are stored on disk. This model is a good choice for the classic data warehouse scenarios.
- **Non-clustered columnstore** where the data is stored in traditional rowstore table and there is an index in the columnstore format that is used for the analytical queries. This model enables Hybrid Transactional-Analytic Processing (HTAP): the ability to run performant real-time analytics on a transactional workload. OLTP queries are executed on rowstore table that is optimized for accessing a small set of rows, while OLAP queries are executed on columnstore index that is better choice for scans and analytics. The query optimizer dynamically chooses rowstore or columnstore format based on the query. Nonclustered columnstore indexes don't decrease the size of the data since original data-set is kept in the original rowstore table without any change. However, the size of additional columnstore index should be in order of magnitude smaller than the equivalent B-tree index.

> [!NOTE]
> In-memory columnstore technology keeps only the data that is needed for processing in the memory, while the data that cannot fit into the memory is stored on-disk. Therefore, the amount of data in in-memory columnstore structures can exceed the amount of available memory.

### Data size and storage for columnstore indexes

Columnstore indexes aren't required to fit in memory. Therefore, the only cap on the size of the indexes is the maximum overall database size. For more information, see [Azure SQL Managed Instance resource limits](resource-limits.md?view=azuresql-mi&preserve-view=true). Azure SQL Managed Instance supports columnstore indexes in all tiers.

When you use clustered columnstore indexes, columnar compression is used for the base table storage. This compression can significantly reduce the storage footprint of your user data, which means that you can fit more data in the database. And the compression can be further increased with [columnar archival compression](/sql/relational-databases/data-compression/data-compression?view=azuresqldb-mi-current&preserve-view=true#using-columnstore-and-columnstore-archive-compression). The amount of compression that you can achieve depends on the nature of the data, but 10 times the compression is not uncommon.

For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times the compression by using columnstore indexes, you can fit a total of 10 TB of user data in the database.

When you use nonclustered columnstore indexes, the base table is still stored in the traditional rowstore format. Therefore, the storage savings aren't as significant as with clustered columnstore indexes. However, if you're replacing many traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in the storage footprint for the table.

## Related content

- [In-memory sample in Azure SQL Managed Instance](in-memory-oltp-sample.md?view=azuresql-mi&preserve-view=true)
- [Quickstart 1: In-memory OLTP Technologies for faster T-SQL Performance](/sql/relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp?view=azuresqldb-mi-current&preserve-view=true)
- [Use in-memory OLTP in an existing Azure SQL application](in-memory-oltp-configure.md?view=azuresql-mi&preserve-view=true)
- [In-memory OLTP overview and usage scenarios](/sql/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization?view=azuresqldb-mi-current&preserve-view=true)
- [Monitor in-memory OLTP storage](in-memory-oltp-monitor-space.md?view=azuresql-mi&preserve-view=true)
- [Learn about in-memory OLTP](/sql/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization?view=azuresqldb-mi-current&preserve-view=true)
- [Learn about columnstore indexes](/sql/relational-databases/indexes/columnstore-indexes-overview?view=azuresqldb-mi-current&preserve-view=true)
- [Learn about real-time operational analytics](/sql/relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics?view=azuresqldb-mi-current&preserve-view=true)
- [Technical article: In-memory OLTP – Common Workload Patterns and Migration Considerations in SQL Server 2014](/previous-versions/dn673538(v=msdn.10))
