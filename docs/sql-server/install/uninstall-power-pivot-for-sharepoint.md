---
title: "解除安裝 Power Pivot for SharePoint | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: install
ms.prod_service: sql-non-specified
ms.service: database-engine
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3941a2f0-0d0c-4d1a-8618-7a6a7751beac
caps.latest.revision: "27"
author: MikeRayMSFT
ms.author: mikeray
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1beb1d390a12ccbfe19d7a8c17f9f862d2b05dd6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="uninstall-power-pivot-for-sharepoint"></a>解除安裝 PowerPivot for SharePoint
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 解除安裝 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安裝是一個多步驟的作業，其中包括準備解除安裝、從伺服器陣列移除功能和方案，以及移除程式檔案與登錄設定。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **本主題內容：**  
  
-   [必要條件](#prereq)  
  
-   [步驟 1：解除安裝前的檢查清單](#bkmk_before)  
  
-   [步驟 2：從 SharePoint 移除功能和方案](#bkmk_remove)  
  
-   [步驟 3：執行 SQL Server 安裝程式以便從本機電腦移除程式](#bkmk_uninstall)  
  
-   [步驟 4：解除安裝 PowerPivot for SharePoint 增益集](#bkmk_addin)  
  
-   [步驟 5：確認解除安裝](#verify)  
  
-   [步驟 6：解除安裝後的檢查清單](#bkmk_post)  
  
##  <a name="prereq"></a> 必要條件  
  
-   您必須是 SharePoint 伺服器陣列管理員或服務應用程式管理員，才能解除安裝伺服器陣列中的功能和方案。  
  
-   如果您要一併解除安裝 Database Engine，則必須是 SQL Server 系統管理員和本機 Administrators 群組的成員。  
  
-   您必須是 Analysis Services 系統管理員和本機 Administrators 群組的成員，才能解除安裝 Analysis Services 和 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]。  
  
##  <a name="bkmk_before"></a> 步驟 1：解除安裝前的檢查清單  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 一旦支援查詢及資料處理的軟體從伺服器陣列中移除之後，就會停用資料存取。 因此第一步，您必須先刪除不再運作的檔案及文件庫。 此動作有助於解決解除安裝此軟體之前所發生任何有關「資料遺失」的問題。  
  
1.  刪除所有與 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安裝有關的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿、文件及文件庫。 此軟體一經解除安裝，所有文件庫及文件皆無法再行運作。  
  
    -   [刪除 Power Pivot 圖庫](../../analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery.md)  
  
    -   [刪除 Power Pivot 資料摘要庫](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)  
  
2.  刪除其他包含或參考 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料之文件庫內的 Excel 活頁簿或 Reporting Services 報表。  
  
3.  移除 PerformancePoint 儀表板中任何參考 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的網頁組件。  
  
4.  檢視現有網站及文件庫的 SharePoint 權限，確認有無需要變更。 某些 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料存取案例 (特別是透過 URL 連接字串對其他活頁簿中之 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料所進行的次要資料存取) 會需要高於「檢視」權限 (此權限通常會指派給只瀏覽網站的 SharePoint 使用者) 的「讀取」權限。 您若是不再需要「讀取」權限，可以視情況降低權限。  
  
5.  您也可選擇停止服務，然後等候數日之後再解除安裝此軟體。 這不是解除安裝的必要步驟，但可以讓您在解決先前未完全解決的資料移轉或技術代換問題時，暫時恢復服務。  
  
##  <a name="bkmk_remove"></a> 步驟 2：從 SharePoint 移除功能和方案  
 使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 組態工具，從 SharePoint 中移除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務和應用程式。  
  
-   您必須是伺服器陣列管理員、Analysis Services 執行個體的伺服器管理員，以及伺服器陣列組態資料庫的 **db_owner** 。  
  
-   請針對 SharePoint 版本使用適當版本的組態工具。 請勿將其中任何一個工具用於 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 安裝。  
  
-   確認 SharePoint Administration Service 正在執行中。  
  
1.  **執行組態工具：** 請注意，只有當 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安裝在本機伺服器上時，才會列出組態工具。請在 **[開始]** 功能表上，指向 **[所有程式]**，依序按一下 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[組態工具]**，然後按一下下列其中一項：  
  
    -   **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 組態**  
  
    -   **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 組態工具**  
  
2.  選取 **[移除功能、服務、應用程式和方案]** ，然後按一下 **[確定]**。  
  
3.  或者，將視窗展開為全螢幕。 您應該會在視窗底部看到一個按鈕列，其中包含 **[驗證]**、 **[執行]**和 **[結束]** 命令。  
  
4.  檢閱工作清單中的每個動作以了解每個動作的用途。  
  
     在 [移除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式] 中，您可以選擇刪除與服務應用程式相關聯的應用程式資料。 應用程式資料是使用服務應用程式建立的 SQL Server 資料庫，用於儲存資料重新整理排程、資料庫執行個體資訊、使用量資料，以及 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 所使用的其他資料。 它不會儲存使用者檔案，例如 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿。 除非您有保留應用程式資料的特定原因 (例如，如果您有與資料重新整理或資料存取相關的資料保留原則)，您才可以在不移除 SharePoint 使用者所建立或儲存之任何檔案的情況下刪除應用程式資料庫。  
  
     若要刪除資料庫，請選取 [移除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式]，然後選取 [刪除與這個服務應用程式關聯的應用程式資料]。  
  
5.  或者，在 **[輸出]** 索引標籤或 **[指令碼]** 索引標籤中檢閱詳細資訊。  
  
     [輸出] 索引標籤是此工具即將執行之動作的摘要。 此資訊會儲存在記錄檔中：  
  
     `C:\Program Files\Microsoft SQL Server\130\Tools\PowerPivotTools\SPAddinConfiguration\Log`  
  
     [指令碼] 索引標籤會顯示 PowerShell 指令程式，或參考此工具將執行的 PowerShell 指令碼檔案。  
  
6.  按一下 **[驗證]** 來檢查每個動作是否有效。 如果無法使用 **[驗證]** ，表示所有動作都適用於您的系統。  
  
7.  按一下 **[執行]** ，執行適用於此工作的所有動作。 只有在通過驗證檢查的情況下，才可以使用**[執行]** 。 當您按一下 **[執行]**時，會出現下列警告，提醒您動作是在批次模式下處理：「工具中標示為有效的所有組態設定都會套用到 SharePoint 伺服器陣列。 您要繼續嗎?」  
  
8.  按一下 **[是]** 繼續。  
  
 **疑難排解錯誤：**  
  
 您可以在組態工具的 [參數] 窗格中檢視每個動作的錯誤資訊。 針對與方案部署或撤銷相關的問題，請確認已啟動 SharePoint Administration 服務。 此服務會執行觸發伺服器陣列中組態變更的計時器作業。 如果該服務未執行，方案部署或撤銷將會失敗。 持續性錯誤指的是現有的部署或撤銷作業已經在佇列中，因此會攔截組態工具的其他動作。 您可以使用下列 PowerShell 命令來確認服務正在執行中。  
  
```  
Get-Service | where {$_.displayname -like "*sharepoint* administration*"}  
```  
  
 若要尋找並移除已經在佇列中的部署或撤銷作業，請執行下列操作：  
  
1.  至於其他所有錯誤，請檢查 ULS 記錄檔。 如需詳細資訊，請參閱[設定及檢視 SharePoint 記錄檔與診斷記錄 &#40;Power Pivot for SharePoint&#41;](~/analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)。  
  
2.  以管理員身分啟動 SharePoint 管理命令介面，然後執行下列命令來檢視佇列中的作業：  
  
    ```  
    Stsadm –o enumdeployments  
    ```  
  
3.  檢閱現有部署中的下列資訊： **[類型]** 是 [撤銷] 或 [部署]、 **[檔案]** 是 powerpivotwebapp.wsp 或 powerpivotfarm.wsp。  
  
4.  若是與 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 方案相關的部署或撤銷，請複製 **JobId** 的 GUID 值，然後將其貼入下列命令 (使用命令介面之 [編輯] 功能表上的 [標記]、[複製] 和 [貼上] 命令來複製 GUID)：  
  
    ```  
    Stsadm –o canceldeployment –id “<GUID>”  
    ```  
  
5.  依序按一下 **[驗證]** 和 **[執行]**，重試組態工具中的工作。  
  
 或者，您可以使用 PowerShell 從伺服器陣列移除功能和方案。 如需詳細資訊，請參閱 [Power Pivot for SharePoint 的 PowerShell 參考](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md)。  
  
##  <a name="bkmk_uninstall"></a> 步驟 3：執行 SQL Server 安裝程式以便從本機電腦移除程式  
 刪除程式檔案需要您執行 SQL Server 安裝程式來解除安裝軟體。 解除安裝會移除安裝程式所建立的檔案和登錄項目。 您可以使用 [程式和功能] 頁面解除安裝軟體。 安裝 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 是安裝 SQL Server 的一部分。  
  
 您可以解除安裝部分安裝，而不影響已安裝的其他 SQL Server 執行個體 (或同一個執行個體中的功能)。 例如，您可以解除安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，但保留安裝其他元件，例如 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或 Database Engine。  
  
1.  從程式清單中選取 [Microsoft SQL Server 2014 (64 位元)]。  
  
2.  按一下 [解除安裝/變更]。  
  
3.  按一下 **[移除]**。 隨即啟動 SQL Server 安裝程式。  
  
     您可以從安裝程式選取 [[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]] 執行個體，然後選取 [Analysis Services] 和 [Analysis Services SharePoint 整合] 只移除該功能，但保留其他所有功能。  
  
##  <a name="bkmk_addin"></a> 步驟 4：解除安裝 PowerPivot for SharePoint 增益集  
 如果您的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 部署包含兩部以上的伺服器，而且已安裝 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 增益集，請從 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 增益集安裝所在的每一部伺服器上解除安裝增益集，以便完整解除安裝所有 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 檔案。 如需詳細資訊，請參閱 [安裝或解除安裝 Power Pivot for SharePoint 增益集 &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)。  
  
##  <a name="verify"></a> 步驟 5：確認解除安裝  
  
1.  在管理中心的 [管理伺服器上的服務] 中，連接到您要解除安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 所在的伺服器。  
  
2.  -   如果您解除安裝 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013，請確認 [SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務] 不再出現於清單中。  
  
    -   如果您解除安裝 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010，請確認 [SQL Server Analysis Services] 和 [SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務] 都不再出現於清單中。  
  
3.  在伺服器陣列中解除安裝最後一部 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 伺服器之後，請執行下列操作：  
  
    1.  在 [應用程式管理] 的 [管理服務應用程式] 中，確認 [[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式] 不再出現於清單中。  
  
    2.  在 [系統設定] 的 [管理伺服器陣列功能] 中，確認 [[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 整合功能] 不再出現於頁面中。 在 [管理伺服器陣列方案] 中，確認 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 方案不再出現於頁面中。  
  
    3.  在 [監視] 的 [設定診斷記錄] 和 [設定 Usage and Health Data Collection] 中，確認 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 事件和事件類別目錄不再出現。  
  
    4.  在 [一般應用程式設定] 中，確認 [[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理儀表板] 不再出現於頁面中。  
  
##  <a name="bkmk_post"></a> 步驟 6：解除安裝後的檢查清單  
 使用下列清單移除解除安裝期間未刪除的軟體與檔案。  
  
1.  刪除 `C:\Program Files\Microsoft SQL Server\MSAS13.PowerPivot`中的所有資料檔和子資料夾，然後再刪除該資料夾。 此步驟也會刪除先前快取在 DATA 目錄中的檔案。  
  
2.  若還未刪除所有的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿、文件及文件庫，請執行此動作。  
  
    -   [刪除 Power Pivot 圖庫](../../analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery.md)  
  
    -   [刪除 Power Pivot 資料摘要庫](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)  
  
3.  在 Secure Store Service 中，刪除所有包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 所使用之預存認證的目標應用程式。 當您解除安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 時，就會刪除 Secure Store Service 中的某些項目，但不會全部刪除。 專為 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 無人看管的資料重新整理帳戶所建立的目標應用程式，以及所有您針對資料重新整理所建立的目標應用程式若仍然存在，應手動予以刪除。  
  
     相反地，由 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務自動產生的各種目標應用程式將會在解除安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 時自動刪除。  
  
4.  在 [控制台] 中，按一下 **[程式]**，然後按一下 **[解除安裝程式]** 解除安裝所有不再使用的 Analysis Services 用戶端程式庫。 當您解除安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 時，不會移除 Analysis Services ADOMD.NET 及 Microsoft SQL Server 分析管理物件。 由於其他使用 Analysis Services 資料的程式庫仍可能需要使用這些程式庫，因此 SQL Server 安裝程式不會自動解除安裝這些程式庫。 如果您不再需要這些用戶端程式庫，必須手動解除安裝它們。  
  
     除非疑難排解或安裝指示要求您解除安裝 SQL Server Reporting Services SharePoint 2010 增益集，否則請勿任意解除安裝。 Access Services 需要使用 Reporting Services 增益集。 此增益集由 SharePoint 產品準備工具所安裝，應繼續保留在系統上，以支援 SharePoint 所需要的功能。  
  
     請勿解除安裝 Analysis Services OLE DB 提供者。 由 SharePoint 所安裝的 OLE DB 提供者，是連接至 Analysis Services 資料庫之 Excel 活頁簿的必要條件。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 所安裝的版本較新，並具備回溯相容性，因此應保留在系統上，以避免日後發生資料連接問題。  
  
## <a name="see-also"></a>另請參閱  
 [安裝或解除安裝 Power Pivot for SharePoint 增益集 &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [Power Pivot 組態工具](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
  
