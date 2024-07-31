---
title: "sp_addsynctriggers (Transact-SQL)"
description: Creates triggers at the Subscriber used with all types of updatable subscriptions.
author: markingmyname
ms.author: maghan
ms.reviewer: randolphwest
ms.date: 01/23/2024
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_addsynctriggers_TSQL"
  - "sp_addsynctriggers"
helpviewer_keywords:
  - "sp_addsynctriggers"
dev_langs:
  - "TSQL"
---
# sp_addsynctriggers (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Creates triggers at the Subscriber used with all types of updatable subscriptions (immediate, queued, and immediate updating with queued updating as failover). This stored procedure is executed at the Subscriber on the subscription database.

> [!IMPORTANT]  
> The [sp_script_synctran_commands](sp-script-synctran-commands-transact-sql.md) procedure should be used instead of `sp_addsynctrigger`. [sp_script_synctran_commands](sp-script-synctran-commands-transact-sql.md) generates a script that contains the `sp_addsynctrigger` calls.

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
sp_addsynctriggers
    [ @sub_table = ] N'sub_table'
    , [ @sub_table_owner = ] N'sub_table_owner'
    , [ @publisher = ] N'publisher'
    , [ @publisher_db = ] N'publisher_db'
    , [ @publication = ] N'publication'
    , [ @ins_proc = ] N'ins_proc'
    , [ @upd_proc = ] N'upd_proc'
    , [ @del_proc = ] N'del_proc'
    , [ @cftproc = ] N'cftproc'
    , [ @proc_owner = ] N'proc_owner'
    [ , [ @identity_col = ] N'identity_col' ]
    [ , [ @ts_col = ] N'ts_col' ]
    [ , [ @filter_clause = ] N'filter_clause' ]
    , [ @primary_key_bitmap = ] primary_key_bitmap
    [ , [ @identity_support = ] identity_support ]
    [ , [ @independent_agent = ] independent_agent ]
    , [ @distributor = ] N'distributor'
    [ , [ @pubversion = ] pubversion ]
    [ , [ @dump_cmds = ] dump_cmds ]
[ ; ]
```

## Arguments

#### [ @sub_table = ] N'*sub_table*'

The name of the Subscriber table. *@sub_table* is **sysname**, with no default.

#### [ @sub_table_owner = ] N'*sub_table_owner*'

The name of the owner of the Subscriber table. *@sub_table_owner* is **sysname**, with no default.

#### [ @publisher = ] N'*publisher*'

The name of the Publisher server. *@publisher* is **sysname**, with no default.

#### [ @publisher_db = ] N'*publisher_db*'

The name of the Publisher database. *@publisher_db* is **sysname**, with no default. If `NULL`, the current database is used.

#### [ @publication = ] N'*publication*'

The name of the publication. *@publication* is **sysname**, with no default.

#### [ @ins_proc = ] N'*ins_proc*'

The name of the stored procedure that supports synchronous transaction inserts at the Publisher. *@ins_proc* is **sysname**, with no default.

#### [ @upd_proc = ] N'*upd_proc*'

The name of the stored procedure that supports synchronous transaction updates at the Publisher. *@upd_proc* is **sysname**, with no default.

#### [ @del_proc = ] N'*del_proc*'

The name of the stored procedure that supports synchronous transaction deletes at the Publisher. *@del_proc* is **sysname**, with no default.

#### [ @cftproc = ] N'*cftproc*'

The name of the autogenerated procedure used by publications that allow queued updating. *@cftproc* is **sysname**, with no default. For publications that allow immediate updating, this value is `NULL`. This parameter applies to publications that allow queued updating (Queued Updating and Immediate Updating with Queued Updating as Failover).

#### [ @proc_owner = ] N'*proc_owner*'

Specifies the user account in the Publisher under which all the autogenerated stored procedures for updating publication (queued and/or immediate) were created. *@proc_owner* is **sysname**, with no default.

#### [ @identity_col = ] N'*identity_col*'

The name of the identity column at the Publisher. *@identity_col* is **sysname**, with a default of `NULL`.

#### [ @ts_col = ] N'*ts_col*'

The name of the **timestamp** column at the Publisher. *@ts_col* is **sysname**, with a default of `NULL`.

#### [ @filter_clause = ] N'*filter_clause*'

A restriction (WHERE) clause that defines a horizontal filter. When entering the restriction clause, omit the keyword WHERE. *@filter_clause* is **nvarchar(4000)**, with a default of `NULL`.

#### [ @primary_key_bitmap = ] *primary_key_bitmap*

A bit map of the primary key columns in the table. *@primary_key_bitmap* is **varbinary(4000)**, with no default.

#### [ @identity_support = ] *identity_support*

Enables and disables automatic identity range handling when queued updating is used. *@identity_support* is **bit**, with a default of `0`.

- `0` means that there's no identity range support.
- `1` enables automatic identity range handling.

#### [ @independent_agent = ] *independent_agent*

Indicates whether there's a single Distribution Agent (an independent agent) for this publication, or one Distribution Agent per publication database and subscription database pair (a shared agent). *@independent_agent* is **bit**, with a default of `0`. This value reflects the value of the `independent_agent` property of the publication defined at the Publisher.

- If `0`, the agent is a Shared Agent.
- If `1`, the agent is an independent agent.

#### [ @distributor = ] N'*distributor*'

The name of the Distributor. *@distributor* is **sysname**, with no default.

#### [ @pubversion = ] *pubversion*

Indicates the version of the Publisher. *@pubversion* is **int**, with a default of `1`.

- `1` means that the Publisher version is [!INCLUDE [ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 2 or earlier versions.
- `2` means that the Publisher is [!INCLUDE [ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 3 (SP 3) and later versions.

*@pubversion* must be explicitly set to `2` when the Publisher version is [!INCLUDE [ssVersion2000](../../includes/ssversion2000-md.md)] SP 3 and later versions.

#### [ @dump_cmds = ] *dump_cmds*

[!INCLUDE [ssinternalonly-md](../../includes/ssinternalonly-md.md)]

## Return code values

`0` (success) or `1` (failure).

## Remarks

`sp_addsynctriggers` is used by the Distribution Agent as part of subscription initialization. This stored procedure isn't commonly run by users, but might be useful if the user needs to set up a no-sync subscription manually.

## Permissions

Only members of the **sysadmin** fixed server role or **db_owner** fixed database role can execute `sp_addsynctriggers`.

## Related content

- [Updatable Subscriptions - For Transactional Replication](../replication/transactional/updatable-subscriptions-for-transactional-replication.md)
- [sp_script_synctran_commands (Transact-SQL)](sp-script-synctran-commands-transact-sql.md)
- [System stored procedures (Transact-SQL)](system-stored-procedures-transact-sql.md)