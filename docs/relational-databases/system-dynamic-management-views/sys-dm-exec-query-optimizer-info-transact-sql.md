---
title: "sys.dm_exec_query_optimizer_info (Transact-SQL)"
description: sys.dm_exec_query_optimizer_info returns detailed statistics about the operation of the SQL Server query optimizer.
author: rwestMSFT
ms.author: randolphwest
ms.reviewer: derekw
ms.date: 07/05/2024
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "dm_exec_query_optimizer_info_TSQL"
  - "dm_exec_query_optimizer_info"
  - "sys.dm_exec_query_optimizer_info_TSQL"
  - "sys.dm_exec_query_optimizer_info"
helpviewer_keywords:
  - "sys.dm_exec_query_optimizer_info dynamic management view"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016 || =azuresqldb-current || =azure-sqldw-latest || >=sql-server-2016 || >=sql-server-linux-2017 || =azuresqldb-mi-current"
---
# sys.dm_exec_query_optimizer_info (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Returns detailed statistics about the operation of the [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] query optimizer. You can use this view when tuning a workload to identify query optimization problems or improvements. For example, you can use the total number of optimizations, the elapsed time value, and the final cost value to compare the query optimizations of the current workload and any changes observed during the tuning process. Some counters provide data that is relevant only for [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] internal diagnostic use. These counters are marked as "Internal only."

> [!NOTE]  
> To call this from [!INCLUDE [ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] or [!INCLUDE [ssPDW](../../includes/sspdw-md.md)], use the name `sys.dm_pdw_nodes_exec_query_optimizer_info`. [!INCLUDE [synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

| Name | Data type | Description |
| --- | --- | --- |
| `counter` | **nvarchar(4000)** | Name of optimizer statistics event. |
| `occurrence` | **bigint** | Number of occurrences of optimization event for this counter. |
| `value` | **float** | Average property value per event occurrence. |
| `pdw_node_id` | **int** | The identifier for the node that this distribution is on.<br /><br />**Applies to**: [!INCLUDE [ssazuresynapse-md](../../includes/ssazuresynapse-md.md)], [!INCLUDE [ssPDW](../../includes/sspdw-md.md)] |

## Permissions

[!INCLUDE [sssql19-md](../../includes/sssql19-md.md)] and earlier versions, and [!INCLUDE [ssazuremi-md](../../includes/ssazuremi-md.md)], require `VIEW SERVER STATE` permission.

[!INCLUDE [sssql22-md](../../includes/sssql22-md.md)] and later versions, requires `VIEW SERVER PERFORMANCE STATE` permission on the server.

On [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)] **Basic**, **S0**, and **S1** service objectives, and for databases in *elastic pools*, the [server admin](/azure/azure-sql/database/logins-create-manage#existing-logins-and-user-accounts-after-creating-a-new-database) account, the [Microsoft Entra admin](/azure/azure-sql/database/authentication-aad-overview#administrator-structure) account, or membership in the **##MS_ServerStateReader##** [server role](/azure/azure-sql/database/security-server-roles) is required. On all other SQL Database service objectives, either the `VIEW DATABASE STATE` permission on the database, or membership in the **##MS_ServerStateReader##** server role is required.

## Remarks

`sys.dm_exec_query_optimizer_info` contains the following properties (counters). All occurrence values are cumulative and are set to `0` at system restart. All values for value fields are set to `NULL` at system restart. All value-column values that specify an average use the occurrence value from the same row as the denominator in the calculation of the average. All query optimizations are measured when [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] determines changes to `dm_exec_query_optimizer_info`, including both user-generated and system-generated queries. Execution of an already-cached plan doesn't change values in `dm_exec_query_optimizer_info`, only optimizations are significant.

| Counter | Occurrence | Value |
| --- | --- | --- |
| `optimizations` | Total number of optimizations. | Not applicable |
| `elapsed time` | Total number of optimizations. | Average elapsed time per optimization of an individual statement (query), in seconds. |
| `final cost` | Total number of optimizations. | Average estimated cost for an optimized plan in internal cost units. |
| `trivial plan` | Internal only | Internal only |
| `tasks` | Internal only | Internal only |
| `no plan` | Internal only | Internal only |
| `search 0` | Internal only | Internal only |
| `search 0 time` | Internal only | Internal only |
| `search 0 tasks` | Internal only | Internal only |
| `search 1` | Internal only | Internal only |
| `search 1 time` | Internal only | Internal only |
| `search 1 tasks` | Internal only | Internal only |
| `search 2` | Internal only | Internal only |
| `search 2 time` | Internal only | Internal only |
| `search 2 tasks` | Internal only | Internal only |
| `gain stage 0 to stage 1` | Internal only | Internal only |
| `gain stage 1 to stage 2` | Internal only | Internal only |
| `timeout` | Internal only | Internal only |
| `memory limit exceeded` | Internal only | Internal only |
| `insert stmt` | Number of optimizations that are for `INSERT` statements. | Not applicable |
| `delete stmt` | Number of optimizations that are for `DELETE` statements. | Not applicable |
| `update stmt` | Number of optimizations that are for `UPDATE` statements. | Not applicable |
| `contains subquery` | Number of optimizations for a query that contains at least one subquery. | Not applicable |
| `unnest failed` | Internal only | Internal only |
| `tables` | Total number of optimizations. | Average number of tables referenced per query optimized. |
| `hints` | Number of times some hint was specified. Hints counted include: `JOIN`, `GROUP`, `UNION` and `FORCE ORDER` query hints, `FORCE PLAN` set option, and join hints. | Not applicable |
| `order hint` | Number of times where join order was forced. This counter isn't restricted to the `FORCE ORDER` hint. Specifying a join algorithm within a query, such as an `INNER HASH JOIN`, also forces the join order, which increments the counter. | Not applicable |
| `join hint` | Number of times the join algorithm was forced by a join hint. The `FORCE ORDER` query hint doesn't increment this counter. | Not applicable |
| `view reference` | Number of times a view is referenced in a query. | Not applicable |
| `remote query` | Number of optimizations where the query referenced at least one remote data source, such as a table with a four-part name or an `OPENROWSET` result. | Not applicable |
| `maximum DOP` | Total number of optimizations. | Average effective `MAXDOP` value for an optimized plan. By default, effective `MAXDOP` is determined by the **max degree of parallelism** server configuration option, and might be overridden for a specific query by the value of the `MAXDOP` query hint. |
| `maximum recursion level` | Number of optimizations in which a `MAXRECURSION` level greater than `0` was specified with the query hint. | Average `MAXRECURSION` level in optimizations where a maximum recursion level was specified with the query hint. |
| `indexed views loaded` | Internal only | Internal only |
| `indexed views matched` | Number of optimizations where one or more indexed views are matched. | Average number of views matched. |
| `indexed views used` | Number of optimizations where one or more indexed views are used in the output plan after being matched. | Average number of views used. |
| `indexed views updated` | Number of optimizations of a DML statement that produce a plan that maintains one or more indexed views. | Average number of views maintained. |
| `dynamic cursor request` | Number of optimizations in which a dynamic cursor request was specified. | Not applicable |
| `fast forward cursor request` | Number of optimizations in which a fast-forward cursor request was specified. | Not applicable |
| `merge stmt` | Number of optimizations that are for `MERGE` statements. | Not applicable |

## Examples

### A. View statistics on optimizer execution

What are the current optimizer execution statistics for this instance of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]?

```sql
SELECT * FROM sys.dm_exec_query_optimizer_info;
```

### B. View the total number of optimizations

How many optimizations are performed?

```sql
SELECT occurrence AS Optimizations
FROM sys.dm_exec_query_optimizer_info
WHERE counter = 'optimizations';
```

### C. Average elapsed time per optimization

What is the average elapsed time per optimization?

```sql
SELECT ISNULL(value,0.0) AS ElapsedTimePerOptimization
FROM sys.dm_exec_query_optimizer_info
WHERE counter = 'elapsed time';
```

### D. Fraction of optimizations that involve subqueries

What fraction of optimized queries contained a subquery?

```sql
SELECT (
    SELECT CAST(occurrence AS FLOAT)
    FROM sys.dm_exec_query_optimizer_info
    WHERE counter = 'contains subquery'
) / (
    SELECT CAST(occurrence AS FLOAT)
    FROM sys.dm_exec_query_optimizer_info
    WHERE counter = 'optimizations'
) AS ContainsSubqueryFraction;
```

### E. View the total number of hints during optimization

How many hints are counted when `FORCE ORDER` is included as a query hint?

```sql
-- Check hint count before query execution
SELECT ISNULL('', 0) AS [Before],
    [counter],
    occurrence
FROM sys.dm_exec_query_optimizer_info
WHERE [counter] IN (
    'hints',
    'order hint',
    'join hint'
);

SELECT poh.PurchaseOrderID,
    poh.OrderDate,
    pod.ProductID,
    pod.DueDate,
    poh.VendorID
FROM Purchasing.PurchaseOrderHeader AS poh
INNER MERGE JOIN Purchasing.PurchaseOrderDetail AS pod
    ON poh.PurchaseOrderID = pod.PurchaseOrderID
OPTION (
    FORCE ORDER,
    RECOMPILE
);

-- check hint count after query execution
SELECT ISNULL('', 0) AS [After],
    [counter],
    occurrence
FROM sys.dm_exec_query_optimizer_info
WHERE [counter] IN (
    'hints',
    'order hint',
    'join hint'
);
```

## Related content

- [Dynamic Management Views and Functions (Transact-SQL)](system-dynamic-management-views.md)
- [Execution Related Dynamic Management Views and Functions (Transact-SQL)](execution-related-dynamic-management-views-and-functions-transact-sql.md)