---
title: "Non-XML Format Files (SQL Server)"
description: SQL Server 2019 supports non-XML format files and XML format files for bulk exporting and importing. Find out about non-XML format files and their benefits.
author: rwestMSFT
ms.author: randolphwest
ms.date: 08/29/2022
ms.service: sql
ms.subservice: data-movement
ms.topic: conceptual
helpviewer_keywords:
  - "non-XML format files"
  - "format files [SQL Server], non-XML format files"
  - "bulk importing [SQL Server], format files"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Use Non-XML format files (SQL Server)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

In [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)], two types of format files are supported for bulk exporting and importing: *non-XML format files* and *XML format files*.

## <a id="Benefits"></a> Benefits of non-XML format files

- You can create a non-XML format file automatically by specifying the **format** option in a **bcp** command.

- When you specify an existing format file in a **bcp** command, the command uses the values that are recorded in the format file and does not prompt you for the file storage type, prefix length, field length, or field terminator.

- You can create a format file for a particular data type such as character data or native data.

- You can create a non-XML format file that contains interactively specified attributes for each data field. For more information, see [Specify Data Formats for Compatibility when Using bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).

> [!NOTE]  
>  XML format files offer several advantages over non-XML format files. For more information, see [XML Format Files &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md).

> [!NOTE]  
> This syntax, including bulk insert, is not supported in Azure Synapse Analytics. [!INCLUDE [Use ADF or PolyBase instead of Synapse Bulk Insert](includes/bulk-insert-synapse.md)]

## <a id="Structure"></a> Structure of Non-XML Format Files

A non-XML format file is a text file that has a specific structure. The non-XML format file contains information about the file storage type, prefix length, field length, and field terminator of every table column.

The following illustration illustrates the format-file fields for a sample non-XML format file.

:::image type="content" source="media/non-xml-format-files-sql-server/format-file-structure.gif" alt-text="Identifies the fields of a non-xml format file.":::

The **Version** and **Number of columns** fields occur one time only. Their meanings are described in the following table.

|Format-file field|Description|  
|------------------------|-----------------|  
|Version|Version number of the **bcp** utility:<br /><br /> 9.0 = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> 10.0 = [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)]<br /><br /> 11.0 = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br /><br /> 12.0 = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]<br /><br /> The version number is recognized only by **bcp**, not by [!INCLUDE[tsql](../../includes/tsql-md.md)].<br /><br /> <br /><br /> Note: The version of the **bcp** utility (Bcp.exe) used to read a format file must be the same as, or a later version than was used to create the format file. For example, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]**bcp** can read a version 10.0 format file, which is generated by [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)]**bcp**, but [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)]**bcp** cannot read a version 12.0 format file, which is generated by [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**bcp**.|  
|Number of columns|Number of fields in the data file. This number must be the same in all rows.|

The other format-file fields describe the data fields that are to be bulk imported or exported. Each data field requires a separate row in the format file. Every format-file row contains values for the format-file fields that are described in the following table.

|Format-file field|Description|
|------------------------|-----------------|
|**Host file field order**|A number that indicates the position of each field in the data file. The first field in the row is 1, and so on.|  
|**Host file data type**|Indicates the data type that is stored in a given field of the data file. With ASCII data files, use SQLCHAR; for native format data files, use default data types. For more information, see [Specify File Storage Type by Using bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md).|  
|**Prefix length**|Number of length prefix characters for the field. Valid prefix lengths are 0, 1, 2, 4, and 8. To avoid specifying the length prefix, set this to 0. A length prefix must be specified if the field contains NULL data values. For more information, see [Specify Prefix Length in Data Files by Using bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md).|  
|**Host file data length**|Maximum length, in bytes, of the data type stored in the particular field of the data file.<br /><br /> If you are creating a non-XML format file for a delimited text file, you can specify 0 for the host file data length of every data field. When a delimited text file having a prefix length of 0 and a terminator is imported, the field-length value is ignored, because the storage space used by the field equals the length of the data plus the terminator.<br /><br /> For more information, see [Specify Field Length by Using bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md).|  
|**Terminator**|Delimiter to separate the fields in a data file. Common terminators are comma (,), tab (\t), and end of line (\r\n). For more information, see [Specify Field and Row Terminators &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).|  
|**Server column order**|Order in which columns appear in the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] table. For example, if the fourth field in the data file maps to the sixth column in a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] table, the server column order for the fourth field is 6.<br /><br /> To prevent a column in the table from receiving any data from the data file, set the server column order value to `0`.|  
|**Server column name**|Name of the column copied from the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] table. The actual name of the field is not required, but the field in the format file must not be blank.|  
|**Column collation**|The collation used to store character and Unicode data in the data file.|

> [!NOTE]  
> You can modify a format file to let you bulk import from a data file in which the number or order of the fields are different from the number or order of table columns. For more information, see the [Related Tasks](#RelatedTasks) list.

## <a id="Examples"></a> Example of a non-XML format file

The following example shows a previously created non-XML format file (`myDepartmentIdentical-f-c.fmt`). This file describes a character-data field for every column in the `HumanResources.Department` table in the [!INCLUDE [sssampledbobject-md](../../includes/sssampledbobject-md.md)] sample database.

The generated format file, `myDepartmentIdentical-f-c.fmt`, contains the following information:

```output
12.0  
4  
1       SQLCHAR       0       7       "\t"     1     DepartmentID     ""  
2       SQLCHAR       0       100     "\t"     2     Name             SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     "\t"     3     GroupName        SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       24      "\r\n"   4     ModifiedDate     ""
```

> [!NOTE]  
>  For an illustration that shows the format-file fields in relation to this sample non-XML format file, see [Structure of Non-XML Format Files](#Structure).

## <a id="RelatedTasks"></a> Related tasks

- [Create a Format File &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)
- [Use a Format File to Bulk Import Data &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)
- [Use a Format File to Skip a Table Column &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)
- [Use a Format File to Skip a Data Field &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)
- [Use a Format File to Map Table Columns to Data-File Fields &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)

## Next steps

- [bcp Utility](../../tools/bcp-utility.md)
- [Create a Format File &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)
- [XML Format Files &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)
- [Format Files for Importing or Exporting Data &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  