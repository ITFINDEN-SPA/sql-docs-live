---
title: "XQueries Handling Relational Data"
description: "Learn how to bind non-XML relational data to XML by using the XQuery extensions sql:column() and sql:variable()."
author: "rothja"
ms.author: "jroth"
ms.date: "03/03/2017"
ms.service: sql
ms.subservice: xml
ms.topic: "language-reference"
helpviewer_keywords:
  - "relational data [XQuery]"
  - "XQuery, relational data"
dev_langs:
  - "XML"
---
# XQueries Handling Relational Data
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sqlserver.md)]

  You specify XQuery against an **xml** type column or variable by using one of the [XML Data Type Methods](../t-sql/xml/xml-data-type-methods.md). These include **query()**, **value()**, **exist()**, or **modify()**. The XQuery is executed against the XML instance identified in the query generating the XML.  
  
 The XML generated by the execution of an XQuery can include values retrieved from other Transact-SQL variable or rowset columns. To bind non-XML relational data to the resulting XML, SQL Server provides the following pseudo functions as XQuery extensions:  
  
-   **sql:column()** function  
  
-   **sql:variable()** function  
  
 You can use these XQuery extensions when specifying an XQuery in the **query()** method of the **xml** data type. As a result, the **query()** method can produce XML that combines data from XML and non-**xml** data types.  
  
 You can also use these functions when you use the **xml** data type methods **modify()**, **value()**, **query()**, and **exist()** to expose a relational value inside XML.  
  
 For more information, see [sql:column() function (XQuery)](../xquery/xquery-extension-functions-sql-column.md) and [sql:variable() function (XQuery)](../xquery/xquery-extension-functions-sql-variable.md).  
  
## See Also  
 [XML Data &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery Language Reference &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML Construction &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  