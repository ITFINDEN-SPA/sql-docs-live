---
title: "SET ANSI_PADDING (Transact-SQL)"
description: SET ANSI_PADDING controls the way the column stores values shorter than the defined size of the column.
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.reviewer: randolphwest
ms.date: 07/08/2024
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "ANSI_PADDING_TSQL"
  - "ANSI_PADDING"
  - "SET_ANSI_PADDING_TSQL"
  - "SET ANSI_PADDING"
helpviewer_keywords:
  - "data types [SQL Server], short values"
  - "ANSI_PADDING option"
  - "short values [SQL Server]"
  - "SET ANSI_PADDING statement"
  - "trailing blanks"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016 || =azure-sqldw-latest || >=sql-server-2016 || >=sql-server-linux-2017 || =azuresqldb-mi-current || =fabric"
---
# SET ANSI_PADDING (Transact-SQL)

[!INCLUDE [sql-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw-fabricse-fabricdw.md)]

Controls the way the column stores values shorter than the defined size of the column, and the way the column stores values that have trailing blanks in **char**, **varchar**, **binary**, and **varbinary** data.

> [!NOTE]  
> `SET ANSI_PADDING OFF`, and the `ANSI_PADDING OFF` database option, are deprecated. In [!INCLUDE [_ss2017](../../includes/sssql17-md.md)] and later versions, and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)] and [!INCLUDE [ssazuremi-md](../../includes/ssazuremi-md.md)], `ANSI_PADDING` is always set to `ON`. Deprecated features shouldn't be used in new applications. For more information, see [Deprecated Database Engine features in SQL Server 2017](../../database-engine/deprecated-database-engine-features-in-sql-server-2017.md#transact-sql-1).

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

Syntax for [!INCLUDE [ssnoversion-md.md](../../includes/ssnoversion-md.md)], [!INCLUDE [sssodfull-md.md](../../includes/sssodfull-md.md)], [!INCLUDE [fabric](../../includes/fabric.md)].

```syntaxsql
SET ANSI_PADDING { ON | OFF }
```

Syntax for [!INCLUDE [ssazuresynapse-md.md](../../includes/ssazuresynapse-md.md)] and [!INCLUDE [sspdw-md.md](../../includes/sspdw-md.md)].

```syntaxsql
SET ANSI_PADDING ON
```

[!INCLUDE [sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Remarks

Columns defined with **char**, **varchar**, **binary**, and **varbinary** data types have a defined size.

This setting affects only the definition of new columns. After the column is created, [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] stores the values based on the setting when the column was created. Existing columns aren't affected by a later change to this setting.

> [!NOTE]  
> `ANSI_PADDING` should always be set to `ON`.

The following table shows the effects of the `SET ANSI_PADDING` setting when values are inserted into columns with **char**, **varchar**, **binary**, and **varbinary** data types.

| Setting | char(*n*) NOT NULL or binary(*n*) NOT NULL | char(*n*) NULL or binary(*n*) NULL | varchar(*n*) or varbinary(*n*) |
| --- | --- | --- | --- |
| `ON` | Pad original value (with trailing blanks for **char** columns and with trailing zeros for **binary** columns) to the length of the column. | Follows same rules as for **char(***n***)** or **binary(***n***)** `NOT NULL` when `SET ANSI_PADDING` is `ON`. | Trailing blanks in character values inserted into **varchar** columns aren't trimmed. Trailing zeros in binary values inserted into **varbinary** columns aren't trimmed. Values aren't padded to the length of the column. |
| `OFF` | Pad original value (with trailing blanks for **char** columns and with trailing zeros for **binary** columns) to the length of the column. | Follows same rules as for **varchar** or **varbinary** when `SET ANSI_PADDING` is `OFF`. | Trailing blanks in character values inserted into a **varchar** column are trimmed. Trailing zeros in binary values inserted into a **varbinary** column are trimmed. |

When padded, **char** columns are padded with blanks, and **binary** columns are padded with zeros. When trimmed, **char** columns have the trailing blanks trimmed, and **binary** columns have the trailing zeros trimmed.

`ANSI_PADDING` must be `ON` when you're creating or changing indexes on computed columns or indexed views. For more information about required SET option settings with indexed views and indexes on computed columns, see [Considerations when you use the SET statements](set-statements-transact-sql.md#considerations-when-you-use-the-set-statements).

The default for `SET ANSI_PADDING` is `ON`. The [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC driver and [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider for [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] automatically set `ANSI_PADDING` to `ON` when connecting. This can be configured in ODBC data sources, in ODBC connection attributes, or OLE DB connection properties set in the application before connecting. The default for `SET ANSI_PADDING` is `OFF` for connections from DB-Library applications.

The `SET ANSI_PADDING` setting doesn't affect the **nchar**, **nvarchar**, **ntext**, **text**, **image**, **varbinary(max)**, **varchar(max)**, and **nvarchar(max)** data types. They always display the `SET ANSI_PADDING ON` behavior. This means trailing spaces and zeros aren't trimmed.

When `ANSI_DEFAULTS` is `ON`, `ANSI_PADDING` is enabled.

The setting of `ANSI_PADDING` is defined at execute or run time and not at parse time.

To view the current setting for this setting, run the following query.

```sql
DECLARE @ANSI_PADDING VARCHAR(3) = 'OFF';
IF ( (16 & @@OPTIONS) = 16 ) SET @ANSI_PADDING = 'ON';
SELECT @ANSI_PADDING AS ANSI_PADDING;
```

## Permissions

Requires membership in the **public** role.

## Examples

The following example shows how the setting affects each of these data types.

Set `ANSI_PADDING` to `ON` and test.

```sql
PRINT 'Testing with ANSI_PADDING ON'
SET ANSI_PADDING ON;
GO

CREATE TABLE t1 (
   charcol CHAR(16) NULL,
   varcharcol VARCHAR(16) NULL,
   varbinarycol VARBINARY(8)
);
GO
INSERT INTO t1 VALUES ('No blanks', 'No blanks', 0x00ee);
INSERT INTO t1 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);

SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '\<',
   varbinarycol
FROM t1;
GO
```

Now set `ANSI_PADDING` to `OFF` and test.

```sql
PRINT 'Testing with ANSI_PADDING OFF';
SET ANSI_PADDING OFF;
GO

CREATE TABLE t2 (
   charcol CHAR(16) NULL,
   varcharcol VARCHAR(16) NULL,
   varbinarycol VARBINARY(8)
);
GO
INSERT INTO t2 VALUES ('No blanks', 'No blanks', 0x00ee);
INSERT INTO t2 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);

SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '<',
   varbinarycol
FROM t2;
GO

DROP TABLE t1;
DROP TABLE t2;
```

## Related content

- [SET Statements (Transact-SQL)](set-statements-transact-sql.md)
- [SESSIONPROPERTY (Transact-SQL)](../functions/sessionproperty-transact-sql.md)
- [CREATE TABLE (Transact-SQL)](create-table-transact-sql.md)
- [INSERT (Transact-SQL)](insert-transact-sql.md)
- [SET ANSI_DEFAULTS (Transact-SQL)](set-ansi-defaults-transact-sql.md)
