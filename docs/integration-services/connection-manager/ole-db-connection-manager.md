---
title: "OLEDB connection manager"
description: An OLEDB connection manager enables a package to connect to a data source by using an OLEDB provider.
author: chugugrace
ms.author: chugu
ms.date: "10/13/2023"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
f1_keywords:
  - "sql13.dts.designer.oledbconnection.f1"
helpviewer_keywords:
  - "OLEDB connection manager"
  - "data sources [Integration Services], connections"
  - "connection managers [Integration Services], OLEDB"
  - "connections [Integration Services], OLEDB"
---
# OLEDB connection manager

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


An OLEDB connection manager enables a package to connect to a data source by using an OLEDB provider. For example, an OLEDB connection manager that connects to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] can use the [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLEDB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
> [!NOTE]
>  The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 OLEDB provider doesn't support the new connection string key words (MultiSubnetFailover=True) for multi-subnet failover clustering. For more information, see the [SQL Server Release Notes](https://go.microsoft.com/fwlink/?LinkId=247824).    
> 
> [!NOTE]
>  If the data source is [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 or [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, the data source requires a different data provider than earlier versions of Excel or Access. For more information, see [Connect to an Excel Workbook](../load-data-to-from-excel-with-ssis.md) and [Connect to an Access Database](./integration-services-ssis-connections.md).    
    
Several [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tasks and data flow components use an OLEDB connection manager. For example, the OLEDB source and OLEDB destination use this connection manager to extract and load data. The Execute SQL task can use this connection manager to connect to a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database to run queries.    
    
You can also use the OLEDB connection manager to access OLEDB data sources in custom tasks written in unmanaged code that uses a language such as C++.    
    
When you add an OLEDB connection manager to a package, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] creates a connection manager that resolves to an OLEDB connection at runtime, sets the connection manager properties, and adds the connection manager to the **Connections** collection on the package.    
    
The `ConnectionManagerType` property of the connection manager is set to `OLEDB`.    
    
Configure the OLEDB connection manager in the following ways:    
    
-   Provide a specific connection string configured to meet the requirements of the selected provider.    
    
-   Depending on the provider, include the name of the data source to connect to.    
    
-   Provide security credentials as appropriate for the selected provider.    
    
-   Indicate whether the connection created from the connection manager is retained at runtime.    
    
[!INCLUDE [entra-id](../../includes/entra-id.md)]

## Log calls and troubleshoot connections    
 You can log the calls that the OLEDB connection manager makes to external data providers. You can then troubleshoot the connections that the OLEDB connection manager makes to external data sources. To log the calls that the OLEDB connection manager makes to external data providers, enable package logging, and select the **Diagnostic** event at the package level. For more information, see [Troubleshooting Tools for Package Execution](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).    
    
## Configure the OLEDB connection manager    
 You can set properties through [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, or programmatically. For more information about the properties that you can set in [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, see [Configure OLEDB Connection Manager](). For information about configuring a connection manager programmatically, see the documentation for **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** class in the Developer Guide.    
    
### Configure OLEDB connection manager

Use the **Configure OLEDB Connection Manager** dialog box to add a connection to a data source. This connection can be new, or a copy of an existing connection.  
  
> [!NOTE]  
>  If the data source is [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, the data source requires a different connection manager than earlier versions of Excel. For more information, see [Connect to an Excel Workbook](../load-data-to-from-excel-with-ssis.md).  
>   
>  If the data source is [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, the data source requires a different OLEDB provider than earlier versions of Access. For more information, see [Connect to an Access Database](./integration-services-ssis-connections.md).  
  
 To learn more about the OLEDB connection manager, see [OLEDB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
#### Options  
 **Data connections**  
 Select an existing OLEDB data connection from the list.  
  
 **Data connection properties**  
 View properties and values for the selected OLEDB data connection.  
  
 **New**  
 Create an OLEDB data connection by using the **Connection Manager** dialog box.  
  
 **Delete**  
 Select a data connection, and then delete it by selecting **Delete**.  
  
#### Managed identities for Azure resources authentication
When running SSIS packages on [Azure-SSIS integration runtime (IR) in Azure Data Factory (ADF)](/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), you can use Microsoft Entra authentication with [system-assigned or user-assigned managed identities for your ADF](/azure/data-factory/connector-azure-sql-database#managed-identity) to access your Azure SQL Database or SQL Managed Instance. Your Azure-SSIS IR can access and copy data from or to your database using this managed identity.

> [!NOTE]
> - When you authenticate with a user-assigned managed identity, the SSIS integration runtime needs to be enabled with the same identity. For more information, see [Enable Microsoft Entra authentication for Azure-SSIS integration runtime](/azure/data-factory/enable-aad-authentication-azure-ssis-ir).
>  
> - When you use Microsoft Entra authentication to access Azure SQL Database or Azure SQL Managed Instance, you might encounter a problem related to package execution failure or unexpected behavior change. For more information, see [Microsoft Entra features and limitations](/azure/sql-database/sql-database-aad-authentication#azure-ad-features-and-limitations).

To use Microsoft Entra authentication with the managed identity for your ADF to access Azure SQL Database server, follow these steps:

1. [Provision a Microsoft Entra administrator](/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server) for your logical server in Azure portal, if you haven't already done so. The Microsoft Entra administrator can be a Microsoft Entra user or group. If you assign a group as the admin, you can add your ADF's managed identity to the group and skip steps 2 and 3. The administrator has full access to your logical server for Azure SQL Database.

1. [Create a contained database user](/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities) for the managed identity of your ADF. Use SQL Server Management Studio (SSMS) to connect to the database with a Microsoft Entra user that has at least ALTER ANY USER permission. Run the following T-SQL statement: 

   ```sql
   CREATE USER [your managed identity name] FROM EXTERNAL PROVIDER;
   ```

   If you use the system-assigned managed identity for your ADF, then *your managed identity name* should be your ADF name. If you use a user-assigned managed identity for your ADF, then *your managed identity name* should be the specified user-assigned managed identity name.

1. Grant the managed identity for your ADF the required permissions, as you normally do for SQL users. Refer to [Database-level roles](../../relational-databases/security/authentication-access/database-level-roles.md) for appropriate roles. Run the following T-SQL statement. For more options, see [this article](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md).

   ```sql
   EXEC sp_addrolemember [role name], [your managed identity name];
   ```

To use Microsoft Entra authentication with the managed identity for your ADF to access Azure SQL Managed Instance, follow these steps:
    
1. [Provision a Microsoft Entra administrator](/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-managed-instance) for your Azure SQL Managed Instance in Azure portal, if you haven't already done so. The Microsoft Entra administrator can be a Microsoft Entra user or group. If you assign a group as the admin, you can add your ADF's managed identity to the group and skip steps 2 and 3. The administrator has full access to your Azure SQL Managed Instance.

1. [Create a login](../../t-sql/statements/create-login-transact-sql.md?view=azuresqldb-mi-current&preserve-view=true) assigned to the managed identity for your ADF. On SSMS, connect to your Azure SQL Managed Instance using SQL Server account that is a **sysadmin**. In `master` database, run the following T-SQL statement:

   ```sql
   CREATE LOGIN [your managed identity name] FROM EXTERNAL PROVIDER;
   ```

   If you use the system managed identity for your ADF, then *your managed identity name* should be your ADF name. If you use a user-assigned managed identity for your ADF, then *your managed identity name* should be the specified user-assigned managed identity name.

1. [Create a contained database user](/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities) representing the managed identity for your ADF. Connect to the database from or to which you want to copy data using SSMS and run the following T-SQL statement:
  
   ```sql
   CREATE USER [your managed identity name] FROM EXTERNAL PROVIDER;
   ```

1. Grant the managed identity for your ADF the required permissions, as you normally do for SQL users. Run the following T-SQL statement. For more options, see [this article](../../t-sql/statements/alter-role-transact-sql.md?view=azuresqldb-mi-current&preserve-view=true).

   ```sql
   ALTER ROLE [role name e.g., db_owner] ADD MEMBER [your managed identity name];
   ```

You can then configure the OLEDB provider on your OLEDB connection manager. Here are the options to do this:
    
- **Configure at design time.** In SSIS Designer, double-click on your OLEDB connection manager to open the **Connection Manager** window. In the **Provider** drop-down list, select [**Microsoft OLEDB Driver for SQL Server**](https://go.microsoft.com/fwlink/?linkid=871294).

  > [!NOTE]
  >  Other providers in the drop-down list might not support Microsoft Entra authentication with your ADF's managed identity.
    
- **Configure at run time.** When you run your package via [SSMS](../ssis-quickstart-run-ssms.md) or [Execute SSIS Package activity in ADF pipeline](/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), find the connection manager property **ConnectionString** for OLEDB connection manager. Update the connection property `Provider` to `MSOLEDBSQL` (that is Microsoft OLEDB Driver for SQL Server).

  ```vb
  Data Source=serverName;Initial Catalog=databaseName;Provider=MSOLEDBSQL;...
  ```

You can now configure Microsoft Entra authentication with the managed identity of your ADF on the OLEDB connection manager. Here are the options to do this:
    
- **Configure at design time.** In SSIS Designer, right-click on your OLEDB connection manager, and select **Properties**. Update the property `ConnectUsingManagedIdentity` to `True`.

  > [!NOTE]
  >  Currently, the connection manager property `ConnectUsingManagedIdentity` doesn't take effect when you run your package in SSIS Designer or on SQL Server, indicating that authentication with the managed identity of your ADF doesn't work.

- **Configure at run time.** When you run your package via [SSMS](../ssis-quickstart-run-ssms.md) or [Execute SSIS Package activity in ADF pipeline](/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), find the OLEDB connection manager and update its property `ConnectUsingManagedIdentity` to `True`.

  > [!NOTE]
  > On Azure-SSIS IR, all other authentication methods (for example, integrated security and password) preconfigured on your OLEDB connection manager are overridden when using Microsoft Entra authentication with a managed identity.

To configure Microsoft Entra authentication with the managed identity for your ADF on your existing packages, the preferred way is to rebuild your SSIS project with the [latest SSIS Designer](../../ssdt/download-sql-server-data-tools-ssdt.md) at least once. Redeploy your SSIS project to run on Azure-SSIS IR, so that the new connection manager property `ConnectUsingManagedIdentity` is automatically added to all OLEDB connection managers in your project. Alternatively, you can use property overrides, with the property path *\Package.Connections[{the name of your connection manager}].Properties[ConnectUsingManagedIdentity]* assigned to `True` at run time.

## See also
- [OLEDB Source](../../integration-services/data-flow/ole-db-source.md)
- [OLEDB Destination](../../integration-services/data-flow/ole-db-destination.md)
- [Integration Services (SSIS) Connections](../../integration-services/connection-manager/integration-services-ssis-connections.md)
