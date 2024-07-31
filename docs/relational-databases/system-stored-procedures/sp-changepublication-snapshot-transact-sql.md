---
title: "sp_changepublication_snapshot (Transact-SQL)"
description: sp_changepublication_snapshot Changes properties of the Snapshot Agent for the specified publication.
author: markingmyname
ms.author: maghan
ms.reviewer: randolphwest
ms.date: 07/05/2024
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_changepublication_snapshot_TSQL"
  - "sp_changepublication_snapshot"
helpviewer_keywords:
  - "sp_changepublication_snapshot"
dev_langs:
  - "TSQL"
---
# sp_changepublication_snapshot (Transact-SQL)

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

Changes properties of the Snapshot Agent for the specified publication. This stored procedure is executed at the Publisher on the publication database.

> [!IMPORTANT]  
> When you configure a Publisher with a remote Distributor, the values supplied for all parameters, including *@job_login* and *@job_password*, are sent to the Distributor as plain text. You should encrypt the connection between the Publisher and its remote Distributor before executing this stored procedure. For more information, see [Configure SQL Server Database Engine for encrypting connections](../../database-engine/configure-windows/configure-sql-server-encryption.md).

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
sp_changepublication_snapshot
    [ @publication = ] N'publication'
    [ , [ @frequency_type = ] frequency_type ]
    [ , [ @frequency_interval = ] frequency_interval ]
    [ , [ @frequency_subday = ] frequency_subday ]
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]
    [ , [ @active_start_date = ] active_start_date ]
    [ , [ @active_end_date = ] active_end_date ]
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]
    [ , [ @snapshot_job_name = ] N'snapshot_job_name' ]
    [ , [ @publisher_security_mode = ] publisher_security_mode ]
    [ , [ @publisher_login = ] N'publisher_login' ]
    [ , [ @publisher_password = ] N'publisher_password' ]
    [ , [ @job_login = ] N'job_login' ]
    [ , [ @job_password = ] N'job_password' ]
    [ , [ @publisher = ] N'publisher' ]
[ ; ]
```

## Arguments

#### [ @publication = ] N'*publication*'

The name of the publication. *@publication* is **sysname**, with no default.

#### [ @frequency_type = ] *frequency_type*

Specifies the frequency with which to schedule the agent. *@frequency_type* is **int**, and can be one of the following values.

| Value | Description |
| --- | --- |
| `1` | One time |
| `2` | On demand |
| `4` | Daily |
| `8` | Weekly |
| `16` | Monthly |
| `32` | Monthly relative |
| `64` | Autostart |
| `128` | Recurring |
| `NULL` (default) | |

#### [ @frequency_interval = ] *frequency_interval*

Specifies the days that the agent runs. *@frequency_interval* is **int**, and can be one of the following values.

| Value | Description |
| --- | --- |
| `1` | Sunday |
| `2` | Monday |
| `3` | Tuesday |
| `4` | Wednesday |
| `5` | Thursday |
| `6` | Friday |
| `7` | Saturday |
| `8` | Day |
| `9` | Weekdays |
| `10` | Weekend days |
| `NULL` (default) | |

#### [ @frequency_subday = ] *frequency_subday*

The units for *@freq_subday_interval*. *@frequency_subday* is **int**, and can be one of these values.

| Value | Description |
| --- | --- |
| `1` | Once |
| `2` | Second |
| `4` | Minute |
| `8` | Hour |
| `NULL` (default) | |

#### [ @frequency_subday_interval = ] *frequency_subday_interval*

The interval for *@frequency_subday*. *@frequency_subday_interval* is **int**, with a default of `NULL`.

#### [ @frequency_relative_interval = ] *frequency_relative_interval*

The date the Snapshot Agent runs. *@frequency_relative_interval* is **int**, with a default of `NULL`.

#### [ @frequency_recurrence_factor = ] *frequency_recurrence_factor*

The recurrence factor used by *@frequency_type*. *@frequency_recurrence_factor* is **int**, with a default of `NULL`.

#### [ @active_start_date = ] *active_start_date*

The date when the Snapshot Agent is first scheduled, formatted as `yyyyMMdd`. *@active_start_date* is **int**, with a default of `NULL`.

#### [ @active_end_date = ] *active_end_date*

The date when the Snapshot Agent stops being scheduled, formatted as `yyyyMMdd`. *@active_end_date* is **int**, with a default of `NULL`.

#### [ @active_start_time_of_day = ] *active_start_time_of_day*

The time of day when the Snapshot Agent is first scheduled, formatted as `HHmmss`. *@active_start_time_of_day* is **int**, with a default of `NULL`.

#### [ @active_end_time_of_day = ] *active_end_time_of_day*

The time of day when the Snapshot Agent stops being scheduled, formatted as `HHmmss`. *@active_end_time_of_day* is **int**, with a default of `NULL`.

#### [ @snapshot_job_name = ] N'*snapshot_job_name*'

The name of an existing Snapshot Agent job name if an existing job is being used. *@snapshot_job_name* is **nvarchar(100)**, with a default of `NULL`.

#### [ @publisher_security_mode = ] *publisher_security_mode*

The security mode used by the agent when connecting to the Publisher. *@publisher_security_mode* is **int**, with a default of `NULL`. A value of `0` must be specified for non-[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] Publishers.

- `0` specifies [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] authentication
- `1` specifies Windows authentication

> [!IMPORTANT]  
> [!INCLUDE [ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]

#### [ @publisher_login = ] N'*publisher_login*'

The login used when connecting to the Publisher. *@publisher_login* is **sysname**, with a default of `NULL`.

*@publisher_login* must be specified when *@publisher_security_mode* is `0`. If *@publisher_login* is `NULL` and *@publisher_security_mode* is `1`, then the Windows account specified in *@job_login* is used when connecting to the Publisher.

#### [ @publisher_password = ] N'*publisher_password*'

The password used when connecting to the Publisher. *@publisher_password* is **sysname**, with a default of `NULL`.

> [!IMPORTANT]  
> Don't use a blank password. Use a strong password. When possible, prompt users to enter security credentials at runtime. If you must store credentials in a script file, you must secure the file to prevent unauthorized access.

#### [ @job_login = ] N'*job_login*'

The login for the Windows account under which the agent runs. *@job_login* is **nvarchar(257)**, with a default of `NULL`. This Windows account is always used for agent connections to the Distributor. You must supply this parameter when creating a new Snapshot Agent job. This can't be changed for a non-[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] publisher.

#### [ @job_password = ] N'*job_password*'

The password for the Windows account under which the agent runs. *@job_password* is **sysname**, with a default of `NULL`. You must supply this parameter when creating a new Snapshot Agent job.

> [!IMPORTANT]  
> When possible, prompt users to enter security credentials at runtime. If you must store credentials in a script file, you must secure the file to prevent unauthorized access.

#### [ @publisher = ] N'*publisher*'

Specifies a non-[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] publisher. *@publisher* is **sysname**, with a default of `NULL`.

> [!NOTE]  
> *@publisher* shouldn't be used when creating a Snapshot Agent at a [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.

## Return code values

`0` (success) or `1` (failure).

## Remarks

`sp_changepublication_snapshot` is used in snapshot replication, transactional replication, and merge replication.

## Permissions

Only members of the **sysadmin** fixed server role or **db_owner** fixed database role can execute `sp_changepublication_snapshot`.

## Related content

- [View and Modify Publication Properties](../replication/publish/view-and-modify-publication-properties.md)
- [Change Publication and Article Properties](../replication/publish/change-publication-and-article-properties.md)
- [sp_addpublication_snapshot (Transact-SQL)](sp-addpublication-snapshot-transact-sql.md)
- [System stored procedures (Transact-SQL)](system-stored-procedures-transact-sql.md)