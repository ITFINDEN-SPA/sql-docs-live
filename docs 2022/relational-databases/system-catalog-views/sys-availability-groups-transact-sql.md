---
title: "sys.availability_groups (Transact-SQL)"
description: Returns a row for each availability group for which the local instance of SQL Server hosts an availability replica.
author: rwestMSFT
ms.author: randolphwest
ms.date: 04/18/2024
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.availability_groups_TSQL"
  - "availability_groups_TSQL"
  - "sys.availability_groups"
  - "availability_groups"
helpviewer_keywords:
  - "Availability Groups [SQL Server], monitoring"
  - "sys.availability_groups catalog view"
dev_langs:
  - "TSQL"
---
# sys.availability_groups (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Returns a row for each availability group for which the local instance of SQL Server hosts an availability replica. Each row contains a cached copy of the availability group metadata.

| Column name | Data type | Description |
| --- | --- | --- |
| `group_id` | **uniqueidentifier** | Unique identifier (GUID) of the availability group. |
| `name` | **sysname** | Name of the availability group. This is a user-specified name that must be unique within the Windows Server Failover Cluster (WSFC). |
| `resource_id` | **nvarchar(40)** | Resource ID for the WSFC cluster resource. |
| `resource_group_id` | **nvarchar(40)** | Resource Group ID for the WSFC cluster resource group of the availability group. |
| `failure_condition_level` | **int** | User-defined failure condition level under which an automatic failover must be triggered, one of the integer values shown in the table immediately below this table.<br /><br />The failure-condition levels (1-5) range from the least restrictive, level 1, to the most restrictive, level 5. A given condition level encompasses all of the less restrictive levels. Thus, the strictest condition level, 5, includes the four less restrictive condition levels (1-4), level 4 includes levels 1-3, and so forth.<br /><br />To change this value, use the `FAILURE_CONDITION_LEVEL` option of the [ALTER AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/alter-availability-group-transact-sql.md) statement. |
| `health_check_timeout` | **int** | Wait time (in milliseconds) for the [sp_server_diagnostics (Transact-SQL)](../system-stored-procedures/sp-server-diagnostics-transact-sql.md) system stored procedure to return server-health information, before the server instance is assumed to be slow or not responding. The default value is 30000 milliseconds (30 seconds).<br /><br />To change this value, use the `HEALTH_CHECK_TIMEOUT` option of the [ALTER AVAILABILITY GROUP (Transact-SQL)](../../t-sql/statements/alter-availability-group-transact-sql.md) statement. |
| `automated_backup_preference` | **tinyint** | Preferred location for performing backups on the availability databases in this availability group. The following are the possible values and their descriptions.<br /><br />0: Primary. Backups should always occur on the primary replica.<br />1: Secondary only. Performing backups on a secondary replica is preferable.<br />2: Prefer Secondary. Performing backups on a secondary replica is preferred, but performing backups on the primary replica is acceptable if no secondary replica is available for backup operations. This is the default behavior.<br />3: Any Replica. No preference about whether backups are performed on the primary replica or on a secondary replica.<br /><br />For more information, see [Offload supported backups to secondary replicas of an availability group](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md). |
| `automated_backup_preference_desc` | **nvarchar(60)** | Description of `automated_backup_preference`, one of:<br /><br />`PRIMARY`<br />`SECONDARY_ONLY`<br />`SECONDARY`<br />`NONE` |
| `version` | **smallint** | The version of the availability group metadata stored in the Windows Failover Cluster. This version number is incremented when new features are added. |
| `basic_features` | **bit** | Specifies whether this is a Basic availability group. For more information, see [Basic Always On availability groups for a single database](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md). |
| `dtc_support` | **bit** | Specifies whether DTC support is enabled for this availability group. The `DTC_SUPPORT` option of `CREATE AVAILABILITY GROUP` controls this setting. |
| `db_failover` | **bit** | Specifies whether the availability group supports failover for database health conditions. The `DB_FAILOVER` option of `CREATE AVAILABILITY GROUP` controls this setting. |
| `is_distributed` | **bit** | Specifies whether this is a distributed availability group. For more information, see [Distributed availability groups](../../database-engine/availability-groups/windows/distributed-availability-groups.md). |
| `cluster_type` | **tinyint** | 0: Windows Server failover cluster<br />1: None<br />2: External cluster (for example, Linux Pacemaker) |
| `cluster_type_desc` | **nvarchar(60)** | Text description of cluster type |
| `required_synchronized_secondaries_to_commit` | **int** | The number of secondary replicas that must be in a synchronized state for a commit to complete |
| `sequence_number` | **bigint** | Identifies the availability group configuration sequence. Incrementally increases every time the availability group primary replica updates the configuration of the group. |
| `is_contained` | **bit** | 1: Big data cluster master instance configured for high-availability.<br />0: all other. |

## Failure condition level values

The following table describes the possible failure condition levels for the `failure_condition_level` column.

| Value | Failure condition |
| --- | --- |
| `1` | Specifies that an automatic failover should be initiated when any of the following occurs:<br /><br />- The [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] service is down.<br />- The lease of the availability group for connecting to the WSFC failover cluster expires because no ACK is received from the server instance.<br /><br />For more information, see [How It Works: SQL Server Always On Lease Timeout](https://techcommunity.microsoft.com/t5/sql-server-support-blog/how-it-works-sql-server-alwayson-lease-timeout/ba-p/317268). |
| `2` | Specifies that an automatic failover should be initiated when any of the following occurs:<br /><br />- The instance of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] doesn't connect to cluster, and the user-specified `health_check_timeout` threshold of the availability group is exceeded.<br />- The availability replica is in failed state. |
| `3` | Specifies that an automatic failover should be initiated on critical [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] internal errors, such as orphaned spinlocks, serious write-access violations, or too much dumping.<br /><br />This is the default value. |
| `4` | Specifies that an automatic failover should be initiated on moderate [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] internal errors, such as a persistent out-of-memory condition in the [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] internal resource pool. |
| `5` | Specifies that an automatic failover should be initiated on any qualified failure conditions, including:<br /><br />- Exhaustion of SQL Engine worker-threads.<br />- Detection of an unsolvable deadlock. |

## Permissions

Requires `VIEW ANY DEFINITION` permission on the server instance.

## Related content

- [sys.availability_replicas (Transact-SQL)](sys-availability-replicas-transact-sql.md)
- [What is an Always On availability group?](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
- [Monitor Availability Groups (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)