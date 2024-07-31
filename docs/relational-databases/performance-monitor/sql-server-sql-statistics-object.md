---
title: "SQL Server, SQL Statistics object"
description: "Learn about the SQLServer:SQL Statistics object, which provides counters to monitor compilation and the type of requests sent to an instance of SQL Server."
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: 12/04/2023
ms.service: sql
ms.subservice: performance
ms.topic: reference
helpviewer_keywords:
  - "SQLServer:SQL Statistics"
  - "SQL Statistics object"
---
# SQL Server, SQL Statistics object
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  The **SQLServer:SQL Statistics** object in [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] provides counters to monitor compilation and the type of requests sent to an instance of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]. Monitoring the number of query compilations and recompilations and the number of batches received by an instance of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] gives you an indication of how quickly [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] is processing user queries and how effectively the query optimizer is processing the queries.  
  
 Compilation is a significant part of a query's turnaround time. In order to save the compilation cost, the [!INCLUDE [ssDE](../../includes/ssde-md.md)] saves the compiled query plan in a query cache. The objective of the cache is to reduce compilation by storing compiled queries for later reuse, therefore ending the requirement to recompile queries when later executed. However, each unique query must be compiled at least one time. Query recompilations can be caused by the following factors:  
  
-   Schema changes, including base schema changes such as adding columns or indexes to a table, or statistics schema changes such as inserting or deleting a significant number of rows from a table.  
  
-   Environment (SET statement) changes. Changes in session settings such as ANSI_PADDING or ANSI_NULLS can cause a query to be recompiled.  
  
 For more information about simple and forced parameterization, see [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md).  
  
 These are the [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Statistics** counters.  
  
|SQL Server SQL Statistics counters|Description|  
|----------------------------------------|-----------------|  
|**Auto-Param Attempts/sec**|Number of auto-parameterization attempts per second. Total should be the sum of the failed, safe, and unsafe auto-parameterizations. Auto-parameterization occurs when an instance of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] tries to parameterize a [!INCLUDE [tsql](../../includes/tsql-md.md)] request by replacing some literals with parameters so that reuse of the resulting cached execution plan across multiple similar-looking requests is possible. Auto-parameterizations are also known as simple parameterizations in newer versions of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]. This counter does not include forced parameterizations.|  
|**Batch Requests/sec**|Number of [!INCLUDE [tsql](../../includes/tsql-md.md)] command batches received per second. This statistic is affected by all constraints (such as I/O, number of users, cache size, complexity of requests, and so on). High batch requests mean good throughput.|  
|**Failed Auto-Params/sec**|Number of failed auto-parameterization attempts per second. This should be small. Auto-parameterizations are also known as simple parameterizations in later versions of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Forced Parameterizations/sec**|Number of successful forced parameterizations per second.|  
|**Guided Plan Executions/sec**|Number of plan executions per second in which the query plan has been generated by using a plan guide.|  
|**Misguided Plan Executions/sec**|Number of plan executions per second in which a plan guide could not be honored during plan generation. The plan guide was disregarded and normal compilation was used to generate the executed plan.|  
|**Safe Auto-Params/sec**|Number of safe auto-parameterization attempts per second. Safe refers to a determination that a cached execution plan can be shared between different similar-looking [!INCLUDE [tsql](../../includes/tsql-md.md)] statements. [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] makes many auto-parameterization attempts some of which turn out to be safe and others fail. Auto-parameterizations are also known as simple parameterizations in later versions of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]. This does not include forced parameterizations.|  
|**SQL Attention rate**|Number of attentions per second. An attention is a request by the client to end the currently running request.|  
|**SQL Compilations/sec**|Number of SQL compilations per second. Indicates the number of times the compile code path is entered. Includes compiles caused by statement-level recompilations in [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]. After [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] user activity is stable, this value reaches a steady state.|  
|**SQL Re-Compilations/sec**|Number of statement recompiles per second. Counts the number of times statement recompiles are triggered. Generally, you want the recompiles to be low.|  
|**Unsafe Auto-Params/sec**|Number of unsafe auto-parameterization attempts per second. For example, the query has some characteristics that prevent the cached plan from being shared. These are designated as unsafe. This does not count the number of forced parameterizations.|  
  
  
## Example

You begin to explore the query performance counters in this object using this T-SQL query on the [sys.dm_os_performance_counters](../system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) dynamic management view:

```sql
SELECT * FROM sys.dm_os_performance_counters
WHERE object_name LIKE '%SQL Statistics%';
```  

## Related content

- [SQL Server, Plan Cache object](sql-server-plan-cache-object.md)
- [Monitor Resource Usage (Performance Monitor)](monitor-resource-usage-system-monitor.md)