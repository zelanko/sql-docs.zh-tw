---
title: "系統設定 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Master Data Services, system settings
- system settings [Master Data Services]
ms.assetid: 83075cdf-f059-4646-8ba2-19be8202f130
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5f82834be298872df88b00bda5d8184d179ab2a
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/05/2018
---
# <a name="system-settings-master-data-services"></a>系統設定 (Master Data Services)
  針對與 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫相關聯的所有 Web 應用程式和 Web 服務，您可以設定系統設定。  
  
 這些設定中有許多都是可在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 的 [資料庫] 頁面上設定。 有些設定可在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的 [系統設定] 資料表 (mdm.tblSystemSetting) 中設定。  
  
 這些設定會依下列類別目錄分組：  
  
-   [一般設定](#General)  
  
-   [版本管理設定](#Versions)  
  
-   [暫存設定](#Staging)  
  
-   [總管設定](#Explorer)  
  
-   [Excel 增益集設定](#xls)  
  
-   [商務規則設定](#BusinessRules)  
  
-   [通知設定](#Notifications)  
  
-   [安全性設定](#Security)  
  
-   [未使用](#NotUsed)  
  
##  <a name="General"></a> 一般設定  
  
|組態管理員設定|系統設定|描述|  
|-----------------------------------|--------------------|-----------------|  
|**資料庫連接逾時**|**DatabaseConnectionTimeOut**|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫允許連接完成的秒數。 如果連接未在此時間內完成，則會取消連接並傳回錯誤。 預設值為 **60** 秒 (1 分鐘)。|  
|**資料庫命令逾時**|**DatabaseCommandTimeOut**|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫允許命令完成的秒數。 如果命令未在此時間內完成，則會取消命令並傳回錯誤。 預設值為 **3600** 秒 (60 分鐘)。|  
|**Web 服務逾時**|**ServerTimeOut**|ASP.NET 允許 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 頁面要求完成的秒數。 如果要求未在此時間內完成，則會取消要求並傳回錯誤。 預設值為 **120000** 秒 (2000 分鐘)。|  
|**用戶端逾時**|**ClientTimeOut**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 返回到首頁之前非使用狀態的秒數。 預設值為 **300** 秒 (5 分鐘)。|  
|**每批次的資料列數目**|**RowsPerBatch**|Web 服務傳回之每個批次中所要擷取的記錄數目。 預設值為 **50**。|  
||**ApplicationName**|事件記錄檔中顯示的文字。 預設值為 **MDM**。|  
||**SiteTitle**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 瀏覽器標題列中顯示的文字。 預設值為 [主資料管理員]。|  
|**記錄保留 (天)**|**LogRentionDays**|記錄的保留天數。 預設值為 -1，表示不會清除記錄檔資料表。<br /><br /> 若值為 0，則只保留當天資料的記錄資料表。 且會截斷前一天的資料記錄。<br /><br /> 若值大於 0，記錄資料保留的天數由值指定。|  
  
##  <a name="Versions"></a> 版本管理設定  
  
|組態管理員設定|系統設定|描述|  
|-----------------------------------|--------------------|-----------------|  
|**僅複製認可的版本**|**CopyOnlyCommittedVersion**|在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中，決定使用者是否可以複製狀態為 [已認可] 的模型版本，或是複製任何狀態的版本。 預設值是 [是] 或 **1**，表示使用者只能複製 [已認可] 的版本。 變更為 [否] 或 **2** 則會允許使用者複製所有版本。|  
  
 如需詳細資訊，請參閱[版本 &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)。  
  
##  <a name="Staging"></a> 暫存設定  
  
|組態管理員設定|系統設定|描述|  
|-----------------------------------|--------------------|-----------------|  
|**記錄所有暫存交易**|**StagingTransactionLogging**|僅適用於 SQL Server 2008 R2。 決定在將暫存記錄載入 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫時，是否要記錄交易。 預設值是 [關閉] 或 **2**。 變更為 [開啟] 或 **1** 則會開啟記錄功能。|  
|**暫存批次間隔**|**StagingBatchInterval**|在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] [整合管理] 功能區域中，從選取 [啟動批次] 後到開始處理批次前所經過的秒數。 預設值為 **60** 秒 (1 分鐘)。|  
  
 如需詳細資訊，請參閱[概觀︰從資料表匯入資料 &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)。  
  
##  <a name="Explorer"></a> 總管設定  
  
|組態管理員設定|系統設定|描述|  
|-----------------------------------|--------------------|-----------------|  
|**階層中預設的成員數目**|**HierarchyChildNodeLimit**|在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 總管功能區域中，於顯示 […其他…] 之前，每個階層節點中所顯示的成員數目上限。 就會出現。 您可以按一下 […更多…] 來顯示下一個成員群組。 預設值為 **50**。|  
|**顯示階層中預設的名稱**|**ShowNamesInHierarchy**|在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 總管功能區域中，決定檢視階層時所選取的預設設定。<br /><br /> 預設值是 [是] 或 **1**，表示每個成員的名稱和程式碼都會顯示。 變更為 [否] 或 **2** 則只會顯示程式碼。|  
|**清單中網域屬性的數目**|**DBAListRowLimit**|在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 總管功能區域中，當您按兩下方格中的網域屬性值時所顯示的屬性數目。 預設值為 **50**。 如果有超過 50 個成員存在，則會改為顯示可搜尋對話方塊。|  
||**GridFilterDefaultFuzzySimilarityLevel**|在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 總管功能區域中，使用 [比對] 篩選準則時所使用的相似度層級。 預設值為 **0.3**。 設定的值愈接近 **1** ，傳回的相符項目就愈接近搜尋準則。 設定成 **1** 則會傳回完全相符的項目。|  
  
##  <a name="xls"></a> Excel 增益集設定  
  
|組態管理員設定|系統設定|描述|  
|-----------------------------------|--------------------|-----------------|  
|在網站首頁上顯示 Excel 增益集的文字|ShowAddInText|在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，顯示讓使用者下載 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]的連結。|  
|網站首頁 Excel 增益集的安裝路徑|AddInURL|在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，如果顯示指向 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 的連結，則是使用者按一下連結之後前往的位置。|  
  
##  <a name="BusinessRules"></a> 商務規則設定  
  
|組態管理員設定|系統設定|描述|  
|-----------------------------------|--------------------|-----------------|  
|**要遞增新商務規則的數目依據**|**BusinessRuleDefaultPriorityIncrement**|在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] [系統管理] 功能區域中，每個新商務規則之優先順序遞增的數目。 預設值為 **10**。|  
|**要套用商務規則的成員數目**|**BusinessRuleRealtimeMemberCount**|在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 總管功能區域中，方格中要套用商務規則的成員數目上限。 在 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 中，使用中工作表中要套用商務規則的成員數目上限。 預設值為 **10000**。|  
  
 如需詳細資訊，請參閱[商務規則 &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)。  
  
##  <a name="Notifications"></a> 通知設定  
  
|組態管理員設定|系統設定|描述|  
|-----------------------------------|--------------------|-----------------|  
|**通知的主資料管理員 URL**|**MDMRootURL**|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式的 URL，其為電子郵件通知中所用的連結，例如 `http://constoso/mds`。|  
|**通知電子郵件間隔**|**NotificationInterval**|傳送電子郵件的頻率 (以秒為單位)。 預設值為 **120** 秒 (2 分鐘)。|  
|**單一電子郵件中的通知數**|**NotificationsPerEmail**|將在單一通知電子郵件中列出的驗證問題最大數目。 如果存在其他問題，則這些問題將不包含在該電子郵件中，但會在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中提供。|  
|**預設電子郵件格式**|**EmailFormat**|所有電子郵件通知的格式。 預設值是 **HTML** 或 **1**。 資料庫設定 **2** 表示 [文字]。<br /><br /> 注意：您可以在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中覆寫個別使用者的此項目，方式為在使用者的 [一般] 索引標籤上變更並儲存 [電子郵件格式]。|  
|**電子郵件地址的規則運算式**|**EmailRegExPattern**|在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] [使用者及群組的權限] 功能區域中，用來驗證在使用者 [一般] 索引標籤上輸入之電子郵件地址的規則運算式。如需規則運算式的詳細資訊，請參閱 MSDN Library 中的[規則運算式語言項目](http://go.microsoft.com/fwlink/?LinkId=164401)。|  
|**Database Mail 帳戶**|**EmailProfilePrincipalAccount**|顯示傳送電子郵件通知時所要使用的 Database Mail 帳戶。 預設的設定檔是 **mds_email_user**。|  
|**Database Mail 設定檔**|**DatabaseMailProfile**|傳送電子郵件通知時所要使用的 Database Mail 設定檔。 預設值是空白。|  
||**ValidationIssueHTML**|當商務規則驗證失敗時，使用者所取得 HTML 格式的電子郵件文字。|  
||**ValidationIssueText**|當商務規則驗證失敗時，使用者所取得純文字格式的電子郵件文字。|  
||**VersionStatusChangeText**|當版本狀態變更時，使用者所取得純文字格式的電子郵件文字。 只有具有整個模型之 [更新] 權限的使用者才會收到此電子郵件。|  
||**VersionStatusChangeHTML**|當版本狀態變更時，使用者所取得 HTML 格式的電子郵件文字。 只有具有整個模型之 [更新] 權限的使用者才會收到此電子郵件。|  
  
 如需詳細資訊，請參閱[通知 &#40;Master Data Services&#41;](../master-data-services/notifications-master-data-services.md)。  
  
##  <a name="Security"></a> 安全性設定  
  
|組態管理員設定|系統設定|描述|  
|-----------------------------------|--------------------|-----------------|  
||**SecurityMemberProcessInterval**|在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] [使用者及群組的權限] 功能區域中，[階層成員] 索引標籤上設定之使用者和群組權限的套用頻率 (以秒為單位)。 預設值為 **3600** 秒 (60 分鐘)。|  
  
 如需詳細資訊，請參閱[立即套用成員權限 &#40;Master Data Services&#41;](../master-data-services/immediately-apply-member-permissions-master-data-services.md)。  
  
##  <a name="NotUsed"></a> 未使用  
 [系統設定] 資料表中不使用下列設定。  
  
-   **SecurityMode**  
  
-   **MDSHubName**  
  
-   **ApplicationLogging**  
  
-   **ReportServer**  
  
-   **ReportDirectory**  
  
-   **BusinessRuleEngineIterationLimit**  
  
-   **BusinessRuleExtensibility**  
  
-   **AttributeExplorerMarkAllActionMemberCount**  
  
## <a name="see-also"></a>另請參閱  
 [資料庫物件安全性 &#40;Master Data Services&#41;](../master-data-services/database-object-security-master-data-services.md)  
  
  
