---
title: "Create a format file with bcp (SQL Server)"
description: When you bulk import or export a SQL Server table, a format file allows writing data files with little editing or reading data files from other programs.
author: rwestMSFT
ms.author: randolphwest
ms.date: 11/23/2023
ms.service: sql
ms.subservice: data-movement
ms.topic: conceptual
helpviewer_keywords:
  - "format files [SQL Server], creating"
monikerRange: ">=aps-pdw-2016 || =azuresqldb-current || >=sql-server-2016 || >=sql-server-linux-2017 || =azuresqldb-mi-current"
---
# Create a format file with bcp (SQL Server)

[!INCLUDE [SQL Server Azure SQL Database Synapse Analytics PDW](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

This article describes how to use the [bcp utility](../../tools/bcp-utility.md) to create a format file for a particular table. The format file is based on the data-type option specified (`-n`, `-c`, `-w`, or `-N`) and the table or view delimiters.

When you bulk import into a [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] table or bulk export data from a table, you can use a format file as a flexible system for writing data files. Format files require little or no editing to comply with other data formats, or to read data files from other software programs.

## Limitations

The version of the **bcp** utility (`bcp.exe`) used to read a format file must be the same as, or later than the version used to create the format file. For example, [!INCLUDE [sssql16-md](../../includes/sssql16-md.md)] **bcp** can read a version 12.0 format file, which is generated by [!INCLUDE [sssql14-md](../../includes/sssql14-md.md)] **bcp**, but [!INCLUDE [sssql14-md](../../includes/sssql14-md.md)] **bcp** can't read a version 13.0 format file, which is generated by [!INCLUDE [sssql16-md](../../includes/sssql16-md.md)] **bcp**.

> [!NOTE]  
> This syntax, including bulk insert, isn't supported in Azure Synapse Analytics. [!INCLUDE [Use ADF or PolyBase instead of Synapse Bulk Insert](includes/bulk-insert-synapse.md)]

## Create format files

[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] support two types of format file: non-XML format and XML format. The non-XML format is the original format supported by earlier versions of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)].

Generally, XML and non-XML format files are interchangeable. However, we recommend that you use XML syntax for format files, because they provide several advantages over non-XML format files.

## [XML format file](#tab/xml)

[!INCLUDE [article-uses-adventureworks](../../includes/article-uses-adventureworks.md)] [!INCLUDE [ssSampleDBdesc](../../includes/sssampledbdesc-md.md)]

### Create an XML format file

To use a **bcp** command to create a format file, specify the `format` argument and use `nul` instead of a data-file path. The `format` option always requires the `-f` option, and to create an XML format file, you must also specify the `-x` option, such as `bcp <table_or_view> format nul -f <format_file_name> -x`.

To distinguish an XML format file, we recommend that you use `.xml` as the file name extension, for example, `MyTable.xml`.

For information about the structure and fields of XML format files, see [XML Format Files (SQL Server)](xml-format-files-sql-server.md).

### Examples

This section contains the following examples that show how to use **bcp** commands to create an XML format file. The `HumanResources.Department` table contains four columns: `DepartmentID`, `Name`, `GroupName`, and `ModifiedDate`.

#### A. Create an XML format file for character data

The following example creates an XML format file, `Department.xml`, for the `HumanResources.Department` table. The format file uses character data formats and a non-default field terminator (`,`). The contents of the generated format file are presented after the command.

The **bcp** command contains the following qualifiers.

| Qualifiers | Description |
| --- | --- |
| `format nul -x -f <format_file>` | Specifies the XML format file. |
| `-c` | Specifies character data. |
| `-t,` | Specifies a comma (`,`) as the field terminator.<br /><br />**Note:** If the data file uses the default field terminator (`\t`), the `-t` switch is unnecessary. |
| `-T` | Specifies that the **bcp** utility connects to [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] with a trusted connection using integrated security. If `-T` isn't specified, you must specify `-U` and `-P` to successfully sign in. |

At the Windows command prompt, enter the following `bcp` command:

```cmd
bcp AdventureWorks2022.HumanResources.Department format nul -c -x -f Department-c.xml -t, -T
```

The generated format file, `Department-c.xml`, contains the following XML elements:

```xml
<?xml version="1.0"?>
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
<RECORD>
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="24"/>
</RECORD>
<ROW>
  <COLUMN SOURCE="1" NAME="DepartmentID" xsi:type="SQLSMALLINT"/>
  <COLUMN SOURCE="2" NAME="Name" xsi:type="SQLNVARCHAR"/>
  <COLUMN SOURCE="3" NAME="GroupName" xsi:type="SQLNVARCHAR"/>
  <COLUMN SOURCE="4" NAME="ModifiedDate" xsi:type="SQLDATETIME"/>
</ROW>
</BCPFORMAT>
```

For information about the syntax of this format file, see [XML Format Files (SQL Server)](xml-format-files-sql-server.md). For information about character data, see [Use character format to import or export data (SQL Server)](use-character-format-to-import-or-export-data-sql-server.md).

#### B. Create an XML format file for native data

The following example creates an XML format file, `Department-n.xml`, for the `HumanResources.Department` table. The format file uses native data types. The contents of the generated format file are presented after the command.

The **bcp** command contains the following qualifiers.

| Qualifiers | Description |
| --- | --- |
| `format nul -x -f <format_file>` | Specifies the XML format file. |
| `-n` | Specifies native data types. |
| `-T` | Specifies that the **bcp** utility connects to [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] with a trusted connection using integrated security. If `-T` isn't specified, you must specify `-U` and `-P` to successfully sign in. |

At the Windows command prompt, enter the following `bcp` command:

```cmd
bcp AdventureWorks2022.HumanResources.Department format nul -x -f Department-n.xml -n -T
```

The generated format file, `Department-n.xml`, contains the following XML elements:

```xml
<?xml version="1.0"?>
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
<RECORD>
  <FIELD ID="1" xsi:type="NativeFixed" LENGTH="2"/>
  <FIELD ID="2" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="3" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="4" xsi:type="NativeFixed" LENGTH="8"/>
</RECORD>
<ROW>
  <COLUMN SOURCE="1" NAME="DepartmentID" xsi:type="SQLSMALLINT"/>
  <COLUMN SOURCE="2" NAME="Name" xsi:type="SQLNVARCHAR"/>
  <COLUMN SOURCE="3" NAME="GroupName" xsi:type="SQLNVARCHAR"/>
  <COLUMN SOURCE="4" NAME="ModifiedDate" xsi:type="SQLDATETIME"/>
</ROW>
</BCPFORMAT>
```

For information about the syntax of this format file, see [XML Format Files (SQL Server)](xml-format-files-sql-server.md). For information about how to use native data, see [Use native format to import or export data (SQL Server)](use-native-format-to-import-or-export-data-sql-server.md).

## [Non-XML format file](#tab/non-xml)

[!INCLUDE [article-uses-adventureworks](../../includes/article-uses-adventureworks.md)] [!INCLUDE [ssSampleDBdesc](../../includes/sssampledbdesc-md.md)]

### Create a non-XML format file

To use a **bcp** command to create a format file, specify the `format` argument and use `nul` instead of a data-file path. The `format` option also requires the `-f` option, such as: `bcp <table_or_view> format nul -f <format_file_name>`.

To distinguish a non-XML format file, we recommend that you use `.fmt` as the file name extension, for example, `MyTable.fmt`.

For information about the structure and fields of non-XML format files, see [Use non-XML format files (SQL Server)](non-xml-format-files-sql-server.md).

### Examples

This section contains the following examples that show how to use **bcp** commands to create a non-XML format file. The `HumanResources.Department` table contains four columns: `DepartmentID`, `Name`, `GroupName`, and `ModifiedDate`.

#### A. Create a non-XML format file for native data

The following example creates an XML format file, `Department-n.xml`, for the `HumanResources.Department` table. The format file uses native data types. The contents of the generated format file are presented after the command.

The **bcp** command contains the following qualifiers.

| Qualifiers | Description |
| --- | --- |
| `format nul -f <format_file>` | Specifies the non-XML format file. |
| `-n` | Specifies native data types. |
| `-T` | Specifies that the **bcp** utility connects to [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] with a trusted connection using integrated security. If `-T` isn't specified, you must specify `-U` and `-P` to successfully sign in. |

At the Windows command prompt, enter the following `bcp` command:

```cmd
bcp AdventureWorks2022.HumanResources.Department format nul -T -n -f Department-n.fmt
```

The generated format file, `Department-n.fmt`, contains the following information:

```output
12.0
4
1  SQLSMALLINT   0       2       ""   1     DepartmentID         ""
2  SQLNCHAR      2       100     ""   2     Name                 SQL_Latin1_General_CP1_CI_AS
3  SQLNCHAR      2       100     ""   3     GroupName            SQL_Latin1_General_CP1_CI_AS
4  SQLDATETIME   0       8       ""   4     ModifiedDate         ""
```

For more information, see [Use non-XML format files (SQL Server)](non-xml-format-files-sql-server.md).

#### B. Create a non-XML format file for character data

The following example creates an XML format file, `Department.fmt`, for the `HumanResources.Department` table. The format file uses character data formats and a non-default field terminator (`,`). The contents of the generated format file are presented after the command.

The **bcp** command contains the following qualifiers.

| Qualifiers | Description |
| --- | --- |
| `format nul -f <format_file>` | Specifies a non-XML format file. |
| `-c` | Specifies character data. |
| `-T` | Specifies that the **bcp** utility connects to [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] with a trusted connection using integrated security. If `-T` isn't specified, you must specify `-U` and `-P` to successfully sign in. |

At the Windows command prompt, enter the following `bcp` command:

```cmd
bcp AdventureWorks2022.HumanResources.Department format nul -c -f Department-c.fmt -T
```

The generated format file, `Department-c.fmt`, contains the following information:

```output
12.0
4
1  SQLCHAR       0       7       "\t"     1     DepartmentID            ""
2  SQLCHAR       0       100     "\t"     2     Name                    SQL_Latin1_General_CP1_CI_AS
3  SQLCHAR       0       100     "\t"     3     GroupName               SQL_Latin1_General_CP1_CI_AS
4  SQLCHAR       0       24      "\r\n"   4     ModifiedDate            ""
```

For more information, see [Use non-XML format files (SQL Server)](non-xml-format-files-sql-server.md).

#### C. Create a non-XML format file for Unicode native data

To create a non-XML format file for Unicode native data for the `HumanResources.Department` table, use the following command:

```cmd
bcp AdventureWorks2022.HumanResources.Department format nul -T -N -f Department-n.fmt
```

For more information about how to use Unicode native data, see [Use Unicode Native Format to Import or Export Data (SQL Server)](use-unicode-native-format-to-import-or-export-data-sql-server.md).

#### D. Create a non-XML format file for Unicode character data

To create a non-XML format file for Unicode character data for the `HumanResources.Department` table that uses default terminators, use the following command:

```cmd
bcp AdventureWorks2022.HumanResources.Department format nul -T -w -f Department-w.fmt
```

For more information about how to use Unicode character data, see [Use Unicode character format to import or export data (SQL Server)](use-unicode-character-format-to-import-or-export-data-sql-server.md).

#### F. Use a format file with the code page option

If you create a format file using **bcp** (that is, by using `bcp format`), information about the collation/code page is written in the format file.

The following example format file, for a table with five columns, includes the collation.

```output
13.0
5
1  SQLCHAR         0       0       "\t"             1     c_0          Cyrillic_General_CS_AS
2  SQLCHAR         0       0       "\t"             2     c_1          Cyrillic_General_CS_AS
3  SQLCHAR         0       3000    "\t"             3     c_2          Cyrillic_General_CS_AS
4  SQLCHAR         0       5       "\t"             4     c_3          ""
5  SQLCHAR         0       41      "!!!\r\r\n"      5     c_4          ""
```

If you try to import data into [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] using `bcp in -c -C65001 -f format_file` ..." or "`BULK INSERT`/`OPENROWSET` ... `FORMATFILE='format_file' CODEPAGE=65001` ...", information about the collation/code page has priority over 65001 option.

Therefore, if you generate a  format file, you must manually delete the collation info from the generated format file before you start importing data back into [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)].

The following example shows the format file without the collation info.

```output
13.0
5
1  SQLCHAR         0       0       "\t"             1     c_0              ""
2  SQLCHAR         0       0       "\t"             2     c_1              ""
3  SQLCHAR         0       3000    "\t"             3     c_2              ""
4  SQLCHAR         0       5       "\t"             4     c_3              ""
5  SQLCHAR         0       41      "!!!\r\r\n"      5     c_4              ""
```

---

## Map data fields to table columns

As created by **bcp**, a format file describes all the table columns in order. You can modify a format file to rearrange or omit table rows. You can customize a format file to a data file whose fields don't map directly to the table columns. For more information, see the following articles:

- [Use a format file to skip a table column (SQL Server)](use-a-format-file-to-skip-a-table-column-sql-server.md)
- [Use a format file to skip a data field (SQL Server)](use-a-format-file-to-skip-a-data-field-sql-server.md)
- [Use a format file to map table columns to data-file fields (SQL Server)](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)

## Related content

- [bcp Utility](../../tools/bcp-utility.md)
- [Use non-XML format files (SQL Server)](non-xml-format-files-sql-server.md)
- [XML Format Files (SQL Server)](xml-format-files-sql-server.md)