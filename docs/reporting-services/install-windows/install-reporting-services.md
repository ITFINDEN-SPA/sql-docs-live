---
title: "Install and configure SQL Server Reporting Services"
description: "Install and configure SQL Server Reporting Services (SSRS) components for storing report items, rendering reports, and processing other report services."
author: maggiesMSFT
ms.author: maggies
ms.date: 07/08/2024
ms.service: reporting-services
ms.subservice: report-server
ms.topic: install-set-up-deploy
ms.custom:
  - intro-installation
  - updatefrequency5
monikerRange: ">= sql-server-2016"
#customer intent: As a SQL Server user, I want to install and configure SQL Server Reporting Services so that I can better leverage data and generate robust reports.

---
# Install and configure SQL Server Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

This article helps you download, install, and configure SQL Server Reporting Services (SSRS). SSRS installation involves server components for storing report items, rendering reports, and processing of subscription and other report services. Alternatively, an administrator can install Reporting Services with [Microsoft Endpoint Configuration Manager](/configmgr/).

::: moniker range="=sql-server-ver16"
Download [**SQL Server 2022 Reporting Services**](https://www.microsoft.com/download/details.aspx?id=104502) from the Microsoft Download Center.

::: moniker-end

::: moniker range="<=sql-server-ver15"
Download [**SQL Server 2019 Reporting Services**](https://www.microsoft.com/download/details.aspx?id=100122) from the Microsoft Download Center.

::: moniker-end

::: moniker range="=sql-server-2017"
Download [**SQL Server 2017 Reporting Services**](https://www.microsoft.com/download/details.aspx?id=55252) from the Microsoft Download Center.

::: moniker-end

> [!NOTE]
> Looking for Power BI Report Server? See [Install Power BI Report Server](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/).
> 
> Upgrading or migrating from a SQL Server 2016 or earlier version of Reporting Services? See [Upgrade and migrate Reporting Services](upgrade-and-migrate-reporting-services.md).

## Prerequisites

Review the [Hardware and software requirements for installing SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md). Ensure that the computer where you're installing SSRS meets the appropriate hardware and software prerequisites for the version you want to install.

## Install SSRS

Use the following steps to install SSRS.

1. Locate `SQLServerReportingServices.exe` and launch the installer.

1. Select **Install Reporting Services**.

1. Choose an edition to install and select **Next**.

    For a free edition, choose either Evaluation or Developer.

    :::image type="content" source="media/install-reporting-services/report-server-install-edition-select.png" alt-text="Screenshot of the Reporting Services editions that are available for download.":::

    Otherwise, enter a product key. For more information, see [Find the product key for SQL Server Reporting Services](find-reporting-services-product-key-ssrs.md).

1. Accept the license terms and conditions, and then select **Next**.

1. Select **Next**.

1. Specify the installation location for the report server. Select **Install** to continue.

    > [!NOTE]
    > The default path is `C:\Program Files\Microsoft SQL Server Reporting Services`.

1. After the installation completes, select **Configure report server** to launch the Report Server Configuration Manager.

## Configure your report server

After you select **Configure Report Server**, the **Report Server Configuration Manager** appears. For more information, see [Report Server Configuration Manager](reporting-services-configuration-manager-native-mode.md).

Follow the instructions to [Create a report server database](ssrs-report-server-create-a-report-server-database.md) to complete the initial Reporting Services configuration process. 

### Create a database on a different server

If you're creating the report server database on a separate database server, change the service account for the report server to a credential recognized on the database server.

By default, the report server uses the virtual service account. Attempting to create a database on a different server might lead to the following error during the **Applying connection rights** step:

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

To address this issue, you can change the service account to either Network Service or a domain account. Choosing **Network Service** applies rights in the context of the report server's computer account.

For more information, see [Configure the report server service account](configure-the-report-server-service-account-ssrs-configuration-manager.md).

## Windows service

The installation creates a Windows service as a part of the process. The service displays as **SQL Server Reporting Services**. The service name is **SQLServerReportingServices**.

## Default URL reservations

URL reservations are composed of a prefix, host name, port, and virtual directory:

|Part|Description|
|----------|-----------------|
|Prefix|The default prefix is `HTTP`. If you installed a Transport Layer Security (TLS) certificate, the installer creates URL reservations that use the `HTTPS` prefix.|
|Host name|The default host name is a strong wildcard (+). It specifies that the report server accepts any HTTP request on the designated port for any host name that resolves to the computer, including `https://<computername>/reportserver`, `https://localhost/reportserver`, or `https://<IPAddress>/reportserver`.|
|Port|The default port is 80. If you use any other port, you must explicitly add the port to the URL when you open web portal in a browser window.|
|Virtual directory|By default, the Report Server web service virtual directory is `reportserver`. For the web portal, the default virtual directory is `reports`.|

Examples of the complete URL string are:

- `https://+:80/reportserver`: This string provides access to the report server.

- `https://+:80/reports`: This string provides access to the web portal.

## Firewall

If you're accessing the report server from a remote computer and there's a firewall present, make sure you configured any firewall rules.

Open the TCP port that you configured for your web service URL and web portal URL. By default, these URLs are configured on TCP port 80.

## Configure other features

You might need to configure other features for better report access and usability. You can configure integration with the Power BI service so that you can pin report items to a Power BI dashboard. For more information, see [Power BI Report Server Integration (Configuration Manager)](power-bi-report-server-integration-configuration-manager.md).

### Configure email for subscriptions processing

To configure email for subscriptions processing, see:

- [Email settings in SSRS native mode](e-mail-settings-reporting-services-native-mode-configuration-manager.md)
- [Email delivery in Reporting Services](../subscriptions/e-mail-delivery-in-reporting-services.md)

### Set up reports from a remote computer

You can also set up the web portal so that you can access and manage reports from a remote computer. For more information, see:

- [Configure a firewall for report server access](../report-server/configure-a-firewall-for-report-server-access.md)
- [Configure a report server for remote administration](../report-server/configure-a-report-server-for-remote-administration.md)

## Related content

- For information on how to install SQL Server Reporting Services native mode, see [Install Reporting Services native mode report server](install-reporting-services-native-mode-report-server.md). 

- With your report server installed, begin to create reports and deploy the reports to your report server. For information on how to start with Report Builder, see [Install Microsoft Report Builder](../../reporting-services/install-windows/install-report-builder.md).

- For information on how to create reports using SQL Server Data Tools, [download SQL Server Data Tools](../../ssdt/download-sql-server-data-tools-ssdt.md).

::: moniker range="=sql-server-2016"

- For information on how to install SQL Server 2016 Reporting Services (and earlier) in SharePoint integration mode, see [Install the first Report Server in SharePoint mode](install-the-first-report-server-in-sharepoint-mode.md).

::: moniker-end

More questions? [Try asking the Reporting Services forum](/answers/search.html?c=&f=&includeChildren=&q=ssrs+OR+reporting+services&redirect=search%2fsearch&sort=relevance&type=question+OR+idea+OR+kbentry+OR+answer+OR+topic+OR+user).
