---
title: "CREATE EVENT SESSION (Transact-SQL)"
description: CREATE EVENT SESSION creates an Extended Events session that identifies the source of the events, the event session targets, and the event session options.
author: markingmyname
ms.author: maghan
ms.date: "05/15/2024"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "CREATE EVENT SESSION"
  - "SESSION"
  - "EVENT SESSION"
  - "SESSION_TSQL"
  - "EVENT_SESSION_TSQL"
  - "CREATE_EVENT_SESSION_TSQL"
helpviewer_keywords:
  - "event sessions [SQL Server]"
  - "CREATE EVENT SESSION statement"
dev_langs:
  - "TSQL"
---
# CREATE EVENT SESSION (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Creates an Extended Events session that identifies the source of the events, the event session targets, and the event session options.

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
CREATE EVENT SESSION event_session_name
ON { SERVER | DATABASE }
{  
    <event_definition> [ ,...n]
    [ <event_target_definition> [ ,...n] ]
    [ WITH ( <event_session_options> [ ,...n] ) ]
}
;

<event_definition>::=
{
    ADD EVENT [event_module_guid].event_package_name.event_name
         [ ( {
                 [ SET { event_customizable_attribute = <value> [ ,...n] } ]
                 [ ACTION ( { [event_module_guid].event_package_name.action_name [ ,...n] } ) ]
                 [ WHERE <predicate_expression> ]
        } ) ]
}

<predicate_expression> ::=
{
    [ NOT ] <predicate_factor> | {( <predicate_expression> ) }
    [ { AND | OR } [ NOT ] { <predicate_factor> | ( <predicate_expression> ) } ]
    [ ,...n ]
}  
  
<predicate_factor>::=
{
    <predicate_leaf> | ( <predicate_expression> )
}

<predicate_leaf>::=
{
      <predicate_source_declaration> { = | < > | ! = | > | > = | < | < = } <value>
    | [event_module_guid].event_package_name.predicate_compare_name ( <predicate_source_declaration>, <value> )
}

<predicate_source_declaration>::=
{
    event_field_name | ( [event_module_guid].event_package_name.predicate_source_name )
}

<value>::=
{
    number | 'string'
}

<event_target_definition>::=
{
    ADD TARGET [event_module_guid].event_package_name.target_name
        [ ( SET { target_parameter_name = <value> [ ,...n] } ) ]
}

<event_session_options>::=
{  
    [    MAX_MEMORY = size [ KB | MB ] ]
    [ [,] EVENT_RETENTION_MODE = { ALLOW_SINGLE_EVENT_LOSS | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS } ]
    [ [,] MAX_DISPATCH_LATENCY = { seconds SECONDS | INFINITE } ]
    [ [,] MAX_EVENT_SIZE = size [ KB | MB ] ]
    [ [,] MEMORY_PARTITION_MODE = { NONE | PER_NODE | PER_CPU } ]
    [ [,] TRACK_CAUSALITY = { ON | OFF } ]
    [ [,] STARTUP_STATE = { ON | OFF } ]
}
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments

#### *event_session_name*
Is the user-defined name for the event session. *event_session_name* is alphanumeric, can be up to 128 characters, must be unique within an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], and must comply with the rules for [Identifiers](../../relational-databases/databases/database-identifiers.md).

#### ADD EVENT [ *event_module_guid* ].*event_package_name*.*event_name*
Is the event to associate with the event session, where:

- *event_module_guid* is the GUID for the module that contains the event.
- *event_package_name* is the package that contains the action object.
- *event_name* is the event object.

Events appear in the `sys.dm_xe_objects` view as object_type 'event'.

#### SET { *event_customizable_attribute*= \<value> [ ,...*n*] }
Allows customizable attributes for the event to be set. Customizable attributes appear in the `sys.dm_xe_object_columns` view as column_type 'customizable ' and object_name = *event_name*.

#### ACTION ( { [*event_module_guid*].*event_package_name*.*action_name* [ **,**...*n*] })
Is the action to associate with the event session, where:

- *event_module_guid* is the GUID for the module that contains the event.
- *event_package_name* is the package that contains the action object.
- *action_name* is the action object.

Actions appear in the `sys.dm_xe_objects` view as object_type 'action'.

#### WHERE \<predicate_expression>
Specifies the predicate expression used to determine if an event should be processed. If \<predicate_expression> is true, the event is processed further by the actions and targets for the session. If \<predicate_expression> is false, the event is dropped, avoiding additional action and target processing. Predicate expressions are limited to 3,000 characters.

*event_field_name*
Is the name of the event field that identifies the predicate source.

[*event_module_guid*].*event_package_name*.*predicate_source_name*
Is the name of the global predicate source where:

- *event_module_guid* is the GUID for the module that contains the event.
- *event_package_name* is the package that contains the predicate object.
- *predicate_source_name* is defined in the `sys.dm_xe_objects` view as `object_type` 'pred_source'.

[*event_module_guid*].*event_package_name*.*predicate_compare_name*
Is the name of the predicate object to associate with the event, where:

- *event_module_guid* is the GUID for the module that contains the event.
- *event_package_name* is the package that contains the predicate object.
- *predicate_compare_name* is a global source defined in the `sys.dm_xe_objects` view as `object_type` 'pred_compare'.

*number*
Is any numeric type including **decimal**. Limitations are the lack of available physical memory or a number that is too large to be represented as a 64-bit integer.

'*string*'
Either an ANSI or Unicode string as required by the predicate compare. No implicit string type conversion is performed for the predicate compare functions. Passing the wrong type results in an error.

#### ADD TARGET [*event_module_guid*].*event_package_name*.*target_name*
Is the target to associate with the event session, where:

- *event_module_guid* is the GUID for the module that contains the event.
- *event_package_name* is the package that contains the action object.
- *target_name* is the target. Targets appear in `sys.dm_xe_objects` view as `object_type` 'target'.

#### SET { *target_parameter_name*= \<value> [, ...*n*] }
Sets a target parameter.

To see all target parameters and their descriptions, execute the following query, replacing the `target-name` placeholder with the target name, such as `event_file`, `ring_buffer`, `histogram`, etc.

```sql
SELECT name AS target_parameter_name,
       column_value AS default_value,
       description
FROM sys.dm_xe_object_columns
WHERE column_type = 'customizable'
      AND
      object_name = 'target-name';
```

> [!IMPORTANT]
> If you are using the ring buffer target, we recommend that you set the `MAX_MEMORY` *target* parameter (distinct from the `MAX_MEMORY` session parameter) to 1024 kilobytes (KB) or less to help avoid possible data truncation of the XML output.

For more information about target types, see [Targets for Extended Events in SQL Server](../../relational-databases/extended-events/targets-for-extended-events-in-sql-server.md).

#### WITH ( \<event_session_options> [ ,...*n*] )
Specifies options to use with the event session.

#### MAX_MEMORY =*size* [ KB | **MB** ]
Specifies the maximum amount of memory to allocate to the session for event buffering. The default is 4 MB. *size* is a whole number and can be a kilobyte (KB) or a megabyte (MB) value. The maximum amount can't exceed 2 GB (less than 2,048 MB). However, using memory values in GB range isn't recommended.

#### EVENT_RETENTION_MODE = { **ALLOW_SINGLE_EVENT_LOSS** | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS }
Specifies the event retention mode to use for handling event loss.

**ALLOW_SINGLE_EVENT_LOSS**
An event can be lost from the session. A single event is only dropped when all the event buffers are full. Losing a single event when event buffers are full allows for acceptable [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] performance characteristics, while minimizing the loss of data in the processed event stream.

ALLOW_MULTIPLE_EVENT_LOSS
Full event buffers containing multiple events can be lost from the session. The number of events lost is dependent upon the memory size allocated to the session, the partitioning of the memory, and the size of the events in the buffer. This option minimizes performance impact on the server when event buffers are quickly filled, but large numbers of events can be lost from the session.

NO_EVENT_LOSS
No event loss is allowed. This option ensures that all events raised are retained. Using this option forces all tasks that fire events to wait until space is available in an event buffer. Using NO_EVENT_LOSS can cause detectable performance issues while the event session is active. User connections may stall while waiting for events to be flushed from the buffer.

> [!NOTE]
> For the event file targets in Azure SQL Database and in Azure SQL Managed Instance with the always-up-to-date update policy, starting from June 2024, NO_EVENT_LOSS behaves the same as ALLOW_SINGLE_EVENT_LOSS. If you specify NO_EVENT_LOSS, a warning with message ID 25665, severity 10, and message *This target does not support the NO_EVENT_LOSS event retention mode. The ALLOW_SINGLE_EVENT_LOSS retention mode is used instead.* is returned, and the session is created.
>
> This change avoids connection timeouts, failover delays, and other issues that can reduce database availability when NO_EVENT_LOSS is used with event file targets in Azure blob storage.
>
> NO_EVENT_LOSS will be removed as a supported EVENT_RETENTION_MODE argument in future updates to Azure SQL Database and Azure SQL Managed Instance. Avoid using this feature in new development work, and plan to modify applications that currently use this feature.

#### MAX_DISPATCH_LATENCY = { *seconds* SECONDS | **INFINITE** }
Specifies the amount of time that events are buffered in memory before being dispatched to event session targets. By default, this value is set to 30 seconds.

*seconds* SECONDS
The time, in seconds, to wait before starting to flush buffers to targets. *seconds* is a whole number. The minimum latency value is 1 second. However, 0 can be used to specify INFINITE latency.

**INFINITE**
Flush buffers to targets only when the buffers are full, or when the event session closes.

> [!NOTE]
> MAX_DISPATCH_LATENCY = 0 SECONDS is equivalent to MAX_DISPATCH_LATENCY = INFINITE.

#### MAX_EVENT_SIZE =*size* [ KB | **MB** ]
Specifies the maximum allowable size for events. MAX_EVENT_SIZE should only be set to allow single events larger than MAX_MEMORY; setting it to less than MAX_MEMORY raises an error. *size* is a whole number and can be a kilobyte (KB) or a megabyte (MB) value. If *size* is specified in kilobytes, the minimum allowable size is 64 KB. When MAX_EVENT_SIZE is set, two buffers of *size* are created in addition to MAX_MEMORY, and the total memory used for event buffering is MAX_MEMORY + 2 * MAX_EVENT_SIZE.

#### MEMORY_PARTITION_MODE = { **NONE** | PER_NODE | PER_CPU }
Specifies the location where event buffers are created.

**NONE**
A single set of buffers are created within the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance.

PER_NODE
A set of buffers is created for each NUMA node.

PER_CPU
A set of buffers is created for each CPU.

#### TRACK_CAUSALITY = { ON | **OFF** }
Specifies whether or not causality is tracked. If enabled, causality allows related events on different server connections to be correlated together.

#### STARTUP_STATE = { ON | **OFF** }
Specifies whether or not to start this event session automatically when [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] starts.

> [!NOTE]
> If `STARTUP_STATE = ON`, the event session will only start if [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is stopped and then restarted.

ON
The event session is started at startup.

**OFF**
The event session isn't started at startup.

## Remarks

The order of precedence for the logical operators is `NOT` (highest), followed by `AND`, followed by `OR`.

## Permissions

On SQL Server and SQL Managed Instance, requires the `ALTER ANY EVENT SESSION` permission.
On SQL Database, requires the `ALTER ANY DATABASE EVENT SESSION` permission in the database.

## Examples

### SQL Server example

The following example shows how to create an event session named `test_session`. This example adds two events and uses the Event Tracing for Windows target.

```sql
IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='test_session')
    DROP EVENT session test_session ON SERVER;
GO
CREATE EVENT SESSION test_session
ON SERVER
    ADD EVENT sqlos.async_io_requested,
    ADD EVENT sqlserver.lock_acquired
    ADD TARGET package0.etw_classic_sync_target
        (SET default_etw_session_logfile_path = N'C:\demo\traces\sqletw.etl' )
    WITH (MAX_MEMORY=4MB, MAX_EVENT_SIZE=4MB);
GO
```

### Azure SQL example

In [!INCLUDE[ssazuremi-md](../../includes/ssazuremi-md.md)] or [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)], store .xel files in Azure Blob Storage. You can use `sys.fn_xe_file_target_read_file` to read from extended event sessions you create yourself and store in Azure Blob Storage. For example walkthrough, review [Event File target code for extended events in Azure SQL Database and Azure SQL Managed Instance](/azure/azure-sql/database/xevent-code-event-file).

### Code examples can differ for Azure SQL Database and SQL Managed Instance

[!INCLUDE[sql-on-premises-vs-azure-similar-sys-views-include.](../../includes/paragraph-content/sql-on-premises-vs-azure-similar-sys-views-include.md)]

## See also

- [sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)
- [sys.dm_xe_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)
- [sys.dm_xe_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)

## Next steps

- [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)
- [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)
