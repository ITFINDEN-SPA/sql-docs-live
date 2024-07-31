---
title: "Use URL access in Web applications"
description: URL access in Reporting Services enables access to reports over a network, which allows integrating report viewing and navigation into a custom Web application.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/16/2017
ms.service: reporting-services
ms.subservice: application-integration
ms.topic: reference
ms.custom: updatefrequency5
helpviewer_keywords:
  - "links [Reporting Services], URL access"
  - "URL access [Reporting Services], Web applications"
  - "POST requests"
  - "direct addressing [Reporting Services]"
  - "Web applications [Reporting Services]"
  - "hyperlinks [Reporting Services]"
---
# Integrate Reporting Services by using URL access - Web application
  URL access in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] is designed to enable access to individual reports over a network. This type of access is best for integrating report viewing and navigation into a custom Web application. To use URL access in Web applications, you can:  
  
-   Address a URL to a specific report server from a Web site or portal.  
  
-   Use a form POST method and pass query string parameters to a report server URL using form fields.  
  
## URL access through direct addressing  
 To access a report server or report server database item using a URL, provide the URL address from within a Web browser or application. You can also supply parameters to the URL that can affect the appearance of the report or resource that is being accessed. A URL can target a report server through the address bar of a Web browser, or a URL can be the source of an **IFrame** that is part of a larger Web application or portal. You can include hyperlinks to reports on various Web pages of your portal and target a specific frame for the report or open a new browser window in the process.  
  
 In the following example, the hyperlink targets a frame named "main", which might be different from the one that includes the hyperlink. The hyperlink might be part of Web portal.  
  
```  
<a href="https://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main" target="main" >  
   Click here for the Territory Sales Drilldown sample report  
</a>  
```  
  
 In the previous example, the device information setting **LinkTarget** is passed with a value of "main" in the query string of the URL, which ensures that any drillthrough hyperlinks in the report also target the frame named "main".  
  
 For more information about device information settings, see [Passing Device Information Settings to Rendering Extensions](../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
 Many servers and browsers limit the number of characters allowed in a URL. In some cases, a 256-character limit is imposed. To get around this limitation, you can use POST requests using form submission.  
  
> [!NOTE]  
>  Internet Explorer has a maximum URL length of 2,083 characters. This limit applies to both POST and GET request URLs. POST, however, is not limited by the size of the URL for submitting name/value pairs as part of a form, because they are transferred in the header and not the URL.  
  
## URL access through a form POST method  
 When a user requests data from a report server using URL access, the HTTP request uses the GET method. This request is equivalent to a form submission where METHOD="GET". URL requests or form submissions that use METHOD="GET" are limited by the maximum number of characters that a server or Web browser can process.  
  
 With POST requests (METHOD="POST" and input fields), the name/value pairs are transferred in the header and not the URL. Therefore, the name/value pairs of the query string aren't part of the URL, thus enabling you to provide longer and more complex parameter lists.  
  
 A user can use direct access to see the URL for the report server. The user might be able to modify the query string or note the particular URL request and report server parameters for later use.  
  
 The following sample HTML demonstrates the use of a form that you can use to target a report server with a specific URL and pass query string parameters as part of the form's input fields.  
  
```  
<FORM id="frmRender" action="https://server/reportserver?/SampleReports/  
   Territory Sales Drilldown" method="post" target="_self">  
   <INPUT type="hidden" name="rs:Command" value="Render">   
   <INPUT type="hidden" name="rc:LinkTarget" value="main">  
   <INPUT type="hidden" name="rs:Format" value="HTML4.0">  
   <INPUT type="submit" value="Button">  
</FORM>  
```  
  
 In the previous example, if a user selects the button on the form, the report server returns an HTML-rendered report targeted at the current frame. The following example is a comparable URL access string:  
  
```  
https://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main&rs:Format=HTML4.0  
```  
  
## Related content  
 [Integrating Reporting Services into Applications](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Integrating Reporting Services by using URL access](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [Use URL Access in a Windows Application](../../reporting-services/application-integration/integrating-reporting-services-using-url-access-windows-application.md)   
 [URL Access &#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md)  
  
  