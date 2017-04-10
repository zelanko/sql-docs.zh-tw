---
title: "將 Power Pivot 移轉至 SharePoint 2013 | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f698ceb1-d53e-4717-a3a0-225b346760d0
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 18
---
# 將 Power Pivot 移轉至 SharePoint 2013
  
  
 SharePoint 2013 不支援就地升級。 不過，支援**資料庫附加升級**的程序。 此行為與升級至 SharePoint 2010 不同，後者的客戶可以在兩種基本升級方法中選擇：就地升級與資料庫附加升級。  
  
 如果您擁有與 SharePoint 2010 整合的 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 安裝，就無法就地升級 SharePoint 伺服器。 不過，您可以將內容資料庫和伺服器應用程式資料庫從 SharePoint 2010 伺服器陣列移轉至 SharePoint 2013 伺服器陣列。 本主題是完成資料庫附加升級以及完成 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 相關移轉所需步驟的概觀：  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013|  
  
### 移轉概觀  
  
|1|2|3|4|  
|-------|-------|-------|-------|  
|準備 SharePoint 2013 伺服器陣列|備份、複製和還原資料庫。|掛接內容資料庫|移轉 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 排程|  
||[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|-SharePoint 管理中心<br /><br /> -Windows PowerShell|-SharePoint 應用程式頁面<br /><br /> -Windows PowerShell|  
  
 **本主題內容：**  
  
-   [1) 準備 SharePoint 2013 伺服器陣列](#bkmk_prepare_sharepoint2013)  
  
-   [2) 備份、複製和還原資料庫](#bkmk_backup_restore)  
  
-   [3) 準備 Web 應用程式和掛接內容資料庫](#bkmk_prepare_mount_databases)  
  
-   [4) 升級 Power Pivot 排程](#bkmk_upgrade_powerpivot_schedules)  
  
-   [其他資源](#bkmk_additional_resources)  
  
##  <a name="bkmk_prepare_sharepoint2013"></a> 1) 準備 SharePoint 2013 伺服器陣列  
  
1.  > [!TIP]  
    >  請檢閱您現有 Web 應用程式所設定的驗證方法。 SharePoint 2013 Web 應用程式預設為宣告式驗證。 設定為傳統模式驗證的 SharePoint 2010 Web 應用程式需要進行其他步驟，才能將資料庫從 SharePoint 2010 移轉至 SharePoint 2013。 如果您的 Web 應用程式設定為傳統模式驗證，請檢閱 SharePoint 2013 文件集。  
  
2.  安裝新的 SharePoint Server 2013 伺服器陣列。  
  
3.  以 SharePoint 模式安裝 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器執行個體。 如需詳細資訊，請參閱[以 PowerPivot 模式安裝 Analysis Services](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)。  
  
4.  在 SharePoint 伺服器陣列中的每部伺服器上執行 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013 安裝套件 **spPowerPivot.msi** 。 如需詳細資訊，請參閱[安裝或解除安裝 PowerPivot for SharePoint 增益集 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)。  
  
5.  在 SharePoint 2013 管理中心內，將 Excel Services 服務應用程式設定為使用在先前步驟中建立的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] SharePoint 模式伺服器。 如需詳細資訊，請參閱[以 Power Pivot 模式安裝 Analysis Services](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md) 的＜設定基本 Analysis Services SharePoint 整合＞一節。  
  
##  <a name="bkmk_backup_restore"></a> 2) 備份、複製和還原資料庫  
 「SharePoint 資料庫附加升級」程序是指將 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 相關內容及服務應用程式資料庫備份、複製和還原至 SharePoint 2013 伺服器陣列的一連串步驟。  
  
1.  **將資料庫設定唯讀：**在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下資料庫名稱，然後按一下 [屬性]。 在 [選項] 頁面上，將 [資料庫唯讀] 屬性設定為 [True]。  
  
2.  **備份** ：備份您想要移轉至 SharePoint 2013 伺服器陣列的每個內容資料庫及服務應用程式資料庫。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下資料庫名稱，按一下 [工作]，然後按一下 [備份]。  
  
3.  將資料庫備份檔案 (.bak) 複製到所需的目的地伺服器。  
  
4.  **還原** ：將資料庫還原至目的地 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]。 您可以使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 來完成這個步驟。  
  
5.  **將資料庫設定為讀寫：**將 [資料庫唯讀]設定為 [False]。  
  
##  <a name="bkmk_prepare_mount_databases"></a> 3) 準備 Web 應用程式和掛接內容資料庫  
 如需下列程序的詳細說明，請參閱[將資料庫從 SharePoint 2010 升級到 SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690) (http://go.microsoft.com/fwlink/p/?LinkId=256690)。  
  
1.  **讓資料庫離線：**  
  
     使用 SharePoint 管理中心，讓每個 SharePoint 2013 內容資料庫離線。 您所複製的資料庫會取代這些內容資料庫。 請針對您的環境考量最佳順序。 您可以考慮分別讓每個資料庫離線並且掛接其相關的取代資料庫，然後再讓下一個內容資料庫離線。 另一個選項是以群組的方式，讓所有內容資料庫離線。  
  
    1.  在 SharePoint 管理中心內，按一下 **[應用程式管理]**。  
  
    2.  按一下 **[管理內容資料庫]**。  
  
    3.  按一下資料庫的名稱。  
  
    4.  在 **[管理內容資料庫設定]**上，將 **[資料庫狀態]** 設定為 **[離線]**。  
  
    5.  選取 **[移除內容資料庫]**。 請注意，此時會顯示一則警告，表示儲存在內容資料庫中的網站將無法再存取。  
  
-   **掛接內容資料庫：**  
  
     使用 SharePoint 2013 管理命令介面中的 PowerShell 指令程式來掛接移轉的內容資料庫。 您不需要掛接服務應用程式資料庫，只要掛接內容資料庫即可： ![PowerShell 相關內容](../../../analysis-services/instances/install-windows/media/rs-powershellicon.png "PowerShell 相關內容")  
  
    ```  
    Mount-SPContentDatabase "SharePoint_Content_O14-KJSP1" -DatabaseServer "[server name]\powerpivot" -WebApplication [web application URL]  
    ```  
  
     如需詳細資訊，請參閱[附加或卸離內容資料庫 (SharePoint Server 2010)](http://technet.microsoft.com/library/ff628582.aspx) (http://technet.microsoft.com/library/ff628582.aspx)。  
  
     **完成此步驟之後的狀態**  ：當掛接作業完成時，使用者可以看見原本位於舊內容資料庫中的檔案。 因此，使用者可以查看和開啟文件庫中的活頁簿。  
  
    -   > [!TIP]  
        >  此時，移轉程序可能會針對移轉的活頁簿建立新的排程。 不過，這些排程是建立在新的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服務應用程式資料庫中，而非您從舊 SharePoint 伺服器陣列所複製的資料庫。 因此，資料庫不會包含任何舊排程。 在您完成下列步驟以使用舊資料庫並移轉舊排程之後，則無法使用新的排程。  
  
### 疑難排解嘗試掛接資料庫時所發生的問題  
 本節將摘要說明掛接資料庫時可能會遇到的問題。  
  
1.  **驗證錯誤** ：如果您看見與驗證有關的錯誤，請檢閱來源 Web 應用程式所使用的驗證模式。 此錯誤可能是由於 SharePoint 2013 Web 應用程式與 SharePoint 2010 Web 應用程式之間的驗證不符所造成。 如需詳細資訊，請參閱＜ [1) 準備 SharePoint 2013 伺服器陣列](#bkmk_prepare_sharepoint2013) ＞。  
  
2.  **遺漏 PowerPivot. Files：**如果您看見與遺漏 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .dlls 相關的錯誤，表示 **spPowerPivot.msi** 尚未安裝，或並未使用 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 組態工具來設定 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]。  
  
##  <a name="bkmk_upgrade_powerpivot_schedules"></a> 4) 升級 Power Pivot 排程  
 本節描述移轉[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]排程的詳細資料和選項。 排程移轉是兩個步驟的程序。 首先，請將 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服務應用程式設定為使用移轉的服務應用程式資料庫。 接著，請選擇兩個排程移轉選項的其中之一。  
  
 **將服務應用程式設定為使用移轉的服務應用程式資料庫。**  
  
 在 SharePoint 管理中心內，將 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服務應用程式設定為使用您所複製的舊服務應用程式資料庫。 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服務會將服務應用程式資料庫升級為新的結構描述。  
  
1.  在 SharePoint 管理中心內，按一下 **[管理服務應用程式]**。  
  
2.  尋找 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服務應用程式，例如「預設的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服務應用程式」，按一下服務應用程式的名稱，然後按一下 SharePoint 功能區中的 [屬性]。  
  
3.  將資料庫伺服器名稱-執行個體以及資料庫名稱更新為 您所備份、複製和還原的正確資料庫名稱。 一旦您按一下 **[確定]**之後，就會升級服務應用程式資料庫。 錯誤將列在 ULS 記錄中。  
  
 **升級 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 排程**  
  
 設定 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服務應用程式以移轉重新整理排程。  
  
-   **移轉排程選項 1：SharePoint 伺服器陣列管理員**  
  
    1.  在 SharePoint 2013 管理命令介面中，搭配 `Set-PowerPivotServiceApplication` 參數來執行 `-StartMigratingRefreshSchedules` 指令程式，以便啟用自動視需要排程移轉 ![PowerShell 相關內容](../../../analysis-services/instances/install-windows/media/rs-powershellicon.png "PowerShell 相關內容")。 下列 Windows PowerShell 指令碼會假設只有一個 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服務應用程式存在。  
  
        ```  
        $app=Get-PowerPivotServiceApplication  
        Set-PowerPivotServiceApplication $app -StartMigratingRefreshSchedules  
        ```  
  
         執行 Windows PowerShell 指令碼之後，排程就會處於使用中狀態，而且排程會在下一個適當的時間執行。 不過，排程重新整理頁面上的狀態並非 [已啟用]。 當排程第一次執行時，它將進行移轉，而且在排程重新整理頁面上，[ **已啟用**  ] 將會成立。  
  
    2.  如果您想要檢查 StartMigratingRefreshSchedules 屬性的目前值，請執行下列 PowerShell 指令碼。 這個指令碼會在所有的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服務應用程式物件中執行迴圈，並且顯示名稱和屬性值：  
  
        ```  
        $apps = Get-PowerPivotServiceApplication  
        foreach ($app in $apps){}  
        Get-PowerPivotServiceApplication $appp | format-table -property displayname,id,StartMigratingRefreshSchedules  
        ```  
  
     **移轉排程選項 2：使用者更新每個活頁簿**  
  
    1.  另一個移轉排程的選項是針對每個活頁簿啟用排程重新整理。 導覽到包含活頁簿的文件庫。  
  
    2.  開啟操作功能表，然後按一下 [管理 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 資料重新整理] 。  
  
    3.  在 **[排程重新整理]** 區段中，按一下 **[啟用]**。  
  
    4.  您可以選取 **[並且盡快重新整理]**。 一旦您按一下 [確定] 之後，這個選項就會將一個重新整理執行個體加入至佇列。 定期重新整理排程仍然會在適當的時間觸發。  
  
    5.  按一下 **[確定]**。 重新整理記錄現在會顯示在重新整理頁面中，而且排程會在一般時間引發。  
  
 **SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿**  
  
-   於 SharePoint 2013 的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 中使用 SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 活頁簿時，活頁簿不會自動升級。 當您移轉包含 2008 R2 活頁簿的內容資料庫之後，就可以使用這些活頁簿，但是排程不會升級。  
  
-   如需詳細資訊，請參閱[升級活頁簿和排程的資料重新整理 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)。  
  
##  <a name="bkmk_additional_resources"></a> 其他資源  
  
> [!NOTE]  
>  如需有關 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 和 SharePoint 資料庫附加升級的詳細資訊，請參閱下列主題：  
  
-   [升級活頁簿和排程的資料重新整理 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
-   [SharePoint 2013 升級程序概觀](http://go.microsoft.com/fwlink/p/?LinkId=256688) (http://go.microsoft.com/fwlink/p/?LinkId=256688)。  
  
-   [升級為 SharePoint 2013 之前的清除準備工作](http://go.microsoft.com/fwlink/p/?LinkId=256689) (http://go.microsoft.com/fwlink/p/?LinkId=256689)。  
  
-   [Upgrade databases from SharePoint 2010 to SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690) (http://go.microsoft.com/fwlink/p/?LinkId=256690) (將資料庫從 SharePoint 2010 升級到 SharePoint 2013)。  
  
  