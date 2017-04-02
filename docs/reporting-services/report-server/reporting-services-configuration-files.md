---
title: "Reporting Services 組態檔 | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "部署 [Reporting Services], 組態檔"
  - "組態選項 [Reporting Services]"
  - "修改組態檔"
  - "組態檔 [Reporting Services]"
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
caps.latest.revision: 52
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 51
---
# Reporting Services 組態檔
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會將元件資訊儲存在登錄以及安裝過程中複製到檔案系統的組態檔內。 組態檔包含僅供內部使用和使用者自訂值的組合。 使用者自訂值會透過安裝程式、組態工具、命令列公用程式，以及手動編輯組態檔等方式指定。  
  
 只有當您要加入或設定進階設定時，才需要修改組態檔。 組態設定會指定為 XML 元素或屬性。 如果您了解 XML 和組態檔，就可以使用文字或程式碼編輯器來修改可由使用者定義的設定。 如需如何修改組態檔的詳細資訊，或想要進一步了解報表伺服器如何讀取全新和更新的組態設定，請參閱[修改 Reporting Services 組態檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
> [!NOTE]  
>  在先前的版本中，報表管理員具有名為 RSWebApplication.config 的自訂組態檔。 該檔案現在已過時。 如果您是從舊版安裝升級，雖然系統不會刪除該檔案，但是報表伺服器也不會從該檔案讀取任何設定。 如果該檔案存在電腦上，您就應該刪除它。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中，所有報表管理員的組態設定都是透過 RSReportServer.config 檔進行儲存和讀取。 若要檢閱已刪除或移動之設定的清單，請參閱 [SQL Server 2016 中 SQL Server Reporting Services 的重大變更](../../reporting-services/breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)。  
  
 本主題內容：  
  
-   [組態檔的摘要 (原生模式)](#bkmk_config_file_Summary_native_mode)  
  
-   [組態檔的摘要 (SharePoint 模式)](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> 組態檔的摘要 (原生模式)  
 下表將提供儲存組態設定之位置的描述。 大部分組態設定都會儲存在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]隨附的組態檔中。 根據預設，其安裝目錄如下：  
  
```  
C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER  
```  
  
|儲存於：|說明|位置|  
|----------------|-----------------|--------------|  
|RSReportServer.config|儲存報表伺服器服務之功能區的組態設定：報表管理員、報表伺服器 Web 服務，以及背景處理。 如需每個設定的詳細資訊，請參閱 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。|\<安裝目錄> \Reporting Services\ReportServer|  
|RSSrvPolicy.config|儲存伺服器延伸模組的程式碼存取安全性原則。 如需有關這個檔案的詳細資訊，請參閱＜ [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)＞。|\<安裝目錄> \Reporting Services\ReportServer|  
|RSMgrPolicy.config|儲存報表管理員的程式碼存取安全性原則。 如需有關這個檔案的詳細資訊，請參閱＜ [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)＞。|\<安裝目錄> \Reporting Services\ReportManager|  
|報表伺服器 Web 服務的 Web.config|只包含 ASP.NET 所需的設定。|\<安裝目錄> \Reporting Services\ReportServer|  
|報表管理員的 Web.config|只包含 ASP.NET 所需的設定。|\<安裝目錄> \Reporting Services\ReportManager|  
|ReportingServicesService.exe.config|儲存針對報表伺服器服務指定追蹤層級和記錄選項的組態設定。 如需有關這個檔案中之元素的詳細資訊，請參閱＜ [ReportingServicesService Configuration File](../../reporting-services/report-server/reportingservicesservice-configuration-file.md)＞。|\<安裝目錄> \Reporting Services\ReportServer \Bin|  
|登錄設定|儲存用來解除安裝 Reporting Services 的組態狀態和其他設定。 如果您要疑難排解安裝或組態問題，可以檢視這些設定來取得有關報表伺服器之設定方式的資訊。<br /><br /> 請勿直接修改這些設定，因為這樣做可能會讓安裝失效。|HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft \Microsoft SQL Server \\<執行個體識別碼\> \Setup<br /><br /> **- 和 -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|儲存報表設計師的組態設定。 如需詳細資訊，請參閱 [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)。|\<磁碟機>:\Program Files\Microsoft Visual Studio 10\Common7\IDE\PrivateAssemblies|  
|RSPreviewPolicy.config|儲存報表預覽期間使用之伺服器延伸模組的程式碼存取安全性原則。 如需有關這個檔案的詳細資訊，請參閱＜ [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)＞。|C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> 組態檔的摘要 (SharePoint 模式)  
 下表提供用於 SharePoint 模式報表伺服器之組態檔的描述。 大部分組態設定都儲存在 SharePoint 服務應用程式資料庫中。 如需詳細資訊，請參閱 [Reporting Services SharePoint 服務和服務應用程式](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md)。  
  
 根據預設，SharePoint 模式的安裝目錄如下：  
  
```  
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|儲存於：|說明|位置|  
|----------------|-----------------|--------------|  
|RSReportServer.config|儲存報表伺服器服務之功能區的組態設定：報表管理員、報表伺服器 Web 服務，以及背景處理。 如需每個設定的詳細資訊，請參閱 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。|\<安裝目錄> \Reporting Services\ReportServer|  
|RSSrvPolicy.config|儲存伺服器延伸模組的程式碼存取安全性原則。 如需有關這個檔案的詳細資訊，請參閱＜ [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)＞。|\<安裝目錄> \Reporting Services\ReportServer|  
|報表伺服器 Web 服務的 Web.config|只包含 ASP.NET 所需的設定。|\<安裝目錄> \Reporting Services\ReportServer|  
|登錄設定|儲存用來解除安裝 Reporting Services 的組態狀態和其他設定。 同時儲存有關每個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的資訊。<br /><br /> 請勿直接修改這些設定，因為這樣做可能會讓安裝失效。|HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft \Microsoft SQL Server \\<執行個體識別碼\> \Setup<br /><br /> 範例執行個體識別碼：MSSQL13.MSSQLSERVER<br /><br /> **- 和 -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|儲存報表設計師的組態設定。 如需詳細資訊，請參閱 [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)。|\<磁碟機>:\Program Files\Microsoft Visual Studio 10\Common7\IDE\PrivateAssemblies|  
  
## 請參閱＜  
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Reporting Services 延伸模組](../../reporting-services/extensions/reporting-services-extensions.md)   
 [rsconfig 公用程式 &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)   
 [啟動與停止 Report Server 服務](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  