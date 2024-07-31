---
title: "sys.dm_db_xtp_checkpoint_stats (Transact-SQL)"
description: sys.dm_db_xtp_checkpoint_stats returns statistics about the In-Memory OLTP checkpoint operations in the current database. Learn how this view differs for versions of SQL Server.
author: rwestMSFT
ms.author: randolphwest
ms.date: 07/08/2024
ms.service: sql
ms.subservice: in-memory-oltp
ms.topic: "reference"
f1_keywords:
  - "dm_db_xtp_checkpoint_stats"
  - "dm_db_xtp_checkpoint_stats_TSQL"
  - "sys.dm_db_xtp_checkpoint_stats"
  - "sys.dm_db_xtp_checkpoint_stats_TSQL"
helpviewer_keywords:
  - "sys.dm_db_xtp_checkpoint_stats dynamic management view"
dev_langs:
  - "TSQL"
monikerRange: ">=sql-server-2016 || >=sql-server-linux-2017 || =azuresqldb-mi-current"
---
# sys.dm_db_xtp_checkpoint_stats (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Returns statistics about the [!INCLUDE [inmemory](../../includes/inmemory-md.md)] checkpoint operations in the current database. If the database has no [!INCLUDE [inmemory](../../includes/inmemory-md.md)] objects, `sys.dm_db_xtp_checkpoint_stats` returns an empty result set.

For more information, see [[!INCLUDE [inmemory](../../includes/inmemory-md.md)] (In-Memory Optimization)](../in-memory-oltp/overview-and-usage-scenarios.md).

```sql
USE [In_Memory_db_name]
SELECT * FROM sys.dm_db_xtp_checkpoint_stats;
```

[!INCLUDE [ssSQL14](../../includes/sssql14-md.md)] is substantially different from more recent versions, and is discussed separately.

## [SQL Server 2016 and later versions](#tab/sql2016)

The following table describes the columns in `sys.dm_db_xtp_checkpoint_stats`, for [!INCLUDE [sssql16-md](../../includes/sssql16-md.md)] and later versions.

| Column name | Type | Description |
| --- | --- | --- |
| `last_lsn_processed` | **bigint** | Last LSN seen by the controller. |
| `end_of_log_lsn` | **numeric(38)** | The LSN of the end of log. |
| `bytes_to_end_of_log` | **bigint** | Log bytes unprocessed by the controller, corresponding to the bytes between `last_lsn_processed` and `end_of_log_lsn`. |
| `log_consumption_rate` | **bigint** | Rate of transaction log consumption by the controller (in KB/sec). |
| `active_scan_time_in_ms` | **bigint** | Time spent by the controller in actively scanning the transaction log. |
| `total_wait_time_in_ms` | **bigint** | Cumulative wait time for the controller while not scanning the log. |
| `waits_for_io` | **bigint** | Number of waits for log IO incurred by the controller thread. |
| `io_wait_time_in_ms` | **bigint** | Cumulative time spent waiting on log IO by the controller thread. |
| `waits_for_new_log_count` | **bigint** | Number of waits incurred by the controller thread for a new log to be generated. |
| `new_log_wait_time_in_ms` | **bigint** | Cumulative time spent waiting on a new log by the controller thread. |
| `idle_attempts_count` | **bigint** | Number of times the controller transitioned to an idle state. |
| `tx_segments_dispatched` | **bigint** | Number of segments seen by the controller and dispatched to the serializers. Segment is a contiguous portion of log that forms a unit of serialization. It is currently sized to 1 MB, but can change in future. |
| `segment_bytes_dispatched` | **bigint** | Total byte count of bytes dispatched by the controller to serializers, since the database restart. |
| `bytes_serialized` | **bigint** | Total count of bytes serialized since database restart. |
| `serializer_user_time_in_ms` | **bigint** | Time spent by serializers in user mode. |
| `serializer_kernel_time_in_ms` | **bigint** | Time spent by serializers in kernel mode. |
| `xtp_log_bytes_consumed` | **bigint** | Total count of log bytes consumed since the database restart. |
| `checkpoints_closed` | **bigint** | Count of checkpoints closed since the database restart. |
| `last_closed_checkpoint_ts` | **bigint** | Timestamp of the last closed checkpoint. |
| `hardened_recovery_lsn` | **numeric(38)** | Recovery starts from this LSN. |
| `hardened_root_file_guid` | **uniqueidentifier** | GUID of the root file that hardened as a result of the last completed checkpoint. |
| `hardened_root_file_watermark` | **bigint** | **Internal Only**. Specifies how far it is valid to read the root file up to (this is an internally relevant type only - called BSN). |
| `hardened_truncation_lsn` | **numeric(38)** | LSN of the truncation point. |
| `log_bytes_since_last_close` | **bigint** | Bytes from last close to the current end of log. |
| `time_since_last_close_in_ms` | **bigint** | Time since last close of the checkpoint. |
| `current_checkpoint_id` | **bigint** | Currently new segments are being assigned to this checkpoint. The checkpoint system is a pipeline. The current checkpoint is the one which segments from the log are being assigned to. Once it reaches a limit, the controller releases the checkpoint, and a new one created as current. |
| `current_checkpoint_segment_count` | **bigint** | Count of segments in the current checkpoint. |
| `recovery_lsn_candidate` | **bigint** | **Internally Only**. Candidate to be picked as recoverylsn when `current_checkpoint_id` closes. |
| `outstanding_checkpoint_count` | **bigint** | Number of checkpoints in the pipeline waiting to be closed. |
| `closing_checkpoint_id` | **bigint** | ID of the closing checkpoint.<br /><br />Serializers are working in parallel, so once they finish, the checkpoint is a candidate for closing by close thread. But the close thread can only close one at a time and it must be in order, so the closing checkpoint is the one that the close thread is working on. |
| `recovery_checkpoint_id` | **bigint** | ID of the checkpoint to be used in recovery. |
| `recovery_checkpoint_ts` | **bigint** | Time stamp of recovery checkpoint. |
| `bootstrap_recovery_lsn` | **numeric(38)** | Recovery LSN for the bootstrap. |
| `bootstrap_root_file_guid` | **uniqueidentifier** | GUID of the root file for the bootstrap. |
| `internal_error_code` | **bigint** | Error seen by any of the controller, serializer, close, and merge threads. |
| `bytes_of_large_data_serialized` | **bigint** | Specifies the amount of data that was serialized. |
| `db_in_checkpoint_only_mode` | **bit** | True if database is in in-memory OLTP checkpoint-only mode.<br /><br />**Applies to:** [!INCLUDE [sssql22-md](../../includes/sssql22-md.md)] and later versions. |

## [SQL Server 2014](#tab/sql2014)

The following table describes the columns in `sys.dm_db_xtp_checkpoint_stats`, for [!INCLUDE [ssSQL14](../../includes/sssql14-md.md)].

| Column name | Type | Description |
| --- | --- | --- |
| `log_to_process_in_bytes` | **bigint** | The number of log bytes between the thread's current log sequence number (LSN) and the end-of-log. |
| `total_log_blocks_processed` | **bigint** | Total number of log blocks processed since server startup. |
| `total_log_records_processed` | **bigint** | Total number of log records processed since server startup. |
| `xtp_log_records_processed` | **bigint** | Total number of [!INCLUDE [inmemory](../../includes/inmemory-md.md)] log records processed since server startup. |
| `total_wait_time_in_ms` | **bigint** | Cumulative wait time in ms. |
| `waits_for_io` | **bigint** | Number of waits for log IO. |
| `io_wait_time_in_ms` | **bigint** | Cumulative time spent waiting on log IO. |
| `waits_for_new_log` | **bigint** | Number of waits for new log to be generated. |
| `new_log_wait_time_in_ms` | **bigint** | Cumulative time spent waiting on new log. |
| `log_generated_since_last_checkpoint_in_bytes` | **bigint** | Amount of log generated since the last [!INCLUDE [inmemory](../../includes/inmemory-md.md)] checkpoint. |
| `ms_since_last_checkpoint` | **bigint** | Amount of time in milliseconds since the last [!INCLUDE [inmemory](../../includes/inmemory-md.md)] checkpoint. |
| `checkpoint_lsn` | **numeric (38)** | The recovery log sequence number (LSN) associated with the last completed [!INCLUDE [inmemory](../../includes/inmemory-md.md)] checkpoint. |
| `current_lsn` | **numeric (38)** | The LSN of the log record that is currently processing. |
| `end_of_log_lsn` | **numeric (38)** | The LSN of the end of the log. |
| `task_address` | **varbinary(8)** | The address of the SOS_Task. Join to `sys.dm_os_tasks` to find additional information. |

---

## Permissions

[!INCLUDE [sssql19-md](../../includes/sssql19-md.md)] and earlier versions require `VIEW DATABASE STATE` permission on the database.

[!INCLUDE [sssql22-md](../../includes/sssql22-md.md)] and later versions, require `VIEW DATABASE PERFORMANCE STATE` permission on the database.

## Related content

- [Introduction to Memory-Optimized Tables](../in-memory-oltp/introduction-to-memory-optimized-tables.md)
- [Memory-Optimized Table Dynamic Management Views (Transact-SQL)](memory-optimized-table-dynamic-management-views-transact-sql.md)
- [[!INCLUDE[inmemory](../../includes/inmemory-md.md)] Overview and Usage Scenarios](../in-memory-oltp/overview-and-usage-scenarios.md)
- [Optimize performance by using in-memory technologies in Azure SQL Database](/azure/azure-sql/database/in-memory-oltp-overview?view=azuresql-db&preserve-view=true)
- [Optimize performance by using in-memory technologies in Azure SQL Managed Instance](/azure/azure-sql/managed-instance/in-memory-oltp-overview?view=azuresql-mi&preserve-view=true)
