---
title: 伺服器屬性進階頁面 | Microsoft Docs
description: 您可以使用進階伺服器屬性頁面來設定報表伺服器的系統屬性。 這項工具提供圖形化使用者介面，如此您不需要撰寫程式碼就可以設定屬性。
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.date: 01/28/2020
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: d1bfbb7a1abb13df05ce402fa79a1598ee04ca1f
ms.sourcegitcommit: cf8db6330be0d89bbec362e4c7e187b5461026f0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/06/2020
ms.locfileid: "77054841"
---
# <a name="server-properties-advanced-page---power-bi-report-server--reporting-services"></a>伺服器屬性進階頁面 - Power BI 報表伺服器和 Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

您可以使用這個頁面來設定報表伺服器的系統屬性。 有許多方式可設定系統屬性。 這項工具提供了圖形化使用者介面，如此您不需要撰寫程式碼就可以設定屬性。

若要開啟此頁面，請啟動 SQL Server Management Studio，並連線至報表伺服器執行個體，然後以滑鼠右鍵按一下報表伺服器名稱，再選取 [屬性]  。 選取 [進階]  ，即可開啟此頁面。

## <a name="options"></a>選項。

### <a name="accesscontrolallowcredentials"></a>AccessControlAllowCredentials
(僅限 Power BI 報表伺服器、Reporting Services 2017 及更新版本) 指出當 `credentials` 旗標設定為 True 時，是否可以公開用戶端要求的回應。 預設值為 **false**。

### <a name="accesscontrolallowheaders"></a>AccessControlAllowHeaders
(僅限 Power BI 報表伺服器、Reporting Services 2017 及更新版本) 伺服器在用戶端提出要求時允許的標頭清單 (以逗號分隔)。 這個屬性可以是空字串，而指定 * 將允許所有標題。

### <a name="accesscontrolallowmethods"></a>AccessControlAllowMethods
(僅限 Power BI 報表伺服器、Reporting Services 2017 及更新版本) 伺服器在用戶端提出要求時允許的 HTTP 方法清單 (以逗號分隔)。 預設值為 (GET、PUT、POST、PATCH、DELETE)，而指定 * 將允許所有方法。

### <a name="accesscontrolalloworigin"></a>AccessControlAllowOrigin
(僅限 Power BI 報表伺服器、Reporting Services 2017 及更新版本) 伺服器在用戶端提出要求時允許的來源清單 (以逗號分隔)。 預設值是可防止所有要求的空白，而指定 * 將在未設定認證時允許所有來源；如果指定認證，則必須指定明確的來源清單。

### <a name="accesscontrolexposeheaders"></a>AccessControlExposeHeaders
(僅限 Power BI 報表伺服器、Reporting Services 2017 及更新版本) 伺服器會向用戶端公開的標頭清單 (以逗號分隔)。 預設值是空白。

### <a name="accesscontrolmaxage"></a>AccessControlMaxAge
(僅限 Power BI 報表伺服器、Reporting Services 2017 及更新版本) 指定可快取預檢要求結果的秒數。 預設值為 600 (10 分鐘)。

### <a name="allowedresourceextensionsforupload"></a>AllowedResourceExtensionsForUpload
(僅限 Power BI 報表伺服器、Reporting Services 2017 及更新版本) 設定可上傳到報表伺服器的資源副檔名。 不需要包含內建檔案類型的副檔名，例如 &ast;.rdl 和 &ast;.pbix。 預設為「&ast;、&ast;.xml、&ast;.xsd、&ast;.xsl、&ast;.png、&ast;.gif、&ast;.jpg、&ast;.tif、&ast;.jpeg、&ast;.tiff、&ast;.bmp、&ast;.pdf、&ast;.svg、&ast;.rtf、&ast;.txt、&ast;.doc、&ast;.docx、&ast;.pps、&ast;.ppt、&ast;.pptx」。

### <a name="customheaders"></a>CustomHeaders 

(僅限 Power BI 報表伺服器 2020 年 1 月、Reporting Services 2019 及更新版本)

設定所有符合指定 regex 模式的 URL 標頭值。 使用者可以使用有效的 XML 來更新 CustomHeaders 值，以設定所選要求 URL 的標頭值。 系統管理員可以在 XML 中新增任意數量的標頭。 根據預設，不會有任何自訂標頭，且值為空白。 

> [!NOTE]
> 太多標頭可能會影響效能。 

我們建議您驗證拓撲的組態，以確保標頭集與您的 Reporting Services 部署相容。 如果瀏覽器也不具有適當的設定，則選擇的設定可能會在瀏覽器中造成錯誤。 例如，如果您的伺服器未設定為使用 https，則不應新增 HSTS 組態。 不相容的標頭可能會導致瀏覽器轉譯錯誤。

#### <a name="customheaders-xml-format"></a>CustomHeaders XML 格式

```xml
<CustomHeaders>
    <Header>
        <Name>{Name of the header}</Name>
        <Pattern>{Regex pattern to match URLs}</Pattern>
        <Value>{Value of the header}</Value>
    </Header>
</CustomHeaders>
```

#### <a name="setting-the-customheaders-property"></a>設定 CustomHeaders 屬性

- 您可以使用 [SetSystemProperties](https://docs.microsoft.com/dotnet/api/reportservice2010.reportingservice2010.setsystemproperties) SOAP 端點傳遞 CustomHeaders 屬性作為參數，以設定此屬性。
- 您可以使用 REST 端點 [UpdateSystemProperties](https://app.swaggerhub.com/apis/microsoft-rs/PBIRS/2.0#/System/UpdateSystemProperties)：`/System/Properties` 傳遞 CustomHeaders 屬性

#### <a name="example"></a>範例

下列範例顯示如何針對具有相符 regex 模式的 URL 來設定 HSTS 和其他自訂標頭。

```xml
<CustomHeaders>
    <Header>
        <Name>Strict-Transport-Security</Name>
        <Pattern>\/Reports\/mobilereport</Pattern>
        <Value>max-age=86400</Value>
    </Header>
    <Header>
        <Name>Embed</Name>
        <Pattern>(.+)(/reports/)(.+)(rs:embed=true)</Pattern>
        <Value>True</Value>
    </Header>
</CustomHeaders>
```

上述 XML 中的第一個標頭，會將 `Strict-Transport-Security: max-age=86400` 標頭新增至相符的要求。
- http://adventureworks/Reports/mobilereport/New%20Mobile%20Report - Regex 相符且將設定 HSTS 標頭
- http://adventureworks/ReportServer/mobilereport/New%20Mobile%20Report - 不相符

上述 XML 中第二個標頭會新增 URL 的 `Embed: True` 標頭，其中包含 `/reports/` 和 `rs:embed=true` 查詢參數。
- https://adventureworks/reports/mobilereport/New%20Mobile%20Report?rs:embed=true - 相符
- https://adventureworks/reports/mobilereport/New%20Mobile%20Report?rs:embed=false - 不相符

### <a name="editsessioncachelimit"></a>EditSessionCacheLimit
指定可以在報表編輯工作階段中使用的資料快取項目數目。 預設數目是 5。  

### <a name="editsessiontimeout"></a>EditSessionTimeout
指定報表編輯工作階段逾時之前的秒數。預設值為 7200 秒 (兩小時)。 

### <a name="enablecdnvisuals"></a>EnableCDNVisuals 
(僅限 Power BI 報表伺服器) 啟用時，Power BI 報表會從由 Microsoft 所裝載內容傳遞網路 (CDN) 載入最新認證的自訂視覺效果。 如果您的伺服器沒有網際網路資源存取權，則可以關閉此選項。 在此情況下，自訂視覺效果會從已發佈至伺服器的報表載入。 預設值為 **True**。  

###  <a name="enableclientprinting"></a>EnableClientPrinting  
決定是否可從報表伺服器下載 RSClientPrint ActiveX 控制項。 有效值為 **true** 和 **false**。 預設值為 **true**。 如需此控制項所需之其他設定的詳細資訊，請參閱 [啟用和停用 Reporting Services 的用戶端列印功能](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)。  

### <a name="enablecustomvisuals"></a>EnableCustomVisuals 
(僅限 Power BI 報表伺服器) 啟用 Power BI 自訂視覺效果的顯示。 值為 True/False。 *預設值為 True。*  

###  <a name="enableexecutionlogging"></a>EnableExecutionLogging  
指出報表執行記錄是否已啟用。 預設值為 **true**。 如需報表伺服器執行記錄的詳細資訊，請參閱 [報表伺服器執行記錄和 ExecutionLog3 檢視](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)。  

### <a name="enableintegratedsecurity"></a>EnableIntegratedSecurity
決定報表資料來源連線是否支援 Windows 整合式安全性。 預設值為 **True**。 有效值如下：

|值|描述|
|---------|---------|
|**True**|已啟用 Windows 整合式安全性。|
|**False**|未啟用 Windows 整合式安全性。 設定為使用 Windows 整合式安全性的報表資料來源不會執行。|

### <a name="enableloadreportdefinition"></a>EnableLoadReportDefinition
選取此選項，指定使用者是否可以從報表產生器報表執行未規劃的報表執行。 設定這個選項會針對報表伺服器決定 **EnableLoadReportDefinition** 屬性的值。  

如果您清除此選項，屬性會設為 False。 報表伺服器將不會針對使用報表模型作為資料來源的報表產生點選連結報表。 LoadReportDefinition 方法的任何呼叫都會遭封鎖。  

關閉此選項可減少惡意使用者利用 LoadReportDefinition 要求讓報表伺服器超過負載，藉以啟動阻斷服務攻擊的威脅。  

### <a name="enablemyreports"></a>EnableMyReports  
指出 [我的報表] 功能是否已啟用。 值若為 **true** 表示此功能已啟用。  

### <a name="enablepowerbireportexportdata"></a>EnablePowerBIReportExportData 
(僅限 Power BI 報表伺服器) 啟用從 Power BI 視覺效果的 Power BI 報表伺服器資料匯出。 值為 True、False。  預設值是 True。 

### <a name="enablepowerbireportexportunderlyingdata"></a>EnablePowerBIReportExportUnderlyingData 
(僅限 Power BI 報表伺服器) 指出客戶是否可以從 Power BI 報表伺服器上的 Power BI 視覺效果匯出基礎資料。 值若為 true 表示此功能已啟用。

### <a name="enableremoteerrors"></a>EnableRemoteErrors
包含外部錯誤資訊 (例如，有關報表資料來源的錯誤資訊) 以及針對從遠端電腦要求報表之使用者傳回的錯誤訊息。 有效值為 **true** 和 **false**。 預設值為 **false**。 如需詳細資訊，請參閱[啟用遠端錯誤 &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md)。  

### <a name="enabletestconnectiondetailederrors"></a>EnableTestConnectionDetailedErrors
指出當使用者使用報表伺服器來測試資料來源連線時，是否要將詳細的錯誤訊息傳送至用戶端電腦。 預設值為 **true**。 如果此選項設定為 **false**，就只會傳送一般錯誤訊息。

###  <a name="executionlogdayskept"></a>ExecutionLogDaysKept  
要將報表執行資訊保留在執行記錄中的天數。 這個屬性的有效值包括 **-1** 至 **2**、**147**、**483**和**647**。 如果此值為 **-1**，系統不會從執行記錄資料表中刪除項目。 預設值是 **60**秒。  

> [!NOTE]
> 將值設定為 **0** 會「刪除」  執行記錄中的所有項目。 **-1** 值會保留執行記錄的項目，且不會將其刪除。

### <a name="executionloglevel"></a>ExecutionLogLevel
設定執行記錄層級。 *預設值為「標準」。*

### <a name="externalimagestimeout"></a>ExternalImagesTimeout
決定在連接逾時之前必須擷取外部影像檔的時間長度。預設值為 **600** 秒。  

### <a name="interprocesstimeoutminutes"></a>InterProcessTimeoutMinutes
(僅限 Power BI 報表伺服器、Reporting Services 2019 及更新版本) 設定程序逾時 (以分鐘為單位)。 *預設值為 30。*

### <a name="maxfilesizemb"></a>MaxFileSizeMb
設定報表的最大檔案大小 (以 MB 為單位)。 *預設值為 1000。最大值為 2000。*

### <a name="modelcleanupcycleminutes"></a>ModelCleanupCycleMinutes 
(僅限 Power BI 報表伺服器) 設定頻率以檢查記憶體中未使用的模型 (以分鐘為單位)。 *預設值為 15。*

### <a name="modelexpirationminutes"></a>ModelExpirationMinutes 
(僅限 Power BI 報表伺服器) 設定未使用模型從記憶體收回的頻率 (以分鐘為單位)。 *預設值為 60。*

###  <a name="myreportsrole"></a>MyReportsRole  
在使用者之 [我的報表] 資料夾上建立安全性原則時所使用的角色名稱。 預設值是 **My Reports Role**秒。  

### <a name="officeaccesstokenexpirationseconds"></a>OfficeAccessTokenExpirationSeconds 
(僅限 Power BI 報表伺服器、Reporting Services 2019 及更新版本) 設定您要 Office 存取權杖多久到期 (以秒為單位)。 *預設值為 60。*

### <a name="officeonlinediscoveryurl"></a>OfficeOnlineDiscoveryURL 
(僅限 Power BI 報表伺服器) 設定 Office Online Server 執行個體的位址以檢視 Excel 活頁簿。

### <a name="rdlxreporttimetout"></a>RDLXReportTimetout
RDLX 報表 *(SharePoint Server 中的 Power View 報表)* 報表伺服器命名空間中所有受控報表的預設報表處理逾時值 (以秒為單位)。 在報表層級可以覆寫這個值。 如果已設定此屬性，當指定的時間已過期時，報表伺服器就會嘗試停止處理報表。 有效值是 **-1** 到 **2**,**147**,**483**,**647**。 如果此值為 **-1**，命名空間中的報表就不會在處理期間逾時。 預設值是 **1800**秒。

### <a name="requireintune"></a>RequireIntune
(僅限 Power BI 報表伺服器、Reporting Services 2017 及更新版本) 需要 Intune 透過 Power BI 行動應用程式來存取您組織的報表。 *預設值為 False。*

### <a name="restrictedresourcemimetypeforupload"></a>RestrictedResourceMimeTypeForUpload
(僅限 Power BI 報表伺服器 2019 年 1 月、Reporting Services 2017 及更新版本) 不允許使用者用來上傳內容的 mime 類型集合。 已經使用受限 mime 類型來儲存的任何資源，只能下載為 application/octet-stream，而無法由瀏覽器開啟或執行。  根據預設，此清單中沒有任何受限的項目，但我們建議組織將其填入以提供最安全的體驗。

### <a name="schedulerefreshtimeoutminutes"></a>ScheduleRefreshTimeoutMinutes 
(僅限 Power Bi 報表伺服器) 在含內嵌 AS 模型的 PowerBI 報表上排定重新整理的資料重新整理逾時 (以分鐘為單位)。 預設值是 120 分鐘。

### <a name="sessiontimeout"></a>SessionTimeout
工作階段維持作用中狀態的時間長度 (以秒為單位)。 預設值是 **600**秒。  

### <a name="sharepointintegratedmode"></a>SharePointIntegratedMode
此唯讀屬性指出伺服器模式。 如果此值為 False，報表伺服器就會以原生模式執行。  

### <a name="showdownloadmenu"></a>ShowDownloadMenu
(僅限 Power BI 報表伺服器、Reporting Services 2017 及更新版本) 啟用用戶端工具下載功能表。 *預設值為 true。*

### <a name="sitename"></a>SiteName
顯示在入口網站頁面標題中的報表伺服器網站名稱。 預設值為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 這個屬性可以是空字串。 最大長度是 8,000 個字元。  

### <a name="snapshotcompression"></a>SnapshotCompression
定義快照集的壓縮方式。 預設值是 **SQL**秒。 有效值如下：

|值|描述|
|---------|---------|
|**SQL**|快照集在儲存於報表伺服器資料庫時會進行壓縮。 此壓縮為目前的行為。|
|**None**|系統不會壓縮快照集。|
|**全部**|系統會針對所有儲存選項壓縮快照集，包括報表伺服器資料庫或是檔案系統。|

### <a name="storedparameterslifetime"></a>StoredParametersLifetime
指定預存參數可儲存的最大天數。 有效值是 **-1**、 **+1** 到 **2,147,483,647**。 預設值為 **180** 天。  

### <a name="storedparametersthreshold"></a>StoredParametersThreshold
指定報表伺服器可儲存的最大參數值數目。 有效值是 **-1**、 **+1** 到 **2,147,483,647**。 預設值是 **1500**秒。  

### <a name="supportedhyperlinkschemes"></a>SupportedHyperlinkSchemes 
(僅限 Power BI 報表伺服器 2019 年 1 月、Reporting Services 2019 及更新版本)：設定可在超連結動作上定義以便轉譯的 URI 配置清單 (以逗號分隔)，或 “&ast;” 以啟用所有超連結配置。 例如，設定 “http,https” 會允許 “https://www. contoso.com” 的超連結，但會移除 “mailto:bill@contoso.com” 或 “javascript:window.open(‘ www.contoso.com’, ‘_blank’)” 的超連結。 預設為 “&ast;”。

### <a name="systemreporttimeout"></a>SystemReportTimeout
在報表伺服器命名空間中管理之所有報表的預設報表處理逾時值 (以秒為單位)。 在報表層級可以覆寫這個值。 如果已設定此屬性，當指定的時間已過期時，報表伺服器就會嘗試停止處理報表。 有效值是 **-1** 到 **2**,**147**,**483**,**647**。 如果此值為 **-1**，命名空間中的報表就不會在處理期間逾時。 預設值是 **1800**秒。  

### <a name="systemsnapshotlimit"></a>SystemSnapshotLimit
針對報表所儲存之快照集的最大數目。 有效值是 **-1** 到 **2**,**147**,**483**,**647**。 如果此值為 **-1**，表示沒有任何快照集限制。  

### <a name="timerinitialdelayseconds"></a>TimerInitialDelaySeconds
(僅限 Power BI 報表伺服器、Reporting Services 2017 及更新版本) 設定要初始時間延遲多久 (以秒為單位)。 *預設值為 60。*

### <a name="trustedfileformat"></a>TrustedFileFormat
(僅限 Power BI 報表伺服器、Reporting Services 2017 及更新版本) 設定在 Reporting Services 入口網站之下，所有要在瀏覽器中開啟的外部檔案格式。 未列出的外部檔案格式會在瀏覽器中提示下載選項。 預設值為 jpg、jpeg、jpe、wav、bmp、pdf、img、gif、json、mp4、web、png。

### <a name="usesessioncookies"></a>UseSessionCookies
指出報表伺服器與用戶端瀏覽器通訊時是否應該使用工作階段 Cookie。 預設值為 **true**。  

## <a name="see-also"></a>另請參閱

[設定報表伺服器屬性 &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[連接至 Management Studio 中的報表伺服器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Reporting Services 屬性](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Management Studio F1 說明中的報表伺服器](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[報表伺服器系統屬性](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[編寫部署和管理工作的指令碼](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[啟用與停用我的報表](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
