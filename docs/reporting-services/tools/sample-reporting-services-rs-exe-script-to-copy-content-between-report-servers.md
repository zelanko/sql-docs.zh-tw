---
title: 在報表伺服器之間複製內容的範例 Reporting Services rs.exe 指令碼 | Microsoft Docs
ms.date: 05/23/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.assetid: d81bb03a-a89e-4fc1-a62b-886fb5338150
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 18d10f94696f901efd4f3938bf9b5e06d1c7078d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "70176283"
---
# <a name="sample-reporting-services-rsexe-script-to-copy-content-between-report-servers"></a>在報表伺服器之間複製內容的範例 Reporting Services rs.exe 指令碼

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2008r2-and-later](../../includes/ssrs-appliesto-2008r2-and-later.md)] [!INCLUDE [ssrs-appliesto-sharepoint-2013-2016](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-pbirs](../../includes/ssrs-appliesto-pbirs.md)]

本文包含並描述範例 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] RSS 指令碼，其可使用 **RS.exe** 公用程式將一部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器的內容項目和設定複製到另一部報表伺服器。 不論是原生或 SharePoint 模式，RS.exe 都會和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]一起安裝。 這個指令碼會在伺服器之間複製 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 項目，例如報表和訂閱。 這個指令碼同時支援 SharePoint 模式和原生模式報表伺服器。  

##  <a name="to-download-the-ssrs_migrationrss-script"></a><a name="bkmk_download_script"></a> 下載 ssrs_migration.rss 指令碼  
 從 GitHub 網站 [Reporting Services RS.exe migration script](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/reporting-services/ssrs-migration-rss) (Reporting Services RS.exe 移轉指令碼) 下載指令碼至本機資料夾。 如需詳細資訊，請參閱本文的[如何使用指令碼](#bkmk_how_to_use_the_script)一節。  
  
##  <a name="supported-scenarios"></a><a name="bkmk_supported_scenarios"></a> 支援的案例  
 這個指令碼同時支援 SharePoint 模式和原生模式報表伺服器。 指令碼支援報表伺服器版本 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 和更新版本，以及 Power BI 報表伺服器。  
  
這個指令碼可用來在相同模式或不同模式的報表伺服器之間複製內容。 例如，您可以執行指令碼將內容從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 原生模式報表伺服器複製到 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] SharePoint 模式報表伺服器。 您可以安裝 RS.exe 的任何伺服器執行這個指令碼。 例如，在下列部署中，您可以：  
  
-   在伺服器 A **上** 執行 RS.exe 和指令碼。  
  
-   **從** 伺服器 B 複製內容  
  
-   **到** 到伺服器 C  
  
|伺服器名稱|報表伺服器模式|  
|-----------------|------------------------|  
|伺服器 A|原生|  
|伺服器 B|SharePoint|  
|伺服器 C|SharePoint|  
  
 如需 RS.exe 公用程式的詳細資訊，請參閱 [RS.exe 公用程式 &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md)。  
  
###  <a name="items-and-resources-the-script-migrates"></a><a name="bkmk_what_is_migrated"></a> 指令碼移轉的項目及資源  
 這個指令碼不會覆寫相同名稱的現有內容項目。  如果指令碼偵測到來源伺服器與目的地伺服器上有相同名稱的項目，則個別項目將會產生「失敗」訊息，但指令碼會繼續。 下表列出指令碼可移轉至目標報表伺服器模式的內容和資源類型。  
  
|Item|已移轉|SharePoint|描述|  
|----------|--------------|----------------|-----------------|  
|密碼|**否**|**否**|密碼 **不會** 移轉。 內容項目移轉之後，請更新目的地伺服器上的認證資訊。 例如，具有預存認證的資料來源。|  
|我的報表|**否**|**否**|原生模式「我的報表」功能是以個別使用者登入為基礎，因此除非使用者使用 **-u** 參數來執行 rss 指令碼，否則指令碼服務將無法存取 [我的報表] 資料夾中的內容。 此外，[我的報表] 不屬於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式的功能，所以資料夾中的項目無法複製到 SharePoint 環境中。 因此，指令碼不會複製來源原生模式報表伺服器上 [我的報表] 資料夾中的報表項目<br /><br /> 若要使用這個指令碼移轉 [我的報表] 資料夾中的內容，請完成下列步驟：<br /><br /> 1.在入口網站中建立新資料夾。 或者，您可以為每個使用者建立資料夾或子資料夾。<br />2.以其中一個具有「我的報表」內容的使用者身分登入。<br />3.在入口網站中，選取 [我的報表]  資料夾。<br />4.選取該資料夾的 [詳細資料]  檢視。<br />5.選取要複製的每一份報表。<br />6.選取入口網站工具列中的 [移動]  。<br />7.選取所需的目的地資料夾。<br />8.對每位使用者重複步驟 2-7。<br />9.執行指令碼。|  
|記錄|**否**|**否**||  
|記錄設定|是|是|雖然記錄設定會移轉，但是記錄詳細資料「不會」移轉。|  
|排程|是|是|若要移轉排程，則必須在目標伺服器上執行 SQL Server Agent。 如果 SQL Server Agent 未在目標上執行，您將會看見類似這句的錯誤訊息：<br /><br /> `Migrating schedules: 1 items found. Migrating schedule: theMondaySchedule ... FAILURE:  The SQL Agent service isn't running. This operation requires the SQL Agent service. ---> Microsoft.ReportingServices.Diagnostics.Utilities.SchedulerNotResponding Exception: The SQL Agent service isn't running. This operation requires the SQL Agent service.`|  
|角色和系統原則|是|是|根據預設，指令碼不會在伺服器之間複製自訂的權限結構描述。 預設行為是，項目會複製到目的地伺服器，且「繼承父權限」旗標會設為 TRUE。 如果您希望指令碼複製個別項目的權限，請使用 SECURITY 參數。<br /><br /> 如果來源和目標伺服器**不屬於相同的報表伺服器模式** (例如從原生模式到 SharePoint 模式)，而且您使用 SECURITY 參數，則指令碼將會根據下文中的比較來嘗試對應預設角色和群組：[將 Reporting Services 中的角色和工作與 SharePoint 群組和權限做比較](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)。 自訂角色和群組不會複製到目的地伺服器。<br /><br /> 當指令碼在 **屬於相同模式**的伺服器之間進行複製，而且您使用 SECURITY 參數時，指令碼將會在目的地伺服器上建立新的角色 (原生模式) 或群組 (SharePoint 模式)。<br /><br /> 如果角色已出現在目的地伺服器上，指令碼將會建立類似下面的「失敗」訊息，並繼續移轉其他項目。 指令碼完成後，請確認目的地伺服器上的角色是否已根據您的需求設定。 正在移轉的角色：找到 8 個項目。<br /><br /> `Migrating role: Browser ... FAILURE: The role 'Browser' already exists and cannot be created. ---> Microsoft.ReportingServices.Diagnostics.Utilities.RoleAlreadyExistsException: The role 'Browser' already exists and cannot be created.`<br /><br /> 如需詳細資訊，請參閱[將報表伺服器的存取權授與使用者](../../reporting-services/security/grant-user-access-to-a-report-server.md)<br /><br /> **注意：** 如果來源伺服器上的使用者不存在於目的地伺服器上，指令碼就無法在目的地伺服器上套用角色指派，而且即使已使用 SECURITY 參數，也無法套用角色指派。|  
|共用資料來源|是|是|指令碼將不會覆寫目標伺服器上的現有項目。 如果目標伺服器上已存在相同名稱的項目，您將會看見類似這句的錯誤訊息：<br /><br /> `Migrating DataSource: /Data Sources/Aworks2012_oltp ... FAILURE:The item '/Data Sources/Aworks2012_oltp' already exists. ---> Microsoft.ReportingServices.Diagnostics.Utilities.ItemAlreadyExistsException: The item '/Data Source s/Aworks2012_oltp' already exists.`<br /><br /> 認證 **不** 會複製作為資料來源的一部分。 內容項目移轉之後，請更新目的地伺服器上的認證資訊。|  
|共用資料集|是|是|| 
|資料夾|是|是|指令碼將不會覆寫目標伺服器上的現有項目。 如果目標伺服器上已存在相同名稱的項目，您將會看見類似這句的錯誤訊息：<br /><br /> `Migrating Folder: /Reports ... FAILURE: The item '/Reports' already exists. ---> Microsoft.ReportingServices.Diagnostics.Utilities.ItemAlreadyExistsException: The item '/Reports' already exists.`|  
|Report|是|是|指令碼將不會覆寫目標伺服器上的現有項目。 如果目標伺服器上已存在相同名稱的項目，您將會看見類似這句的錯誤訊息：<br /><br /> `Migrating Report: /Reports/testThe item '/Reports/test' already exists. ---> Microsoft.ReportingServices.Diagnostics.Utilities.ItemAlreadyExistsException: The item '/Reports/test' already exists.`|  
|參數|是|是||  
|訂用帳戶|是|是||  
|記錄設定|是|是|雖然記錄設定會移轉，但是記錄詳細資料「不會」移轉。|  
|處理選項|是|是||  
|快取重新整理選項|是|是|相依設定會隨目錄項目一起移轉。 以下範例將示範指令碼移轉報表 (.rdl) 以及相關的設定 (例如快取重新整理選項)：<br /><br /> -   移轉報表 TitleOnly.rdl 的參數：找到 0 個項目。<br />-   正在移轉報表 TitleOnly.rdl 的訂用帳戶：找到 1 個項目。<br />-   移轉 \\\server\public\savedreports as TitleOnly 中儲存為 TitleOnly 的訂用帳戶 ...SUCCESS<br />-   移轉報表 TitleOnly.rdl 的記錄設定 ...SUCCESS<br />-   移轉報表 TitleOnly.rdl 的處理選項 ...找到 0 個項目。<br />-   移轉報表 TitleOnly.rdl 的快取重新整理選項 ...SUCCESS<br />-   正在移轉報表 TitleOnly.rdl 的快取重新整理計劃：找到 1 個項目。<br />-   移轉快取重新整理計劃 titleonly_refresh735amM2F ...SUCCESS|  
|快取重新整理計劃|是|是||  
|影像|是|是||  
|報表組件|是|是||  
  
##  <a name="required-permissions"></a><a name="bkmk_required_permissions"></a>必要權限  
 指令碼中用來讀取或寫入項目和資源之所有方法所需的權限不盡相同。 下表摘要列出每個項目或資源使用的方式，以及相關內容的連結。 請瀏覽至個別文章以查看必要的權限。 例如，ListChildren 方法主題說明下列操作的必要權限：  
  
-   **原生模式需要的權限：** 項目的 ReadProperties  
  
-   **SharePoint 模式需要的權限：** ViewListItems  
  
|項目或資源|來源|目標|  
|----------------------|------------|------------|  
|目錄項目|<xref:ReportService2010.ReportingService2010.ListChildren%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetProperties%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetItemDataSources%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetItemReferences%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetDataSourceContents%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetItemLink%2A>|<xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A><br /><br /> <xref:ReportService2010.ReportingService2010.SetItemDataSources%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetItemReferences%2A><br /><br /> <xref:ReportService2010.ReportingService2010.CreateDataSource%2A><br /><br /> <xref:ReportService2010.ReportingService2010.CreateLinkedItem%2A><br /><br /> <xref:ReportService2010.ReportingService2010.CreateFolder%2A>|  
|角色|<xref:ReportService2010.ReportingService2010.ListRoles%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetRoleProperties%2A>|<xref:ReportService2010.ReportingService2010.CreateRole%2A>|  
|系統原則|<xref:ReportService2010.ReportingService2010.GetSystemPolicies%2A>|<xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A>|  
|排程|<xref:ReportService2010.ReportingService2010.ListSchedules%2A>|<xref:ReportService2010.ReportingService2010.CreateSchedule%2A>|  
|訂用帳戶|<xref:ReportService2010.ReportingService2010.ListSubscriptions%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetSubscriptionProperties%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetDataDrivenSubscriptionProperties%2A>|<xref:ReportService2010.ReportingService2010.CreateSubscription%2A><br /><br /> <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>|  
|快取重新整理計劃|<xref:ReportService2010.ReportingService2010.ListCacheRefreshPlans%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetCacheRefreshPlanProperties%2A>|<xref:ReportService2010.ReportingService2010.CreateCacheRefreshPlan%2A>|  
|參數|<xref:ReportService2010.ReportingService2010.GetItemParameters%2A>|<xref:ReportService2010.ReportingService2010.SetItemParameters%2A>|  
|執行選項|<xref:ReportService2010.ReportingService2010.GetExecutionOptions%2A>|<xref:ReportService2010.ReportingService2010.SetExecutionOptions%2A>|  
|快取選項|<xref:ReportService2010.ReportingService2010.GetCacheOptions%2A>|<xref:ReportService2010.ReportingService2010.SetCacheOptions%2A>|  
|記錄設定|<xref:ReportService2010.ReportingService2010.GetItemHistoryOptions%2A>|<xref:ReportService2010.ReportingService2010.SetItemHistoryOptions%2A>|  
|項目原則|<xref:ReportService2010.ReportingService2010.GetPolicies%2A>|<xref:ReportService2010.ReportingService2010.SetPolicies%2A>|  
  
 如需詳細資訊，請參閱 [將 Reporting Services 中的角色和工作與 SharePoint 群組和權限做比較](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)。  
  
##  <a name="how-to-use-the-script"></a><a name="bkmk_how_to_use_the_script"></a> 如何使用指令碼  
  
1.  將指令碼檔案下載至本機資料夾，例如 **c:\rss\ssrs_migration.rss**。  
  
2.  **以系統管理權限**開啟命令提示字元。  
  
3.  導覽至包含 ssrs_migration.rss 檔案的資料夾。  
  
4.  搭配適合您狀況的參數執行命令。  
  
 **基本範例，原生模式報表伺服器到原生模式報表伺服器：**  
  
 下列範例將從原生模式 **Sourceserver** 將內容移轉至原生模式 **Targetserver**。  
  
 `rs.exe -i ssrs_migration.rss -e Mgmt2010 -s https://SourceServer/ReportServer -u Domain\User -p password -v ts="https://TargetServer/reportserver" -v tu="Domain\Userser" -v tp="password"`  
  
 **使用方式附註：**  
  
-   指令碼會以兩個步驟執行。  
  
     第一個步驟是稽核，傳回將要移轉的項目清單，第二個步驟則是移轉程序。  
  
     如果您只是想查看可能的移轉清單，或是想要修改參數，可以 **在第一個步驟之後取消指令碼** 。 第一個步驟中不會列出相依設定。 例如，報表的快取選項不會列出，而是列出報表本身。  
  
    > [!TIP]  
    > 若您只想稽核單一伺服器，請針對來源和目的地使用相同的伺服器，然後在完成步驟 1 後取消。  
  
     步驟 1 稽核資訊相當適合用於檢閱來源和目標原生模式伺服器上的現有角色。 以下是步驟一稽核清單的範例。 請注意清單中包含一個 [角色] 區段，因為使用了 switch-v security="True" 參數：  
  
    -   `Retrieve and report the list of items that will be migrated. You can cancel the script after step 1 if you do not want to start the actual migration.`  
  
         `Retrieving roles:`  
  
         `Role: Browser`  
  
         `Role: Content Manager`  
  
         `Role: Model Item Browser`  
  
         `Retrieve and report the list of items that will be migrated. You can cancel the script after step 1 if you do not want to start the actual migration.`  
  
         `Retrieving roles:`  
  
         `Role: Browser`  
  
         `Role: Content Manager`  
  
         `Role: CustomRole`  
  
         `Role: Model Item Browser`  
  
         `Role: My Reports`  
  
         `Role: Publisher`  
  
         `Role: Report Builder`  
  
         `Role: System Administrator`  
  
         `Role: System User`  
  
         `Retrieving system policies:`  
  
         `Retrieving system policies:`  
  
         `System policy: BUILTIN\Administrators`  
  
         `System policy: domain\user1`  
  
         `System policy: domain\ueser2`  
  
         `Retrieving schedules:`  
  
         `Schedule: theMondaySchedule`  
  
         `Retrieving catalog items. This may take a while.`  
  
         `Folder: /Data Sources`  
  
         `DataSource: /Data Sources/Aworks2012_oltp`  
  
         `Folder: /images`  
  
         `Resource: /images/Boba Fett.png`  
  
         `Resource: /images/R2-D2.png`  
  
         `Folder: /Reports`  
  
         `Report: /Reports/products`  
  
         `Report: /Reports/test`  
  
         `Report: /Reports/TitleOnly`  
  
-   SOURCE_URL 和 TARGET_URL 必須是指向來源和目標 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器的有效報表伺服器 URL。 在原生模式中，報表伺服器 URL 看起來像此 URL：  
  
    -   `https://servername/reportserver`  
  
     在 SharePoint 模式中，URL 看起來像此 URL：  
  
    -   `https://servername/_vti_bin/reportserver`  
  
-   在 SharePoint 中對使用者呈現的虛擬資料夾結構可能與基礎結構有所不同。 在瀏覽器中開啟 `https://servername/_vti_bin/reportserver` 或 `https://servername/sites/site_name/_vti_bin/reportserver` ，查看非虛擬資料夾結構。 這樣有助於在 SharePoint 模式中，為伺服器設定 "/" 以外的來源資料夾和目標資料夾。  
  
-   密碼不會移轉，而且必須重新輸入，例如具有預存認證的資料來源。  
  
##  <a name="parameter-description"></a><a name="bkmk_parameter_description"></a> 參數描述  
  
|參數|描述|必要|  
|---------------|-----------------|--------------|  
|**-s** Source_URL|來源報表伺服器的 URL|是|  
|**-u** Domain\password **-p** password|來源伺服器的認證。|(選擇性) 如果遺失則使用預設認證|  
|**-v st**="SITE"||選擇性。 這個參數僅用於 SharePoint 模式報表伺服器。|  
|**- v f**="SOURCEFOLDER"|設定為 "/" 表示移轉所有內容，設定為類似 "/folder/subfolder" 則表示部分移轉。 將會複製這個資料夾中的所有內容|(選擇性) 預設值為 "/"。|  
|**-v ts**="TARGET_URL"|目標 RS 伺服器的 URL||  
|**-v tu**="domain\username" **-v tp**="password"|目標伺服器的認證。|(選擇性) 如果遺失則使用預設認證。 **注意：** 在目標伺服器中，使用者將列為共用排程的「建立者」，以及報表項目的「修改者」帳戶。|  
|**-v tst**="SITE"||選擇性。 這個參數僅用於 SharePoint 模式報表伺服器。|  
|**-v tf** ="TARGETFOLDER"|設定為 "/" 表示移轉至根層級。 設定為 "/folder/subfolder" 表示複製到已存在的資料夾。 "SOURCEFOLDER" 內的所有內容都會複製到 "TARGETFOLDER"。|(選擇性) 預設值為 "/"。|  
|**-v security**= "True/False"|如果設為 "False"，則目的地目錄項目將會根據目標系統的設定繼承安全性設定。 這是在不同報表伺服器類型 (例如，原生模式到 SharePoint 模式) 之間進行移轉的建議設定。 如果設為 "True"，則指令碼會嘗試移轉安全性設定。|(選擇性) 預設值為 "False"。|  
  
##  <a name="more-examples"></a><a name="bkmk_more_examples"></a> 更多範例  
  
###  <a name="native-mode-report-server-to-native-mode-report-server"></a><a name="bkmk_native_2_native"></a> 原生模式報表伺服器到原生模式報表伺服器  
 下列範例將從原生模式 **Sourceserver** 將內容移轉至原生模式 **Targetserver**。  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s https://SourceServer/ReportServer -u Domain\User -p password -v ts="https://TargetServer/reportserver" -v tu="Domain\Userser" -v tp="password"  
```  
  
 下列範例將會加入安全性參數：  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s https://SourceServer/ReportServer -u Domain\User -p password -v ts="https://TargetServer/reportserver" -v tu="Domain\Userser" -v tp="password" -v security="True"  
```  
  
###  <a name="native-mode-to-sharepoint-mode---root-site"></a><a name="bkmk_native_2_sharepoint_root"></a> 原生模式到 SharePoint 模式 - 根網站  
 下列範例將從原生模式 **SourceServer** 將內容移轉至 SharePoint 模式伺服器 **TargetServer** 上的「根網站」。 原生模式伺服器上的 [報表] 和 [資料來源] 資料夾會在 SharePoint 部署上移轉為新文件庫。  
  
 ![ssrs_rss_migrate_root_site](../../reporting-services/tools/media/ssrs-rss-migrate-root-site.gif "ssrs_rss_migrate_root_site")  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s https://SourceServer/ReportServer -u Domain\User -p Password -v ts="https://TargetServer/_vti_bin/ReportServer" -v tu="Domain\User" -v tp="Password"  
```  
  
###  <a name="native-mode-to-sharepoint-mode--bi-site-collection"></a><a name="bkmk_native_2_sharepoint_with_site"></a> 原生模式到 SharePoint 模式 - 'bi' 網站集合  
 下列範例將從原生模式伺服器將內容移轉至包含網站集合 "sites/bi" 和共用文件庫的 SharePoint 伺服器。 指令碼會在目的地文件庫中建立資料夾。 例如，指令碼將在目標文件庫中建立 [報表] 和 [資料來源] 資料夾。  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s https://SourceServer/ReportServer -u Domain\User -p Password -v ts="https://TargetServer/sites/bi/_vti_bin/reportserver" -v tst="sites/bi" -v tf="Shared Documents" -v tu="Domain\User" -v tp="Password"  
```  
  
###  <a name="sharepoint-mode-to-sharepoint-mode--bi-site-collection"></a><a name="bkmk_sharepoint_2_sharepoint"></a> SharePoint 模式到 SharePoint 模式 - 'bi' 網站集合  
 下列範例會移轉內容：  
  
-   從包含 "sites/bi" 網站集合和共用文件庫的 SharePoint 伺服器 **SourceServer** 。  
  
-   到包含 "sites/bi" 網站集合和共用文件庫的 **TargetServer** SharePoint 伺服器。  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s https://SourceServer/_vti_bin/reportserver -v st="sites/bi" -v f="Shared Documents" -u Domain\User1 -p Password -v ts="https://TargetServer/sites/bi/_vti_bin/reportserver" -v tst="sites/bi" -v tf="Shared Documents" -v tu="Domain\User" -v tp="Password"  
```  
  
###  <a name="native-mode-to-native-mode---azure-virtual-machine"></a><a name="bkmk_native_to_native_Azure_vm"></a> 原生模式到原生模式 - Azure 虛擬機器  
 下列範例會移轉內容：  
  
-   從原生模式報表伺服器 **SourceServer**。  
  
-   到 Azure 虛擬機器上執行的 **TargetServer** 原生模式報表伺服器。 **TargetServer** 不會聯結至 **SourceServer** 的網域，而且 **User2** 是 Azure 虛擬機器 **TargetServer** 的系統管理員。  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s https://SourceServer/ReportServer -u Domain\user1 -p Password -v ts="https://ssrsnativeazure.cloudapp.net/ReportServer" -v tu="user2" -v tp="Password2"  
```  
  
> [!TIP]  
> 如需如何使用 Windows PowerShell 在 Windows Azure 虛擬機器上建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器的詳細資訊，請參閱[使用 PowerShell 建立具有原生模式報表伺服器的 Azure VM](https://docs.microsoft.com/azure/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-ps-sql-report) \(不分機器翻譯\)。  
  
##  <a name="sharepoint-mode--bi-site-collection-to-a-native-mode-server-on-an-azure-virtual-machine"></a><a name="bkmk_sharepoint_site_to_native_Azure_vm"></a> SharePoint 模式 -'bi' 站台集合到 Azure 虛擬機器上的原生模式伺服器。 
 下列範例會移轉內容：  
  
-   從包含 "sites/bi" 網站集合和共用文件庫的 SharePoint 模式報表伺服器 **SourceServer** 。  
  
-   到 Azure 虛擬機器上執行的 **TargetServer** 原生模式報表伺服器。 **TargetServer** 不會聯結至 **SourceServer** 的網域，而且 **User2** 是 Azure 虛擬機器 **TargetServer** 的系統管理員。  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s https://uetesta02/_vti_bin/reportserver -u user1 -p Password -v ts="https://ssrsnativeazure.cloudapp.net/ReportServer" -v tu="user2" -v tp="Passowrd2"  
```  
  
##  <a name="verification"></a><a name="bkmk_verification"></a> 驗證  
 本節摘要說明在目的地伺服器上驗證內容和原則是否成功移轉所採取的一些步驟。  
  
### <a name="schedules"></a>排程  
 若要驗證目標伺服器上的排程：  
  
 **Native Mode**  
  
1.  在目的地伺服器上開啟入口網站。  
  
2.  選取上層功能表上的 [網站設定]  。  
  
3.  選取左窗格中的 [排程]  。  
  
 **SharePoint 模式：**  
  
1.  瀏覽至 **[網站設定]** 。  
  
2.  在 **[Reporting Services]** 群組中，按一下 **[管理共用排程]** 。  
  
### <a name="roles-and-groups"></a>角色和群組  
 **Native Mode**  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 並連接至您的原生模式報表伺服器。  
  
2.  在 **[物件總管]** 中按一下 **[安全性]** 。  
  
3.  按一下 [角色]  。  
  
##  <a name="troubleshooting"></a><a name="bkmk_troubleshoot"></a> 疑難排解  
 使用追蹤旗標 **-t** 取得詳細資訊。 例如，如果您執行指令碼並且看到類似下面的訊息  
  
-   無法連線到伺服器: https://\<servername>/ReportServer/ReportService2010.asmx  
  
 再次使用 **-t** 旗標執行指令碼，就會看見類似這句的訊息：  
  
-   System.Exception：無法連接到伺服器： https://\<伺服器名稱>/ReportServer/ReportService2010.asmx ---> System.Net.WebException：**要求失敗，HTTP 狀態為 401：未經授權**。   at System.Web.Services.Protocols.SoapHttpClientProtocol.ReadResponse(SoapClientMessage message, WebResponse response, Stream responseStream, Boolean asyncCall)   at System.Web.Services.Protocols.SoapHttpClientProtocol.Invoke(String methodName, Object[] parameters)   at Microsoft.SqlServer.ReportingServices2010.ReportingService2010.IsSSLRequired()   at Microsoft.ReportingServices.ScriptHost.Management2010Endpoint.PingService(String url, String userName, String password, String domain, Int32 timeout)   at Microsoft.ReportingServices.ScriptHost.ScriptHost.DetermineServerUrlSecurity()   --- 內部例外狀況堆疊追蹤結束 ---  
  
## <a name="see-also"></a>另請參閱  
 [RS.exe 公用程式 &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md)   
 [將 Reporting Services 中的角色和工作與 SharePoint 群組和權限做比較](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
  
  
