---
title: 伺服器屬性 (進階頁面) - Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: tools
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.advanced.f1
ms.assetid: 07b78a84-a6aa-4502-861d-349720ef790e
caps.latest.revision: 18
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 336a201dde0a1afba761e135d561079ce5c95d75
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34550399"
---
# <a name="server-properties-advanced-page---reporting-services"></a>伺服器屬性 (進階頁面) - Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

您可以使用這個頁面來設定報表伺服器的系統屬性。 有許多方式可設定系統屬性。 這項工具提供了圖形化使用者介面，如此您不需要撰寫程式碼就可以設定屬性。

若要開啟此頁面，請啟動 SQL Server Management Studio，並連線至報表伺服器執行個體，然後以滑鼠右鍵按一下報表伺服器名稱，再選取 [屬性]。 選取 [進階]，即可開啟此頁面。

## <a name="options"></a>選項。

**EnableMyReports**  
指出 [我的報表] 功能是否已啟用。 值若為 **true** 表示此功能已啟用。  

**MyReportsRole**  
在使用者之 [我的報表] 資料夾上建立安全性原則時所使用的角色名稱。 預設值是 **My Reports Role**秒。  

**EnableClientPrinting**  
決定是否可從報表伺服器下載 RSClientPrint ActiveX 控制項。 有效值為 **true** 和 **false**。 預設值為 **true**。 如需此控制項所需之其他設定的詳細資訊，請參閱 [啟用和停用 Reporting Services 的用戶端列印功能](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)。  

**EnableExecutionLogging**  
指出報表執行記錄是否已啟用。 預設值為 **true**。 如需報表伺服器執行記錄的詳細資訊，請參閱 [報表伺服器執行記錄和 ExecutionLog3 檢視](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)。  

**ExecutionLogDaysKept**  
要將報表執行資訊保留在執行記錄中的天數。 這個屬性的有效值包括 **-1** 至 **2**、**147**、**483**和**647**。 如果此值為 **-1**，系統不會從執行記錄資料表中刪除項目。 預設值是 **60**秒。  

> [!NOTE] 
> 將值設定為 **0** 會「刪除」執行記錄中的所有項目。 **-1** 值會保留執行記錄的項目，且不會將其刪除。

**SessionTimeout**  
工作階段維持作用中狀態的時間長度 (以秒為單位)。 預設值是 **600**秒。  

**SharePointIntegratedMode**  
此唯讀屬性指出伺服器模式。 如果此值為 False，報表伺服器就會以原生模式執行。  

**SiteName**  
顯示在入口網站頁面標題中的報表伺服器網站名稱。 預設值是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]秒。 這個屬性可以是空字串。 最大長度是 8,000 個字元。  

**StoredParametersLifetime**  
指定預存參數可儲存的最大天數。 有效值是 **-1**、 **+1** 到 **2,147,483,647**。 預設值為 **180** 天。  

**StoredParametersThreshold**  
指定報表伺服器可儲存之參數值的最大數目。 有效值是 **-1**、 **+1** 到 **2,147,483,647**。 預設值是 **1500**秒。  

**UseSessionCookies**  
指出報表伺服器與用戶端瀏覽器通訊時是否應該使用工作階段 Cookie。 預設值為 **true**。  

**ExternalImagesTimeout**  
決定在連接逾時之前必須擷取外部影像檔的時間長度。預設值為 **600** 秒。  

**SnapshotCompression**  
定義快照集的壓縮方式。 預設值是 **SQL**秒。 有效值如下：

|值|描述|
|---------|---------|
|**SQL**|快照集在儲存於報表伺服器資料庫時會進行壓縮。 此壓縮為目前的行為。|
|**無**|系統不會壓縮快照集。|
|**全部**|系統會針對所有儲存選項壓縮快照集，包括報表伺服器資料庫或是檔案系統。|

**SystemReportTimeout**  
在報表伺服器命名空間中管理之所有報表的預設報表處理逾時值 (以秒為單位)。 在報表層級可以覆寫這個值。 如果已設定此屬性，當指定的時間已過期時，報表伺服器就會嘗試停止處理報表。 有效值是 **-1** 到 **2**,**147**,**483**,**647**。 如果此值為 **-1**，命名空間中的報表就不會在處理期間逾時。 預設值是 **1800**秒。  

**SystemSnapshotLimit**  
針對報表所儲存之快照集的最大數目。 有效值是 **-1** 到 **2**,**147**,**483**,**647**。 如果此值為 **-1**，表示沒有任何快照集限制。  

**EnableIntegratedSecurity**  
決定 Windows 整合式安全性是否支援報表資料來源連接。 預設值為 **True**。 有效值如下：

|值|描述|
|---------|---------|
|**True**|已啟用 Windows 整合式安全性。|
|**False**|未啟用 Windows 整合式安全性。 設定為使用 Windows 整合式安全性的報表資料來源不會執行。|

**EnableLoadReportDefinition**  
選取此選項即可指定使用者是否可以從報表產生器報表執行特定報表執行。 設定這個選項會針對報表伺服器決定 **EnableLoadReportDefinition** 屬性的值。  

如果您清除此選項，屬性會設為 False。 報表伺服器將不會針對使用報表模型作為資料來源的報表產生點選連結報表。 LoadReportDefinition 方法的任何呼叫都會遭封鎖。  

關閉此選項可減少惡意使用者利用 LoadReportDefinition 要求讓報表伺服器超過負載，藉以啟動阻斷服務攻擊的威脅。  

**EnableRemoteErrors**  
包含外部錯誤資訊 (例如，有關報表資料來源的錯誤資訊) 以及針對從遠端電腦要求報表之使用者傳回的錯誤訊息。 有效值為 **true** 和 **false**。 預設值為 **false**。 如需詳細資訊，請參閱[啟用遠端錯誤 &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md)。  

**EnableReportDesignClientDownload**  
指定是否可從報表伺服器下載報表產生器安裝套件。 如果您清除此設定，報表產生器的 URL 將會失效。 

**EditSessionCacheLimit**  
指定可以在報表編輯工作階段中使用的資料快取項目數目。 預設數目是 5。  

**EditSessionTimeout**  
指定報表編輯工作階段逾時之前的秒數。預設值為 7200 秒 (兩小時)。  

**EnableCustomVisuals** ***(僅限 Power BI 報表伺服器)***  
PowerBI ReportServer 應該啟用 PowerBI 自訂視覺效果的顯示。 值為 True、False。  預設值是 True。  

**EnablePowerBIReportExportData** ***(僅限 Power BI 報表伺服器)***  
PowerBI ReportServer 應該啟用從 PowerBI 視覺效果匯出資料。 值為 True、False。  預設值是 True。  

**ScheduleRefreshTimeoutMinutes** ***(僅限 Power BI 報表伺服器)***  
在含內嵌 AS 模型的 PowerBI 報表上排定重新整理的資料重新整理逾時 (分鐘)。 預設值是 120 分鐘。

**EnableTestConnectionDetailedErrors**  
指出當使用者使用報表伺服器來測試資料來源連線時，是否要將詳細的錯誤訊息傳送至用戶端電腦。 預設值為 **true**。 如果此選項設定為 **false**，就只會傳送一般錯誤訊息。

**AccessControlAllowCredentials**  
指出 'credentials' 旗標設為 true 時是否可以公開用戶端要求的回應。 預設值為 **false**。

**AccessControlAllowHeaders** 伺服器在用戶端提出要求時允許的標題清單 (以逗號分隔)。 這個屬性可以是空字串，而指定 * 將允許所有標題。

**AccessControlAllowMethods** 伺服器在用戶端提出要求時允許的 HTTP 方法清單 (以逗號分隔)。 預設值為 (GET、PUT、POST、PATCH、DELETE)，而指定 * 將允許所有方法。

**AccessControlAllowOrigin** 伺服器在用戶端提出要求時允許的來源清單 (以逗號分隔)。 預設值是可防止所有要求的空白，而指定 * 將在未設定認證時允許所有來源；如果指定認證，則必須指定明確的來源清單。

**AccessControlExposeHeaders** 伺服器向用戶端公開的標題清單 (以逗號分隔)。 預設值是空白。

**AccessControlMaxAge** 指定可快取推斷要求結果的秒數。 預設值為 600 (10 分鐘)。

## <a name="see-also"></a>另請參閱

[設定報表伺服器屬性 &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[連接至 Management Studio 中的報表伺服器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Reporting Services 屬性](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Management Studio F1 說明中的報表伺服器](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[報表伺服器系統屬性](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[編寫部署和管理工作的指令碼](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[啟用與停用我的報表](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
