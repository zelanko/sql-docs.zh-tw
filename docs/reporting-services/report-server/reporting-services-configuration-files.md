---
title: Reporting Services 設定檔 | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25b695456bbac34e2c6ce8bf8c312c4108dd852e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506648"
---
# <a name="reporting-services-configuration-files"></a>Reporting Services 組態檔
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會將元件資訊儲存在登錄以及安裝過程中複製到檔案系統的組態檔內。 組態檔包含僅供內部使用和使用者自訂值的組合。 使用者自訂值會透過安裝程式、組態工具、命令列公用程式，以及手動編輯組態檔等方式指定。  
  
 只有當您要加入或設定進階設定時，才需要修改組態檔。 組態設定會指定為 XML 元素或屬性。 如果您了解 XML 和組態檔，就可以使用文字或程式碼編輯器來修改可由使用者定義的設定。 如需如何修改設定檔的詳細資訊，或想要進一步了解報表伺服器如何讀取全新和更新的組態設定，請參閱[修改 Reporting Services 設定檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
> [!NOTE]  
> 在先前的版本中，報表管理員具有名為 RSWebApplication.config 的自訂組態檔。該檔案現在已過時。 如果您是從舊版安裝升級，雖然系統不會刪除該檔案，但是報表伺服器也不會從該檔案讀取任何設定。 如果該檔案存在電腦上，您就應該刪除它。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中，所有報表管理員和入口網站的組態設定都是透過 RSReportServer.config 檔案進行儲存和讀取。 若要檢閱已刪除或移動之設定的清單，請參閱 [SQL Server 2016 中 SQL Server Reporting Services 的重大變更](../../reporting-services/breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)。  
  
 本文內容：  
  
-   [組態檔的摘要 (原生模式)](#bkmk_config_file_Summary_native_mode)  
  
-   [組態檔的摘要 (SharePoint 模式)](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> 組態檔的摘要 (原生模式)  
 下表將提供儲存組態設定之位置的描述。 大部分組態設定都會儲存在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 隨附的組態檔中。 根據預設，其安裝目錄如下：  
  
'' 安裝路徑  
C:\Program Files\Microsoft SQL Server\MSRSxx.MSSQLSERVER （其中 xx 是 MS SQL 版本號碼） 或  
C:\Program Files\Microsoft SQL Server Reporting Services\SSRS  
  SSRS 版本而定
```  
  
|Stored in:|Description|Location|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Stores configuration settings for feature areas of the Report Server service: Report Manager or the web portal, the Report Server Web service, and background processing. For more information about each setting, see [RsReportServer.config Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Stores the code access security policies for the server extensions. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|Stores the code access security policies for the web portal. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportManager|  
|Web.config for the Report Server Web service|Includes only those settings that are required for ASP.NET.|\<Installation directory> \Reporting Services \ReportServer|  
|Web.config for Report Manager|Includes only those settings that are required for ASP.NET if applicable for the SSRS version.|\<Installation directory> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|Stores configuration settings that specify the trace levels and logging options for the Report Server service. For more information about the elements in this file, see [ReportingServicesService Configuration File](../../reporting-services/report-server/reportingservicesservice-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer \Bin|  
|Registry settings|Stores configuration state and other settings used to uninstall Reporting Services. If you are troubleshooting an installation or configuration problem, you can view these settings to get information about how the report server is configured.<br /><br /> Do not modify these settings directly as this can invalidate your installation.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> **- And -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|Stores configuration settings for Report Designer. For more information, see [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
|RSPreviewPolicy.config|Stores the code access security policies for the server extensions used during report preview. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> Summary of configuration Files (SharePoint mode)  
 The following table provides a description of configuration files used for a SharePoint mode report server. Most configuration settings are stored in SharePoint service application databases. For more information, see [Reporting Services SharePoint Service and Service Applications](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).  
  
 By default, the installation directory for SharePoint mode is the following:  
  
```Install path
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|儲存於：|描述|位置|  
|----------------|-----------------|--------------|  
|RSReportServer.config|儲存報表伺服器服務之功能區的組態設定：報表管理員或入口網站、報表伺服器 Web 服務，以及背景處理。 如需每個設定的詳細資訊，請參閱 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。|\<安裝目錄> \Reporting Services\ReportServer|  
|RSSrvPolicy.config|儲存伺服器延伸模組的程式碼存取安全性原則。 如需有關這個檔案的詳細資訊，請參閱＜ [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)＞。|\<安裝目錄> \Reporting Services\ReportServer|  
|報表伺服器 Web 服務的 Web.config|包含僅如果適用於 SSRS 版本，則需要適用於 ASP.NET 的設定。|\<安裝目錄> \Reporting Services\ReportServer|  
|登錄設定|儲存用來解除安裝 Reporting Services 的組態狀態和其他設定。 同時儲存有關每個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的資訊。<br /><br /> 請勿直接修改這些設定，因為這樣做可能會讓安裝失效。|HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft \Microsoft SQL Server \\<執行個體識別碼\> \Setup<br /><br /> 範例執行個體識別碼：MSSQL13.MSSQLSERVER<br /><br /> **- 和 -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|儲存報表設計師的組態設定。 如需詳細資訊，請參閱 [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)。|\<磁碟機>:\Program Files\Microsoft Visual Studio 10\Common7\IDE\PrivateAssemblies|  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Reporting Services 延伸模組](../../reporting-services/extensions/reporting-services-extensions.md)   
 [rsconfig 公用程式 &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)   
 [啟動與停止報表伺服器服務](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
