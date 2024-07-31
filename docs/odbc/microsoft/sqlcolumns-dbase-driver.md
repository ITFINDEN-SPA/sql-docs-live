---
title: "SQLColumns (dBASE Driver)"
description: "SQLColumns (dBASE Driver)"
author: David-Engel
ms.author: davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
helpviewer_keywords:
  - "SQLColumns function [ODBC], dBASE Driver"
  - "DBase driver [ODBC], SQLColumns"
---
# SQLColumns (dBASE Driver)
> [!NOTE]  
>  This topic provides dBASE Driver-specific information. For general information about this function, see the appropriate topic under [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Column|Comments|  
|------------|--------------|  
|TABLE_QUALIFIER|The path to a directory is returned.|  
|TABLE_OWNER|NULL is returned in this column because owner name is not supported.|  
|NULLABLE|SQL_NO_NULLS is returned for columns that participate in a primary key or unique index.|