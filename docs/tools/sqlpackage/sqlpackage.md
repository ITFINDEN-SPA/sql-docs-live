---
title: SqlPackage
description: Learn how to automate database development tasks with SqlPackage. View examples and available parameters, properties, and SQLCMD variables.
author: "dzsquared"
ms.author: "drskwier"
ms.reviewer: "maghan"
ms.date: 4/29/2024
ms.service: sql
ms.subservice: tools-other
ms.topic: conceptual
---

# SqlPackage

**SqlPackage** is a command-line utility that automates the database development tasks by exposing some of the public Data-Tier Application Framework (DacFx) APIs.  The primary use cases for SqlPackage focus on database portability and deployments for the SQL Server, Azure SQL, and Azure Synapse Analytics family of databases. SqlPackage can be automated using [Azure Pipelines and GitHub actions](sqlpackage-pipelines.md) or other CI/CD tools.

**[Download the latest version](sqlpackage-download.md)**. For details about the latest release, see the [release notes](release-notes-sqlpackage.md).

[!INCLUDE [entra-id](../../includes/entra-id-hard-coded.md)]

## Portability

Database portability is the ability to move a database schema and data between different instances of SQL Server, Azure SQL, and Azure Synapse Analytics. Exporting a database from Azure SQL Database to an on-premises SQL Server instance, or from SQL Server to Azure SQL Database, are examples of database portability. SqlPackage supports database portability through the [Export](sqlpackage-export.md) and [Import](sqlpackage-import.md) actions, which create and consume BACPAC files. SqlPackage also supports database portability through the [Extract](sqlpackage-extract.md) and [Publish](sqlpackage-publish.md) actions, which create and consume DACPAC files, which can either contain the data directly or reference [data stored in Azure Blob Storage](sqlpackage-with-data-in-parquet-files.md).

- [Export](sqlpackage-export.md): Exports a connected SQL database - including database schema and user data - to a BACPAC file (.bacpac). 
  
- [Import](sqlpackage-import.md): Imports the schema and table data from a BACPAC file into a new user database. 

## Deployments

Database deployments are the process of updating a database schema to match a desired state, such as adding columns to a table or changing the contents of a stored procedure. SqlPackage supports database deployments through the [Publish](sqlpackage-publish.md) and [Extract](sqlpackage-extract.md) actions. The Publish action updates a database schema to match the contents of a source .dacpac file, while the Extract action creates a data-tier application (.dacpac) file containing the schema or schema and user data from a connected SQL database. SqlPackage enables deployments against both new or existing databases from the same artifact (.dacpac) by automatically creating a deployment plan that will apply the necessary changes to the target database.  The deployment plan can be reviewed before applying the changes to the target database with either the [Script](sqlpackage-script.md) or [DeployReport](sqlpackage-deploy-drift-report.md) actions.

- [Extract](sqlpackage-extract.md): Creates a data-tier application (.dacpac) file containing the schema or schema and user data from a connected SQL database. 
  
- [Publish](sqlpackage-publish.md): Incrementally updates a database schema to match the schema of a source .dacpac file. If the database doesn't exist on the server, the publish operation creates it. Otherwise, an existing database is updated. 
  
- [DeployReport](sqlpackage-deploy-drift-report.md): Creates an XML report representing the changes that a publish action would take. 
  
- [DriftReport](sqlpackage-deploy-drift-report.md): Creates an XML report representing the changes applied to a registered database since it was last registered. 
  
- [Script](sqlpackage-script.md): Creates a Transact-SQL incremental update script that updates the schema of a target to match the schema of a source. 

## Command-Line Syntax

**SqlPackage** initiates the actions specified using the [parameters](cli-reference.md#parameters), [properties](cli-reference.md#properties), and SQLCMD variables specified on the command line. 
  
```bash
SqlPackage {parameters} {properties} {SQLCMD variables}
```
More information on the SqlPackage command-line syntax is detailed in the [SqlPackage CLI reference](cli-reference.md) and individual action pages.

## Utility commands

### Version

Displays the sqlpackage version as a build number. Can be used in interactive prompts and in [automated pipelines](sqlpackage-pipelines.md).

```bash
SqlPackage /Version
```

### Help

You can display SqlPackage usage information by using `/?` or `/help:True`.

```bash
SqlPackage /?
```

For parameter and property information specific to a particular action, use the help parameter in addition to that action's parameter.

```bash
SqlPackage /Action:Publish /?
```

## Authentication

SqlPackage authenticates using methods available in [SqlClient](/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring). Configuring the authentication type can be accomplished via the connection string parameters for each SqlPackage action (`/SourceConnectionString` and `/TargetConnectionString`) or through individual parameters for connection properties. The following authentication methods are supported in a connection string:

- SQL Server authentication
- Active Directory (Windows) authentication
- [Microsoft Entra authentication](/azure/azure-sql/database/authentication-aad-overview)
    - Username/password
    - Integrated authentication
    - Universal authentication
    - **Managed identity**
    - Service principal


### Managed identity

[!INCLUDE [entra-id](../../includes/entra-id.md)]

In automated environments, [Microsoft Entra managed identity](/azure/azure-sql/database/authentication-azure-ad-user-assigned-managed-identity) is the recommended authentication method. This method doesn't require passing credentials to SqlPackage at runtime as SqlPackage uses managed identities to connect to databases that support Microsoft Entra authentication, and to obtain Microsoft Entra tokens, without credentials management. When the managed identity is configured for the environment where the SqlPackage action is run, the SqlPackage action can use that identity to authenticate to Azure SQL. For more information on configuring a managed identity for your environment, see the [Managed identity documentation](/entra/architecture/service-accounts-managed-identities).

An example connection string using system-assigned managed identity is:

```bash
Server=sampleserver.database.windows.net; Authentication=Active Directory Managed Identity; Database=sampledatabase;
```

Managed identities are supported in both [Azure DevOps](/azure/devops/integrate/get-started/authentication/service-principal-managed-identity) and [GitHub actions](https://github.com/azure/login) CI/CD pipelines.

### Service principal

[!INCLUDE [entra-id](../../includes/entra-id.md)]

[Microsoft Entra application service principals](/azure/azure-sql/database/authentication-aad-service-principal) are security objects within a Microsoft Entra application that define what an application can do in a given tenant. They're set up in the Azure portal during the application registration process and configured to access Azure resources, like Azure SQL. For more information on configuring a service principal for your environment, see the [Service principal documentation](/entra/architecture/service-accounts-principal).

When using SqlPackage with a service principal, it may be required to retrieve the access token and pass it to SqlPackage. The access token can be retrieved using the [Azure PowerShell module](/powershell/azure) or the [Azure CLI](/cli/azure). The access token can be passed to SqlPackage using the `/at` parameter.

```powershell
# example export connecting using an access token associated with a service principal
$Account = Connect-AzAccount -ServicePrincipal -Tenant $Tenant -Credential $Credential
$AccessToken_Object = (Get-AzAccessToken -Account $Account -ResourceUrl "https://database.windows.net/")
$AccessToken = $AccessToken_Object.Token

SqlPackage /at:$AccessToken /Action:Export /TargetFile:"C:\AdventureWorksLT.bacpac" \
    /SourceConnectionString:"Server=tcp:{yourserver}.database.windows.net,1433;Initial Catalog=AdventureWorksLT;MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;"
# OR
SqlPackage /at:$($AccessToken_Object.Token) /Action:Export /TargetFile:"C:\AdventureWorksLT.bacpac" \
    /SourceConnectionString:"Server=tcp:{yourserver}.database.windows.net,1433;Initial Catalog=AdventureWorksLT;MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;"
```

Service principals are supported in both [Azure DevOps](/azure/devops/integrate/get-started/authentication/service-principal-managed-identity) and [GitHub actions](https://github.com/azure/login) CI/CD pipelines.

## Environment variables

### Connection pooling

Connection pooling can be enabled for all connections made by SqlPackage by setting the `CONNECTION_POOLING_ENABLED` environment variable to `True`. This setting is recommended for operations with Microsoft Entra username and password connections to avoid throttling by the Microsoft Authentication Library (MSAL).


### Temporary files

During SqlPackage operations, the table data is written to temporary files before compression or after decompression. For large databases these temporary files can take up a significant amount of disk space but their location can be specified. The export and extract operations include an optional property to specify `/p:TempDirectoryForTableData` to override the SqlPackage's default value.

The .NET API [GetTempPath](/dotnet/api/system.io.path.gettemppath) is used to determine the default value within SqlPackage.

For Windows, the following environment variables are checked in the following order and the first path that exists is used:
1. The path specified by the `TMP` environment variable.
2. The path specified by the `TEMP` environment variable.
3. The path specified by the `USERPROFILE` environment variable.
4. The Windows directory.

For Linux and macOS, if the path isn't specified in the `TMPDIR` environment variable, the default path `/tmp/` is used.

## SqlPackage and database users

[Contained database users](../../relational-databases/security/contained-database-users-making-your-database-portable.md) are included in SqlPackage operations. However, the password portion of the definition is set to a randomly generated string by SqlPackage, the existing value isn't transferred. It's recommended that the new user's password is reset to a secure value following the import of a `.bacpac` or the deployment of a `.dacpac`. In an automated environment the password values can be retrieved from a secure keystore, such as Azure Key Vault, in a step following SqlPackage.


## Usage data collection

SqlPackage contains Internet-enabled features that can collect and send anonymous feature usage and diagnostic data to Microsoft.

SqlPackage may collect standard computer, use, and performance information that may be transmitted to Microsoft and analyzed to improve the quality, security, and reliability of SqlPackage.

SqlPackage doesn't collect user specific or personal information. To help approximate a single user for diagnostic purposes, SqlPackage generates a random GUID for each computer it runs on and use that value for all events it sends.

For details, see the [Microsoft Privacy Statement](https://go.microsoft.com/fwlink/?LinkID=824704), and [SQL Server Privacy supplement](../../sql-server/sql-server-privacy.md).

### Disable telemetry reporting

To disable telemetry collection and reporting, update the environment variable `DACFX_TELEMETRY_OPTOUT` to `true` or `1`.

## Support

The DacFx library and the SqlPackage CLI tool have adopted the [Microsoft Modern Lifecycle Policy](https://support.microsoft.com/help/30881/modern-lifecycle-policy). All security updates, fixes, and new features are released only in the latest point version of the major version. Maintaining your DacFx or SqlPackage installations to the current version helps ensure that you receive all applicable bug fixes in a timely manner.

Get help with SqlPackage, submit feature requests, and report issues in the [DacFx GitHub repository](https://github.com/microsoft/DacFx).

### Supported SQL offerings

SqlPackage and DacFx support all [supported SQL versions](/lifecycle/products/?products=sql-server) at time of the SqlPackage/DacFx release. For example, a SqlPackage release on January 14 2022 supports all supported versions of SQL in January 14 2022. For more on SQL support policies, see [the SQL support policy](/troubleshoot/sql/general/support-policy-sql-server#support-policy).

In addition to SQL Server, SqlPackage and DacFx supports Azure SQL Managed Instance, Azure SQL Database, Azure Synapse Analytics, and Synapse Data Warehouse in Microsoft Fabric.

## Next steps

- Learn more about [SqlPackage Extract](sqlpackage-extract.md)
- Learn more about [SqlPackage Publish](sqlpackage-publish.md)
- Learn more about [SqlPackage Export](sqlpackage-export.md)
- Learn more about [SqlPackage Import](sqlpackage-import.md)
- Learn more about [troubleshooting issues with SqlPackage](troubleshooting-issues-and-performance-with-sqlpackage.md)
- Share feedback on SqlPackage in the [DacFx GitHub repository](https://github.com/microsoft/DacFx)
