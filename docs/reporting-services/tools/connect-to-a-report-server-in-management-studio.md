---
title: "Connect to a report server in Management Studio"
description: Learn how to connect to any server in the SQL Server family and graphically browse its contents by using the Object Explorer in SQL Server Management Studio.
author: maggiesMSFT
ms.author: maggies
ms.date: 06/12/2024
ms.service: reporting-services
ms.subservice: tools
ms.topic: how-to
ms.custom: updatefrequency5
f1_keywords:
  - "sql13.swb.connecttors.connectionproperties.f1"
  - "sql13.swb.connecttors.login.f1"
  - "sql13.swb.connection.login.reportserver.f1"
helpviewer_keywords:
  - "report servers [Reporting Services], connections"
  - "connections [Reporting Services], report server"
  - "registering report servers"
  - "report servers [Reporting Services], registering"
  - "Connect to Server dialog box, Reporting Services"

#customer intent: As a SQL server user, I want to learn how to connect and graphically browse my SQL databases so that I can access and use my data.
---

# Connect to a report server in Management Studio

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] provides Object Explorer, so you can connect to any server in the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] family and graphically browse its contents. Object Explorer allows you to open connections to multiple server instances in the same workspace as long as the servers are registered in the same server group. For Reporting Services, you can use Object Explorer to do the following tasks:

- Enable report server features.

- Set server defaults and configure role definitions.

- Manage jobs that are running.

- Manage job schedules.

## Prerequisites

- [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]](../../ssms/download-sql-server-management-studio-ssms.md).
- A configured report server in native or Sharepoint mode. For instructions on how to configure your report server, see [Configure a report server (Reporting Services native mode)](../report-server/configure-a-report-server-reporting-services-native-mode.md).
- Sufficient permissions to manage your Report Server. For more information about permissions, see [Connection syntax and permissions](#connection-syntax-and-permissions).
- The server must be registered before you can connect to a report server instance in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. For instructions to register a report server, see [Register a report server](#register-a-report-server).

## Connect to a native mode report server

1. Open **Object Explorer** by selecting it from the **View** menu, if it isn't already open.

1. Select **Connect** to view the list of server types, and then choose the **Reporting Services...** option.

1. In the **Connect to Server** dialog box, enter the name of the report server instance into the **Server name** field. Report server instance names are based on [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance names. By default, the instance name of a local report server instance is the computer name. If you install the report server as a named instance, use this syntax to specify the server: `<servername>[\<instancename>]`.

1. From the **Authentication** drop-down menu, select the authentication type your server uses. If you use **Windows Authentication**, you connect by using your credentials. If you select **Basic Authentication** or **Forms Authentication**, enter the account and password.  
  
1. Select **Connect**. The report server appears in **Object Explorer**.  

1. Right-click the server node to set system properties and server defaults. For more information, see [Set report server properties &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md).

## Connect to a SharePoint integrated mode report server  

1. Open **Object Explorer** by selecting it from the **View** menu, if it isn't already open.

1. Select **Connect** to view the list of server types, and then choose the **Reporting Services...** option.

1. In the **Connect to Server** dialog box, enter a URL to a SharePoint site into the **Server name** field. The following example illustrates the syntax: `https://<web server>/sites/<site>`.

1. From the **Authentication** drop-down menu, select the authentication type your server uses. If you use **Windows Authentication**, you must connect by using your credentials. If you select **Basic Authentication** or **Forms Authentication**, enter the account and password.

1. Select **Connect**. The report server appears in **Object Explorer**.

1. Right-click the server node to set system properties and server defaults. For more information, see [Set report server properties &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md).

## Register a report server

1. If you can't connect to a report server, you either don't have permission to access it, or the server isn't registered. To register the server, select **View** in the menu > **Registered Servers**.

1. Select the **Reporting Services** icon.

1. Expand **Reporting Services** and right-click **Local Server Groups**. Select the **New Server Registration...** option. The **New Server Registration** dialog box appears.

1. For **Server name**, enter a value. You specify the value depending on the server mode:

    - For a native mode report server, enter the name of the report server instance. Report server instance names are based on [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance names. By default, the instance name of a local report server instance is the computer name. If you installed the report server as a named instance, use this syntax to specify the server: `<servername>[\<instancename>]`.

    - For a report server that runs in SharePoint integrated mode, you connect to the SharePoint site that the report server is connected to. Connect to the SharePoint site so that you can view the permission levels. The permissions control access to report server content and operations. You can specify any site in the site collection. The following example shows the syntax: `https://mysharepointsite`.

1. For **Authentication**, select the authentication mode that the report server uses from the drop-down menu.

   - If you use default security, choose **Windows Authentication**.
   - If you installed and deployed a custom security extension, choose **Forms Authentication**.
   - If you configured the report server to use basic authentication, choose **Basic Authentication**.
   - If you configured the report server for SharePoint integrated mode, choose **Windows Authentication**.

1. Select **Test** to verify the connection.

1. When prompted, select **OK**. Then select **Save**.

## Connection syntax and permissions

When you specify [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] as the **Server Type** in the **Connect to Server** dialog box, you can specify either a report server name or an endpoint to the Web service. The following table summarizes the connection syntax, steps, and permissions required to perform specific tasks:

|Connect to|   Tasks   |   Permissions   |
|----------|-----------|-----------------|  
|Native mode report server, connected as the default, or named instance:<br /><br /> `<server name>\<_instance>`<br /><br /> The connection to the report server is made through the Report Server WMI (Windows Management Instrumentation) provider.|View and set server properties and defaults.<br /><br /> View and cancel jobs.<br /><br /> Create and manage shared schedules.<br /><br /> Create, modify, or delete role definitions.|Assigned to the System Administrator role.|  
|Native mode report server, connected as the default, or named instance, through the endpoint to the Report Server Web service:<br /><br /> `https://<servername>/reportserver`<br /><br /> Specifying a URL to the report server provides an alternate way to connect to the report server.|View and set server properties and defaults.<br /><br /> View and cancel jobs.<br /><br /> Create and manage shared schedules.<br /><br /> Create, modify, or delete role definitions.|Assigned to the System Administrator role.|  
|SharePoint integrated mode report server, connected through the SharePoint site:<br /><br /> `https://<webserver>/<SharePointSite>`|View and set server properties and defaults.<br /><br /> View and cancel jobs.<br /><br /> Create and manage shared schedules defined for the site to which you're connected.<br /><br /> View the permission levels defined for the site to which you're connected.|Full Control level of permission on the SharePoint site to which you're connected.|
|SharePoint integrated mode report server, connected through the name of the report server instance:<br /><br /> `<server name>\<_instance>`|View and set server properties and defaults.<br /><br /> View and cancel jobs.|Full Control level of permission on the SharePoint site that is integrated with the report server.<br /><br /> Notice that when you connect to the report server rather than the SharePoint site, the number of tasks that you can do is reduced. The report server can only return application data that is stored or managed in the report server database. It can't return data stored in the SharePoint configuration and content databases.|

## Related content

- [Configure a report server database connection &#40;Report Server Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
- [Reporting Services in SQL Server Management Studio &#40;SSRS&#41;](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)
