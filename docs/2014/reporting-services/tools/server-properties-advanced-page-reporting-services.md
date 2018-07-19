---
title: 伺服器屬性 (進階頁面) - Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 2016-10-18
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.advanced.f1
ms.assetid: 07b78a84-a6aa-4502-861d-349720ef790e
caps.latest.revision: 16
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8b8459ccb49c2e8d2d681cada3646d7d9aa447b5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37258122"
---
# <a name="server-properties-advanced-page---reporting-services"></a>伺服器屬性 (進階頁面) - Reporting Services
  您可以使用這個頁面來設定報表伺服器的系統屬性。 有許多方式可設定系統屬性。 這項工具提供了圖形化使用者介面，如此您不需要撰寫程式碼就可以設定屬性。  
  
 若要開啟此頁面，請啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、連接至報表伺服器執行個體、以滑鼠右鍵按一下報表伺服器名稱，然後選取 [屬性]。 按一下 **[進階]** ，即可開啟此頁面。  
  
## <a name="options"></a>選項。  
 **EnableMyReports**  
 指出 [我的報表] 功能是否已啟用。 值為`true`表示已啟用此功能。  
  
 **MyReportsRole**  
 在使用者之 [我的報表] 資料夾上建立安全性原則時所使用的角色名稱。 預設值是 `My Reports Role`。  
  
 **EnableClientPrinting**  
 決定是否可從報表伺服器下載 RSClientPrint ActiveX 控制項。 有效值`true`和`false`。 預設值是 `true`。 如需此控制項所需之其他設定的詳細資訊，請參閱 [啟用和停用 Reporting Services 的用戶端列印功能](../report-server/enable-and-disable-client-side-printing-for-reporting-services.md)。  
  
 **EnableExecutionLogging**  
 指出報表執行記錄是否已啟用。 預設值是 `true`。 如需有關報表伺服器執行記錄的詳細資訊，請參閱 <<c0> [ 報表伺服器執行記錄和 ExecutionLog3 檢視](../report-server/report-server-executionlog-and-the-executionlog3-view.md)。  
  
 **ExecutionLogDaysKept**  
 要將報表執行資訊保留在執行記錄中的天數。 這個屬性的有效值包括`-1`經由`2`，`147`，`483`，`647`。 如果此值為 `-1`，系統就不會從執行記錄資料表中刪除項目。 預設值是 `60`。  
  
 **SessionTimeout**  
 工作階段維持作用中狀態的時間長度 (以秒為單位)。 預設值是 `600`。  
  
 **SharePointIntegratedMode**  
 這是指出伺服器模式的唯讀屬性。 如果此值為 False，報表伺服器就會以原生模式執行。  
  
 **SiteName**  
 顯示在報表管理員頁面標題中的報表伺服器網站名稱。 預設值是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]秒。 這個屬性可以是空字串。 最大長度是 8,000 個字元。  
  
 **StoredParametersLifetime**  
 指定預存參數可儲存的最大天數。 有效值`-1`，`+1`透過`2,147,483,647`。 預設值是`180`天。  
  
 **StoredParametersThreshold**  
 指定報表伺服器可儲存之參數值的最大數目。 有效值`-1`，`+1`透過`2,147,483,647`。 預設值是 `1500`。  
  
 **UseSessionCookies**  
 指出報表伺服器與用戶端瀏覽器通訊時是否應該使用工作階段 Cookie。 預設值是 `true`。  
  
 **ExternalImagesTimeout**  
 決定在連接逾時之前必須擷取外部影像檔的時間長度。預設值為 `600` 秒。  
  
 **SnapshotCompression**  
 定義快照集的壓縮方式。 預設值是 `SQL`。 有效值如下：  
  
 **SQL =** 當快照集儲存在報表伺服器資料庫時，系統會壓縮快照集。 這是目前的行為。  
  
 **無 =** 系統不會壓縮快照集。  
  
 **全部 =** 系統會針對所有儲存選項壓縮快照集，包括報表伺服器資料庫或是檔案系統。  
  
 **SystemReportTimeout**  
 在報表伺服器命名空間中管理之所有報表的預設報表處理逾時值 (以秒為單位)。 在報表層級可以覆寫這個值。 如果已設定此屬性，當指定的時間已過期時，報表伺服器就會嘗試停止處理報表。 有效值`-1`經由`2`，`147`，`483`，`647`。 如果此值為 `-1`，命名空間中的報表就不會在處理期間逾時。 預設值是 `1800`。  
  
 **SystemSnapshotLimit**  
 針對報表所儲存之快照集的最大數目。 有效值`-1`經由`2`，`147`，`483`，`647`。 如果值為`-1`，沒有任何快照集限制。  
  
 **EnableIntegratedSecurity**  
 決定 Windows 整合式安全性是否支援報表資料來源連接。 預設值為 `True`。 有效值如下：  
  
 `True` = Windows 整合式安全性已啟用。  
  
 `False` = Windows 整合式安全性未啟用。 設定為使用 Windows 整合式安全性的報表資料來源不會執行。  
  
 `EnableLoadReportDefinition`  
 選取此選項即可指定使用者是否可以從報表產生器報表執行特定報表執行。 設定此選項會決定的值`EnableLoadReportDefinition`報表伺服器上的屬性。  
  
 如果您清除此選項，這個屬性將會設定為 False 而且報表伺服器將不會針對使用報表模型做為資料來源的報表產生點選連結報表。 LoadReportDefinition 方法的任何呼叫都會被封鎖。  
  
 關閉此選項可減少惡意使用者利用 LoadReportDefinition 要求讓報表伺服器超過負載，藉以啟動阻斷服務攻擊的威脅。  
  
 **EnableRemoteErrors**  
 包含外部錯誤資訊 (例如，有關報表資料來源的錯誤資訊) 以及針對從遠端電腦要求報表之使用者傳回的錯誤訊息。 有效值`true`和`false`。 預設值是 `false`。 如需詳細資訊，請參閱[啟用遠端錯誤 &#40;Reporting Services&#41;](../report-server/enable-remote-errors-reporting-services.md)。  
  
 **EnableReportDesignClientDownload**  
 指定是否可從報表伺服器下載報表產生器安裝套件。 如果您清除此設定，報表產生器的 URL 將會失效。 如需詳細資訊，請參閱 [設定報表產生器的存取](../report-server/configure-report-builder-access.md)。  
  
 **EditSessionCacheLimit**  
 指定可以在報表編輯工作階段中使用的資料快取項目數目。 預設數目是 5。  
  
 **EditSessionTimeout**  
 指定報表編輯工作階段逾時之前的秒數。預設值是 7200 秒 (2 小時)。  
  
 **EnableTestConnectionDetailedErrors**  
 指出當使用者使用報表伺服器來測試資料來源連接時，是否要將詳細的錯誤訊息傳送至用戶端電腦。 預設值是 `true`。 如果選項設定為`false`，只是一般錯誤訊息傳送。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器屬性 &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [連接至 Management Studio 中的報表伺服器](connect-to-a-report-server-in-management-studio.md)   
 [Reporting Services 屬性](../report-server-web-service/net-framework/reporting-services-properties.md)   
 [Management Studio F1 說明中的報表伺服器](report-server-in-management-studio-f1-help.md)   
 [報表伺服器系統屬性](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
 [編寫部署和管理工作的指令碼](script-deployment-and-administrative-tasks.md)   
 [啟用與停用我的報表](../report-server/enable-and-disable-my-reports.md)  
  
  
