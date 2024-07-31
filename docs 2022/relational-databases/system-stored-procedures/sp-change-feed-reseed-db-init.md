---
title: "sys.sp_change_feed_reseed_db_init (Transact-SQL)"
description: "The sys.sp_change_feed_reseed_db_init system internal stored procedure executes a database reseed."
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.reviewer: imotiwala
ms.date: 03/18/2024
ms.service: fabric
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.sp_change_feed_reseed_db_init_TSQL"
  - "sys.sp_change_feed_reseed_db_init"
  - "sp_change_feed_reseed_db_init_TSQL"
  - "sp_change_feed_reseed_db_init"
helpviewer_keywords:
  - "sp_change_feed_reseed_db_init"
dev_langs:
  - "TSQL"
monikerRange: ">=sql-server-ver16||=azuresqldb-current||=fabric"
---
# sys.sp_change_feed_reseed_db_init (Transact-SQL)

[!INCLUDE [sqlserver2022-asdb-fabric](../../includes/applies-to-version/sqlserver2022-asdb-fabric.md)]

Executes a database reseed.

> [!NOTE]
> This system stored procedure is used internally and is not recommended for direct administrative use. Use the Fabric portal instead. Using this procedure could introduce inconsistency.

This system stored procedure is used for the Fabric Mirrored Database feature for Azure SQL Database. For more information, see [Microsoft Fabric mirrored databases (Preview)](/fabric/database/mirrored-database/overview).

## Syntax

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

```syntaxsql
sys.sp_change_feed_reseed_db_init
    @is_init_needed tinyint
```

## Arguments

#### is_init_needed

Internal use only.

## Returns

`0` (success) or non-zero (failure).

## Permissions

A user with [CONTROL database permissions](../security/permissions-database-engine.md), **db_owner** database role membership, or **sysadmin** server role membership can execute this procedure.

## Related content

- [sys.sp_help_change_feed (Transact-SQL)](sp-help-change-feed.md)
- [sys.sp_help_change_feed_table (Transact-SQL)](sp-help-change-feed-table.md)
- [sys.sp_help_change_feed_table_groups (Transact-SQL)](sp-help-change-feed-table-groups.md)
- [sys.sp_help_change_feed_settings (Transact-SQL)](sp-help-change-feed-settings.md)
- [sys.sp_change_feed_configure_parameters (Transact-SQL)](sp-change-feed-configure-parameters.md)
- [sys.dm_change_feed_log_scan_sessions (Transact-SQL)](../system-dynamic-management-views/sys-dm-change-feed-log-scan-sessions.md)
- [sys.dm_change_feed_errors (Transact-SQL)](../system-dynamic-management-views/sys-dm-change-feed-errors.md)
- [Microsoft Fabric mirrored databases (Preview)](/fabric/database/mirrored-database/overview)
- [Microsoft Fabric mirrored databases monitoring](/fabric/database/mirrored-database/monitor)
- [Explore data in your Mirrored database using Microsoft Fabric](/fabric/database/mirrored-database/explore)