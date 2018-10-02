---
title: 伺服器屬性 (進階頁面) - Reporting Services | Microsoft Docs
author: markingmyname
ms.author: maghan
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.date: 08/16/2018
ms.openlocfilehash: f897c332130ece43357869972ff406ea79a6c21d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47725017"
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

**RDLXReportTimetout** RDLX 報表 *(SharePoint Server 中的 Power View 報表)* 報表伺服器命名空間中所有受控報表的預設報表處理逾時值 (以秒為單位)。 在報表層級可以覆寫這個值。 如果已設定此屬性，當指定的時間已過期時，報表伺服器就會嘗試停止處理報表。 有效值是 **-1** 到 **2**,**147**,**483**,**647**。 如果此值為 **-1**，命名空間中的報表就不會在處理期間逾時。 預設值是 **1800**秒。

**SessionTimeout** 工作階段維持作用中狀態的時間長度 (以秒為單位)。 預設值是 **600**秒。  

**SharePointIntegratedMode**  
此唯讀屬性指出伺服器模式。 如果此值為 False，報表伺服器就會以原生模式執行。  

**SiteName**  
顯示在入口網站頁面標題中的報表伺服器網站名稱。 預設值是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]秒。 這個屬性可以是空字串。 最大長度是 8,000 個字元。  

**StoredParametersLifetime** 指定可儲存預存參數的最大天數。 有效值是 **-1**、 **+1** 到 **2,147,483,647**。 預設值為 **180** 天。  

**StoredParametersThreshold**  
指定報表伺服器可儲存之參數值的最大數目。 有效值是 **-1**、 **+1** 到 **2,147,483,647**。 預設值是 **1500**秒。  

**UseSessionCookies**  
指出報表伺服器與用戶端瀏覽器通訊時是否應該使用工作階段 Cookie。 預設值為 **true**。  

**ExternalImagesTimeout**  
決定在連接逾時之前必須擷取外部影像檔的時間長度。預設值為 **600** 秒。  

**SnapshotCompression** 當時的報表伺服器快照集。

**SnapshotCompression**  
定義快照集的壓縮方式。 預設值是 **SQL**秒。 有效值如下：

|值|Description|
|---------|---------|
|**SQL**|快照集在儲存於報表伺服器資料庫時會進行壓縮。 此壓縮為目前的行為。|
|**無**|系統不會壓縮快照集。|
|**全部**|系統會針對所有儲存選項壓縮快照集，包括報表伺服器資料庫或是檔案系統。|

**SystemReportTimeout**  
在報表伺服器命名空間中管理之所有報表的預設報表處理逾時值 (以秒為單位)。 在報表層級可以覆寫這個值。 如果已設定此屬性，當指定的時間已過期時，報表伺服器就會嘗試停止處理報表。 有效值是 **-1** 到 **2**,**147**,**483**,**647**。 如果此值為 **-1**，命名空間中的報表就不會在處理期間逾時。 預設值是 **1800**秒。  

**SystemSnapshotLimit**  
針對報表所儲存之快照集的最大數目。 有效值是 **-1** 到 **2**,**147**,**483**,**647**。 如果此值為 **-1**，表示沒有任何快照集限制。  

**EnableIntegratedSecurity**  
決定報表資料來源連線是否支援 Windows 整合式安全性。 預設值為 **True**。 有效值如下：

|值|Description|
|---------|---------|
|**True**|已啟用 Windows 整合式安全性。|
|**False**|未啟用 Windows 整合式安全性。 設定為使用 Windows 整合式安全性的報表資料來源不會執行。|

**EnableLoadReportDefinition**  
選取此選項，指定使用者是否可以從報表產生器報表執行未規劃的報表執行。 設定這個選項會針對報表伺服器決定 **EnableLoadReportDefinition** 屬性的值。  

如果您清除此選項，屬性會設為 False。 報表伺服器將不會針對使用報表模型作為資料來源的報表產生點選連結報表。 LoadReportDefinition 方法的任何呼叫都會遭封鎖。  

關閉此選項可減少惡意使用者利用 LoadReportDefinition 要求讓報表伺服器超過負載，藉以啟動阻斷服務攻擊的威脅。  

**EnableRemoteErrors**  
包含外部錯誤資訊 (例如，有關報表資料來源的錯誤資訊) 以及針對從遠端電腦要求報表之使用者傳回的錯誤訊息。 有效值為 **true** 和 **false**。 預設值為 **false**。 如需詳細資訊，請參閱[啟用遠端錯誤 &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md)。  

**AccessControlAllowCredentials**  
指出 'credentials' 旗標設為 true 時是否可以公開用戶端要求的回應。 預設值為 **false**。

**AccessControlAllowHeaders** 伺服器在用戶端提出要求時允許的標題清單 (以逗號分隔)。 這個屬性可以是空字串，而指定 * 將允許所有標題。

**AccessControlAllowMethods** 伺服器在用戶端提出要求時允許的 HTTP 方法清單 (以逗號分隔)。 預設值為 (GET、PUT、POST、PATCH、DELETE)，而指定 * 將允許所有方法。

**AccessControlAllowOrigin** 伺服器在用戶端提出要求時允許的來源清單 (以逗號分隔)。 預設值是可防止所有要求的空白，而指定 * 將在未設定認證時允許所有來源；如果指定認證，則必須指定明確的來源清單。

**AccessControlExposeHeaders** 伺服器向用戶端公開的標題清單 (以逗號分隔)。 預設值是空白。

**AccessControlMaxAge** 指定可快取推斷要求結果的秒數。 預設值為 600 (10 分鐘)。

**EditSessionCacheLimit**  
指定可以在報表編輯工作階段中使用的資料快取項目數目。 預設數目是 5。  

**EditSessionTimeout**  
指定報表編輯工作階段逾時之前的秒數。預設值為 7200 秒 (兩小時)。  

**EnableCustomVisuals** ***(僅限 Power BI 報表伺服器)*** 啟用 Power BI 自訂視覺效果的顯示。 值為 True/False。 *預設值為 True。*  

**ExecutionLogLevel** 設定執行記錄層級。 *預設值為「標準」。*

**InterProcessTimeoutMinutes** 設定處理序逾時 (以分鐘為單位)。 *預設值為 30。*

**MaxFileSizeMb** 設定報表的最大檔案大小 (以 MB 為單位)。 *預設值為 1000。最大值為 2000。*

**ModelCleanupCycleminutes** 設定模型清除循環 (以分鐘為單位)。 *預設值為 15。*

**OfficeAccessTokenExpirationSeconds** ***(僅限 Power BI 報表伺服器)*** 設定您要 Office 存取權杖多久到期 (以秒為單位)。 *預設值為 60。*

**OfficeOnlineDiscoveryURL** ***(僅限 Power BI 報表伺服器)*** 設定 Office Online Server 執行個體的位址以檢視 Excel 活頁簿。

**RequireIntune** 要求 Intune 透過 Power BI 行動應用程式存取組織報表。 *預設值為 False。*

**ScheduleRefreshTimeoutMinutes** ***(僅限 Power BI 報表伺服器)*** 設定您要排程重新整理多久逾時。*預設值為 120。*

**ShowDownloadMenu** 啟用用戶端工具下載功能表。 *預設值為 true。*

**TimeInitialDelaySeconds** 設定您要延遲多久的初始時間 (以秒為單位)。 *預設值為 60。*

**TrustedFileFormat**設定在 Reporting Services 入口網站之下，所有要在瀏覽器中開啟的外部檔案格式。 未列出的外部檔案格式會在瀏覽器中提示下載選項。 預設值為 jpg、jpeg、jpe、wav、bmp、pdf、img、gif、json、mp4、web、png。

**EnablePowerBIReportExportData** ***(僅限 Power BI 報表伺服器)***  
啟用從 Power BI 視覺效果的 Power BI 報表伺服器資料匯出。 值為 True、False。  預設值是 True。  

**ScheduleRefreshTimeoutMinutes** ***(僅限 Power BI 報表伺服器)***  
在含內嵌 AS 模型的 PowerBI 報表上排定重新整理的資料重新整理逾時 (以分鐘為單位)。 預設值是 120 分鐘。

**EnableTestConnectionDetailedErrors**  
指出當使用者使用報表伺服器來測試資料來源連線時，是否要將詳細的錯誤訊息傳送至用戶端電腦。 預設值為 **true**。 如果此選項設定為 **false**，就只會傳送一般錯誤訊息。

## <a name="see-also"></a>另請參閱

[設定報表伺服器屬性 &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[連接至 Management Studio 中的報表伺服器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Reporting Services 屬性](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Management Studio F1 說明中的報表伺服器](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[報表伺服器系統屬性](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[編寫部署和管理工作的指令碼](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[啟用與停用我的報表](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
