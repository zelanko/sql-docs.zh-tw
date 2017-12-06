---
title: "修改 Reporting Services 設定檔 (RSreportserver.config) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 958ef51f-2699-4cb2-a92e-3b4322e36a30
caps.latest.revision: "9"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: d1b8d12e3b01fc8717770ae5fdb117f114ae324d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="modify-a-reporting-services-configuration-file-rsreportserverconfig"></a>Modify a Reporting Services Configuration File (RSreportserver.config)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會將應用程式設定儲存在組態檔集合中。 安裝程式會針對您所安裝的每個報表伺服器執行個體建立組態檔。 在每個檔案內部，其值是在安裝期間設定，或當您使用工具和應用程式來設定作業的伺服器時設定。 在某些情況下，您必須直接修改檔案，以便加入或修改進階設定。 組態設定會指定為 XML 元素或屬性。 如果您了解 XML 和組態檔，就可以使用文字或程式碼編輯器來修改可由使用者定義的設定。  
  
 某些組態設定只能透過某個工具進行設定。 您必須透過 Reporting Services 組態工具、安裝程式或 **rsconfig** 命令列公用程式來修改包含加密值的設定。 您必須是本機管理員群組的成員才能執行這些工具。  
  
> [!IMPORTANT]  
>  修改組態檔時，請特別小心。 如果您修改保留給內部使用的設定，可能會停用安裝程序。 除非您嘗試解決特定問題，否則一般而言不建議您修改組態設定。 如需哪些設定可安全變更的詳細資訊，請參閱 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 或 [RSReportDesigner 組態檔](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)。 如需組態檔的詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 產品文件。  
  
 本主題內容：  
  
-   [讀取和使用組態值](#bkmk_read_values)  
  
-   [關於預設值](#bkmk_default_values)  
  
-   [刪除組態設定](#bkmk_delete_config_settings)  
  
-   [編輯 Reporting Services 組態檔](#bkmk_edit_configuation_file)  
  
##  <a name="bkmk_read_values"></a> 讀取和使用組態值  
 當服務啟動時，以及每次系統儲存組態檔時，報表伺服器都會讀取組態檔。 目前的應用程式網域過期之後，全新和修訂的值才會在新的應用程式網域中生效。 系統會盡可能讓仍然在目前應用程式網域中處理的要求完成。 不過，少數設定需要進行立即應用程式網域回收作業。 在這種情況下，所有處理中的要求都會在新的應用程式網域中重新啟動。  
  
 如果報表伺服器偵測到無效的值，報表伺服器就會在 Windows 應用程式記錄中記錄錯誤，而且無法啟動或使用預設值 (視錯誤情況而定)：  
  
-   如果錯誤是不正確的 XML，則報表伺服器將不會啟動。 如果您造成錯誤時，報表伺服器正在執行，報表伺服器就會忽略無效的組態檔，直到報表伺服器重新啟動或應用程式網域回收為止。 偵測到錯誤之後，報表伺服器將不會再啟動。  
  
-   如果錯誤是無效的組態值，伺服器將使用內部預設值並在追蹤記錄檔中記錄錯誤。 在內部預設值無法使用的少數情況下，如果無效的組態設定對於伺服器作業很重要，伺服器將傳回 rsServerConfigurationError 錯誤。 有關遺漏或無效重要設定的錯誤會以 HTML 錯誤頁面傳回用戶端應用程式並記錄在事件記錄中。  
  
 所有組態檔變更 (包括成功變更) 都會記錄在報表伺服器追蹤記錄檔中。 只有錯誤會記錄在應用程式事件記錄中。  
  
##  <a name="bkmk_default_values"></a> 關於預設值  
 大部分組態設定都具有報表伺服器內部指定的預設值。 如果使用者定義的值無效或未指定，報表伺服器就會使用這些值。 如果由於組態設定無效而必須使用預設值，系統就會在追蹤記錄檔中寫入錯誤。  
  
##  <a name="bkmk_delete_config_settings"></a> 刪除組態設定  
 如果是有預設值的組態設定，從組態檔中移除此設定不會有任何作用。 大部分組態設定實際上都會在內部定義及設定。 如果您刪除組態檔中的項目，內部複本仍然可以使用，而且會使用為它定義的預設值。  
  
##  <a name="bkmk_edit_configuation_file"></a> 編輯 Reporting Services 組態檔  
  
1.  尋找您想要編輯的組態檔：  
  
    -   **RSReportServer.config** 位於下列資料夾：  
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer  
        ```  
        
        ||  
        |-|  
        |**[!INCLUDE[applies](../../includes/applies-md.md)]**SQL Server Reporting Services 中的 Power BI 報表 2017 年 1 月技術預覽|
        
        ```  
        C:\Program Files\Microsoft SQL Server Reporting Services\RSServer\ReportServer
        ```
  
    -   **RSReportServerServices.exe.config** 位於下列資料夾：  
    
        > [!NOTE] 
        > SQL Server Reporting Services 中的 Power BI 報表 2017 年 1 月技術預覽未提供此內容。
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin  
        ```  
  
    -   **RSReportDesigner.config** 位於下列資料夾：  
  
        ```  
        C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
        ```  
  
2.  儲存檔案的副本，以防您需要回復變更。  
  
3.  在 [記事本] 或程式碼編輯器中開啟原始檔。 請勿使用 Textpad，因為它會在儲存檔案之前設定檔案長度，進而導致系統在追蹤記錄檔中寫入無效字元錯誤。  
  
4.  輸入您想要加入或使用的元素或值。 元素會區分大小寫。 如果您要加入元素，請務必使用正確的大小寫字母。 如果您要自訂轉譯延伸模組、驗證延伸模組或資料處理延伸模組，請使用編輯組態檔的特定指示。  
  
    -   [報表伺服器的驗證](../../reporting-services/security/authentication-with-the-report-server.md)  
  
    -   [設定入口網站傳遞自訂驗證 Cookie](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)
  
    -   [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
5.  儲存檔案。  
  
6.  檢查追蹤記錄檔，以便確認錯誤並未發生。 如果您看見錯誤狀況，表示某項設定或其值的指定內容不正確。 請檢閱 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) ，以便取得導致錯誤發生之任何設定的有效值。 如需如何檢視追蹤記錄的詳細資訊，請參閱 [報表伺服器服務追蹤記錄](../../reporting-services/report-server/report-server-service-trace-log.md)。  
  
## <a name="see-also"></a>另請參閱  
 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [ReportingServicesService 設定檔](../../reporting-services/report-server/reportingservicesservice-configuration-file.md)   
 [RSReportDesigner 組態檔](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [部署資料處理延伸模組](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [部署傳遞延伸模組](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)   
 [部署轉譯延伸模組](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)   
 [Reporting Services 設定檔](../../reporting-services/report-server/reporting-services-configuration-files.md)  
  
  
