---
title: CREATE SERVER AUDIT (Transact-SQL)
description: Creates a server audit object using SQL Server Audit.
author: sravanisaluru
ms.author: srsaluru
ms.reviewer: randolphwest
ms.date: 11/14/2023
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "CREATE_SERVER_AUDIT_TSQL"
  - "SERVER AUDIT"
  - "SERVER_AUDIT_TSQL"
  - "CREATE SERVER AUDIT"
helpviewer_keywords:
  - "server audit [SQL Server]"
  - "CREATE SERVER AUDIT statement"
  - "audits [SQL Server], creating"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-mi-current || >=sql-server-2016 || >=sql-server-linux-2017"
---

# CREATE SERVER AUDIT (Transact-SQL)

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

Creates a server audit object using [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] Audit. For more information, see [SQL Server Audit (Database Engine)](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
CREATE SERVER AUDIT audit_name
{
    TO { [ FILE (<file_options> [ , ...n ] ) ] | APPLICATION_LOG | SECURITY_LOG | URL | EXTERNAL_MONITOR }
    [ WITH ( <audit_options> [ , ...n ] ) ]
    [ WHERE <predicate_expression> ]
}
[ ; ]

<file_options>::=
{
    FILEPATH = 'os_file_path'
    [ , MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED } ]
    [ , { MAX_ROLLOVER_FILES = { integer | UNLIMITED } } | { MAX_FILES = integer } ]
    [ , RESERVE_DISK_SPACE = { ON | OFF } ]
}

<audit_options> ::=
{
    [ QUEUE_DELAY = integer ]
    [ , ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION } ]
    [ , AUDIT_GUID = uniqueidentifier ]
    [ , OPERATOR_AUDIT = { ON | OFF } ]
}

<predicate_expression> ::=
{
    [ NOT ] <predicate_factor>
    [ { AND | OR } [ NOT ] { <predicate_factor> } ]
    [ , ...n ]
}

<predicate_factor>::=
    event_field_name { = | < > | != | > | >= | < | <= | LIKE } { number | ' string ' }
```

[!INCLUDE [sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments

#### TO { FILE | APPLICATION_LOG | SECURITY_LOG | URL | EXTERNAL_MONITOR }

Determines the location of the audit target. The options are a binary file, The Windows Application log, or the Windows Security log. [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] can't write to the Windows Security log without configuring additional settings in Windows. For more information, see [Write SQL Server Audit events to the Security log](../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md).

The `URL` target isn't supported for [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)].

> [!IMPORTANT]  
> In [!INCLUDE [ssazuremi-md](../../includes/ssazuremi-md.md)], SQL Audit works at the server level. Locations can only be `URL` or `EXTERNAL_MONITOR`.

#### FILEPATH = '*os_file_path*'

The path of the audit log. The file name is generated based on the audit name and audit GUID. If this path is invalid, the audit isn't created.

`FILEPATH` target isn't supported for [!INCLUDE [ssazuremi-md](../../includes/ssazuremi-md.md)]. You need to use `PATH` instead.

#### MAXSIZE = *max_size*

Specifies the maximum size to which the audit file can grow. The *max_size* value must be an integer followed by MB, GB, TB, or `UNLIMITED`. The minimum size that you can specify for *max_size* is 2 MB and the maximum is 2,147,483,647 TB. When `UNLIMITED` is specified, the file grows until the disk is full. (`0` also indicates `UNLIMITED`.) Specifying a value lower than 2 MB raises the error `MSG_MAXSIZE_TOO_SMALL`. The default value is `UNLIMITED`.

`MAXSIZE` target isn't supported for [!INCLUDE [ssazuremi-md](../../includes/ssazuremi-md.md)].

#### MAX_ROLLOVER_FILES = { *integer* | UNLIMITED }

Specifies the maximum number of files to retain in the file system in addition to the current file. The `MAX_ROLLOVER_FILES` value must be an integer or `UNLIMITED`. The default value is `UNLIMITED`. This parameter is evaluated whenever the audit restarts (which can happen when the instance of the [!INCLUDE [ssDE](../../includes/ssde-md.md)] restarts or when the audit is turned off and then on again) or when a new file is needed because the `MAXSIZE` is reached. When `MAX_ROLLOVER_FILES` is evaluated, if the number of files exceeds the `MAX_ROLLOVER_FILES` setting, the oldest file is deleted. As a result, when the setting of `MAX_ROLLOVER_FILES` is 0 a new file is created each time the `MAX_ROLLOVER_FILES` setting is evaluated. Only one file is automatically deleted when `MAX_ROLLOVER_FILES` setting is evaluated, so when the value of `MAX_ROLLOVER_FILES` is decreased, the number of files doesn't shrink unless old files are manually deleted. The maximum number of files that can be specified is 2,147,483,647.  

`MAX_ROLLOVER_FILES` isn't supported for [!INCLUDE [ssazuremi-md](../../includes/ssazuremi-md.md)].

#### MAX_FILES = *integer*

**Applies to**: [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] and later.

Specifies the maximum number of audit files that can be created. Doesn't roll over to the first file when the limit is reached. When the `MAX_FILES` limit is reached, any action that causes additional audit events to be generated, fails with an error.

#### RESERVE_DISK_SPACE = { ON | OFF }

This option preallocates the file on the disk to the `MAXSIZE` value. It applies only if `MAXSIZE` isn't equal to `UNLIMITED`. The default value is `OFF`.

`RESERVE_DISK_SPACE` target isn't supported for [!INCLUDE [ssazuremi-md](../../includes/ssazuremi-md.md)].

#### QUEUE_DELAY = *integer*

Determines the time, in milliseconds, that can elapse before audit actions are forced to be processed. A value of 0 indicates synchronous delivery. The minimum settable query delay value is `1000` (1 second), which is the default. The maximum is `2147483647` (2,147,483.647 seconds or 24 days, 20 hours, 31 minutes, 23.647 seconds). Specifying an invalid number raises the `MSG_INVALID_QUEUE_DELAY` error.

#### ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION }

Indicates whether the instance writing to the target should fail, continue, or stop [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] if the target can't write to the audit log. The default value is `CONTINUE`.

#### CONTINUE

[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] operations continue. Audit records aren't retained. The audit continues to attempt to log events and resumes if the failure condition is resolved. Selecting the continue option can allow unaudited activity, which could violate your security policies. Use this option, when continuing operation of the [!INCLUDE [ssDE](../../includes/ssde-md.md)] is more important than maintaining a complete audit.

#### SHUTDOWN

Forces the instance of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] to shut down, if [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] fails to write data to the audit target for any reason. The login executing the `CREATE SERVER AUDIT` statement must have the `SHUTDOWN` permission within [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]. The shutdown behavior persists even if the `SHUTDOWN` permission is later revoked from the executing login. If the user doesn't have this permission, then the statement fails and the audit isn't be created. Use the option when an audit failure could compromise the security or integrity of the system. For more information, see [SHUTDOWN](../../t-sql/language-elements/shutdown-transact-sql.md).

#### FAIL_OPERATION

**Applies to**: [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] and later.

Database actions fail if they cause audited events. Actions, which don't cause audited events can continue, but no audited events can occur. The audit continues to attempt to log events and resumes if the failure condition is resolved. Use this option when maintaining a complete audit is more important than full access to the [!INCLUDE [ssDE](../../includes/ssde-md.md)].

#### AUDIT_GUID = *uniqueidentifier*

To support scenarios such as database mirroring, an audit needs a specific GUID that matches the GUID found in the mirrored database. The GUID can't be modified after the audit is created.

#### OPERATOR_AUDIT

**Applies to:** [!INCLUDE [ssazuremi-md](../../includes/ssazuremi-md.md)] only.

Indicates whether auditing captures Microsoft support engineer operations when they need to access your server during a support request.

#### predicate_expression

**Applies to**: [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] and later versions.

Specifies the predicate expression used to determine if an event should be processed or not. Predicate expressions are limited to 3,000 characters, which limits string arguments.

#### event_field_name

**Applies to**: [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] and later versions.

The name of the event field that identifies the predicate source. Audit fields are described in [sys.fn_get_audit_file (Transact-SQL)](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md). All fields can be filtered except `file_name`, `audit_file_offset`, and `event_time`.

> [!NOTE]  
> While the `action_id` and `class_type` fields are of type **varchar** in `sys.fn_get_audit_file`, they can only be used with numbers when they are a predicate source for filtering. To get the list of values to be used with `class_type`, execute the following query:  

> ```sql
> SELECT spt.[name], spt.[number]
> FROM   [master].[dbo].[spt_values] spt
> WHERE  spt.[type] = N'EOD'
> ORDER BY spt.[name];
> ```

#### number

**Applies to**: [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] and later versions.

Any numeric type including **decimal**. Limitations are the lack of available physical memory or a number that is too large to be represented as a 64-bit integer.

#### '*string*'

**Applies to**: [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] and later versions.

Either an ANSI or Unicode string as required by the predicate compare. No implicit string type conversion is performed for the predicate compare functions. Passing the wrong type results in an error.

## Remarks

When a server audit is created, it's in a disabled state.

The `CREATE SERVER AUDIT` statement is in a transaction's scope. If the transaction is rolled back, the statement is also rolled back.

## Permissions

To create, alter, or drop a server audit, principals require the `ALTER ANY SERVER AUDIT` or the `CONTROL SERVER` permission.

When you're saving audit information to a file, to help prevent tampering, restrict access to the file location.

## Examples

### A. Create a server audit with a file target

The following example creates a server audit called `HIPAA_Audit` with a binary file as the target and no options.

```sql
CREATE SERVER AUDIT HIPAA_Audit
    TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );
```

### B. Create a server audit with a Windows Application log target with options

The following example creates a server audit called `HIPAA_Audit` with the target set for the Windows Application log. The queue is written every second and shuts down the [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] engine on failure.

```sql
CREATE SERVER AUDIT HIPAA_Audit
    TO APPLICATION_LOG
    WITH ( QUEUE_DELAY = 1000,  ON_FAILURE = SHUTDOWN);
```

### <a id="ExampleWhere"></a> C. Create a server audit containing a WHERE clause

The following example creates a database, schema, and two tables for the example. The table named `DataSchema.SensitiveData` contains confidential data and access to the table must be recorded in the audit. The table named `DataSchema.GeneralData` doesn't contain confidential data. The database audit specification audits access to all objects in the `DataSchema` schema. The server audit is created with a WHERE clause that limits the server audit to only the `SensitiveData` table. The server audit presumes an audit folder exists at `C:\SQLAudit`.

```sql
CREATE DATABASE TestDB;
GO
USE TestDB;
GO
CREATE SCHEMA DataSchema;
GO
CREATE TABLE DataSchema.GeneralData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);
GO
CREATE TABLE DataSchema.SensitiveData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);
GO
-- Create the server audit in the master database
USE master;
GO
CREATE SERVER AUDIT AuditDataAccess
    TO FILE ( FILEPATH ='C:\SQLAudit\' )
    WHERE object_name = 'SensitiveData' ;
GO
ALTER SERVER AUDIT AuditDataAccess WITH (STATE = ON);
GO
-- Create the database audit specification in the TestDB database
USE TestDB;
GO
CREATE DATABASE AUDIT SPECIFICATION [FilterForSensitiveData]
FOR SERVER AUDIT [AuditDataAccess]
ADD (SELECT ON SCHEMA::[DataSchema] BY [public])
WITH (STATE = ON);
GO
-- Trigger the audit event by selecting from tables
SELECT ID, DataField FROM DataSchema.GeneralData;
SELECT ID, DataField FROM DataSchema.SensitiveData;
GO
-- Check the audit for the filtered content
SELECT * FROM fn_get_audit_file('C:\SQLAudit\AuditDataAccess_*.sqlaudit',default,default);
GO
```

## Related content

- [ALTER SERVER AUDIT  (Transact-SQL)](alter-server-audit-transact-sql.md)
- [DROP SERVER AUDIT  (Transact-SQL)](drop-server-audit-transact-sql.md)
- [CREATE SERVER AUDIT SPECIFICATION (Transact-SQL)](create-server-audit-specification-transact-sql.md)
- [ALTER SERVER AUDIT SPECIFICATION (Transact-SQL)](alter-server-audit-specification-transact-sql.md)
- [DROP SERVER AUDIT SPECIFICATION (Transact-SQL)](drop-server-audit-specification-transact-sql.md)
- [CREATE DATABASE AUDIT SPECIFICATION (Transact-SQL)](create-database-audit-specification-transact-sql.md)
- [ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL)](alter-database-audit-specification-transact-sql.md)
- [DROP DATABASE AUDIT SPECIFICATION (Transact-SQL)](drop-database-audit-specification-transact-sql.md)
- [ALTER AUTHORIZATION (Transact-SQL)](alter-authorization-transact-sql.md)
- [sys.fn_get_audit_file (Transact-SQL)](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)
- [sys.server_audits (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)
- [sys.server_file_audits (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)
- [sys.server_audit_specifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)
- [sys.server_audit_specification_details (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)
- [sys.database_audit_specifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)
- [sys.database_audit_specification_details (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)
- [sys.dm_server_audit_status (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)
- [sys.dm_audit_actions (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)
- [sys.dm_audit_class_type_map (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)
- [Create a Server Audit and Server Audit Specification](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)