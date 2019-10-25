---
title: 安裝 SharePoint 2010 Reporting Services SharePoint 模式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 47efa72e-1735-4387-8485-f8994fb08c8c
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 758c76bf243af66157aa06f761df010a1e086a91
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798354"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2010"></a>安裝適用於 SharePoint 2010 的 Reporting Services SharePoint 模式
  本主題中的程序會引導您完成 SharePoint 模式之 Reporting Services 報表伺服器的單一伺服器安裝。 這些步驟包含執行 [SQL Server 安裝精靈]，以及使用 SharePoint 2010 管理中心的其他組態工作。 本主題也可以用於現有安裝的個別程序，例如建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。 如需將其他 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 伺服器加入至現有伺服器陣列的詳細資訊，請參閱[將其他報表伺服器&#40;加入至伺服器陣列&#41; SSRS 向外](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)延展和[將額外的 Reporting Services Web 前端新增至伺服器](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)陣列。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
 單一伺服器安裝對開發和測試案例很實用，但是不建議在實際執行環境中使用。  
  
> [!NOTE]  
>  如需有關將 SharePoint 模式安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的詳細資訊，請參閱[升級和遷移 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)。  
  

  
##  <a name="bkmk_prereq"></a> Prerequisites  
  
-   > [!IMPORTANT]  
    >  設定及管理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式時，不再需要或支援 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員。 您可以使用 SharePoint 管理中心，在 SharePoint 模式下設定報表伺服器。 如需詳細資訊，請參閱[管理 Reporting Services SharePoint 服務應用程式](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)。  
  
-   檢閱下列需求主題，包括 SharePoint 2010 產品：  
  
    -   [線上版本資訊](https://msdn.microsoft.com/library/dn169381.aspx)
  
    -   [在 SharePoint 2010 伺服器陣列中使用 SQL Server BI 功能的指引](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
-   本主題不涵蓋 SharePoint 2010 產品的安裝。 如需詳細資訊，請參閱[在 SharePoint 2010 伺服器陣列中使用 SQL SERVER BI 功能的指導](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)方針。  
  
-   這些程序並非是用於設定 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 報表伺服器，而且亦不適用於舊版報表伺服器。 舊版報表伺服器不是使用 SharePoint 共用服務架構。 例如，SQL Server 2008 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器和 SQL Server 2008 R2 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器。  
  
-   確認**SharePoint 2010 Administration**服務已在 Windows 伺服器管理員中啟動。  
  
 ![1個伺服器安裝上的 SSRS 元件](../../../2014/sql-server/install/media/rs-deployment-1-server.gif "1個伺服器安裝上的 SSRS 元件")  
  
### <a name="database-considerations-for-a-single-server-configuration"></a>單一伺服器組態的資料庫考量  
  
-   Reporting Services 和 SharePoint 產品及技術都使用 SQL Server 關聯式資料庫儲存應用程式資料。  
  
-   [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 需要相容之 SQL 引擎的 SQL Server Evaluation Edition 執行個體。  
  
-   SharePoint 產品可以使用現有的資料庫執行個體。 如果未安裝資料庫引擎的實例，SharePoint 產品安裝程式會為 SharePoint 應用程式資料庫安裝 SQL Server Express 版本。  
  
-   報表伺服器執行個體無法使用 SQL Server Express Edition 做為其資料庫； 但是，由 SharePoint 產品所安裝的 SQL Server Express Edition 執行個體可以與其他 Database Engine 版本並存。  
  

  
##  <a name="bkmk_install_SSRS"></a>以 SharePoint 模式安裝 Reporting Services 報表伺服器  
  
1.  執行 [SQL Server 安裝精靈]。  
  
2.  在精靈的左側按一下 **[安裝]** ，然後按一下 **[新增 SQL Server 獨立安裝或將功能加入至現有安裝]** 。  
  
3.  在 **[安裝程式支援規則]** 頁面上按一下 **[確定]** (假設已通過所有規則)。  
  
4.  在 **[安裝程式支援檔案]** 頁面中按一下 **[安裝]** 。  
  
5.  在支援檔案完成安裝且支援規則顯示 [**通過**] 狀態之後，按 **[下一步]** 。 檢閱任何警告或封鎖問題。  
  
6.  在 [**產品金鑰**] 頁面上，輸入您的金鑰或接受「企業評估版」的預設值。  
  
     按一下 **[下一步]** 。  
  
7.  檢閱並接受授權條款。 Microsoft 感謝您同意傳送功能使用資料，協助改進產品功能及支援。  
  
     按一下 **[下一步]** 。  
  
8.  在 [**安裝程式角色**] 頁面上，選取 [ **SQL Server 功能安裝**]。  
  
     按 **[下一步]**  
  
     ![安裝程式角色的 SQL Server 功能安裝](../../../2014/sql-server/install/media/rs-setuprole.gif "安裝程式角色的 SQL Server 功能安裝")  
  
9. 在 **[特徵選取]** 頁面上，選取下列選項：  
  
    -   **Reporting Services - SharePoint**  
  
    -   **適用于 SharePoint 2010 產品的 Reporting Services 增益集**。 ![注意](../../../2014/reporting-services/media/rs-fyinote.png "note")安裝增益集的 [安裝精靈] 選項是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的新功能。  
  
    -   如果您尚未有 SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體，您也可以針對完整的環境選取 **[Database Engine Services]** 和 **[管理工具 - 完整]** 。  
  
     按一下 **[下一步]** 。  
  
     ![適用于 SharePoint 模式的 SSRS 功能選取](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "適用于 SharePoint 模式的 SSRS 功能選取")  
  
10. 按一下 [**安裝規則**] 頁面上的 **[下一步]** 。 檢閱任何警告或封鎖問題。  
  
11. 如果您選取 Database Engine 服務，請接受 **[執行個體組態]** 頁面上的預設 **[MSSQLSERVER]** 執行個體，然後按 **[下一步]** 。 Reporting Services 共用服務架構與舊版 Reporting Services 架構不同，不是以 SQL Server「執行個體」為基礎。  
  
12. 檢閱 **[磁碟空間需求]** 頁面，然後按 **[下一步]** 。  
  
13. 在 [**伺服器**設定] 頁面上，輸入適當的認證。 如果您想要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料警示或訂閱功能，則必須將 SQL Server Agent 的 **[啟動類型]** 變更為 **[自動]** 。  
  
     按一下 **[下一步]** 。  
  
14. 如果您選取了 Database Engine 服務，就會看到 **[資料庫引擎組態]** 頁面。請將適當的帳戶加入至 SQL 管理員清單，然後按 **[下一步]** 。  
  
15. 在 **[Reporting Services 組態]** 頁面上，您應該會看到已選取 **[只安裝]** 選項。 此選項會安裝報表伺服器檔案，但不會設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的 SharePoint 環境。完成 SQL Server 安裝之後，您需要遵循本主題中的其他章節設定 SharePoint 環境， 包括安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共用服務及建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。  
  
     ![rs_SQL11_SETUP_SSRS_configpage_withcircles](../../../2014/sql-server/install/media/rs-kj-setup-ssrs-configpage-withcircles.gif "rs_SQL11_SETUP_SSRS_configpage_withcircles")  
  
16. 按一下 **[錯誤報告]** 頁面上的核取方塊傳送錯誤報告，協助 Microsoft 改進 SQL Server 功能與服務。  
  
     按一下 **[下一步]** 。  
  
17. 檢閱任何警告，然後在 **[安裝組態規則]** 頁面上按 **[下一步]** 。  
  
18. 在 **[準備安裝]** 頁面上檢閱安裝摘要，然後按 **[下一步]** 。 摘要會包含**Reporting Services**節點，其中包含**SharePointFilesOnlyMode**的安裝模式值以及帳戶資訊。  
  

  
##  <a name="bkmk_install_SSRS_sharedservice"></a>安裝並啟動 Reporting Services SharePoint 服務  
 ![PowerShell 相關內容](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell 相關內容")  
  
> [!NOTE]  
>  如果您要將安裝到現有的 SharePoint 伺服器陣列中，**則不需要**完成本節中的步驟。 在上一節執行 [SQL Server 安裝精靈] 時，會安裝並啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 服務。  
  
 必要檔案會隨 [SQL Server 安裝精靈] 安裝，但是您必須在 SharePoint 伺服器陣列中註冊服務。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本引進了適用於 SharePoint 模式中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的 PowerShell 支援。 下列步驟將引導您開啟 SharePoint 管理命令介面並執行指令程式：  
  
1.  按一下 **[開始]** 按鈕  
  
2.  按一下 [ **Microsoft SharePoint 2010 產品**] 群組。  
  
3.  以滑鼠右鍵按一下 [ **SharePoint 2010 管理命令**介面] 按一下 [**以系統管理員身分執行**]。  
  
4.  執行下列 PowerShell 命令安裝 SharePoint 服務。 成功完成命令會在管理命令介面中顯示新行。 成功完成命令之後，不會有任何訊息傳回管理命令介面：  
  
    ```powershell
    Install-SPRSService  
    ```  
  
5.  執行下列 PowerShell 命令安裝服務 Proxy：  
  
    ```powershell
    Install-SPRSServiceProxy  
    ```  
  
6.  執行下列 PowerShell 命令啟動服務，或參閱下列附註，以取得從 SharePoint 管理中心啟動服務的指示：  
  
    ```powershell
    Get-SPServiceInstance -All | Where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 您也可以從 SharePoint 管理中心啟動服務，而不是執行第三個 PowerShell 命令。 下列步驟也可用於確認服務是否執行。  
  
1.  在 SharePoint 管理中心內，按一下 **[系統設定]** 群組中的 **[管理伺服器上的服務]** 。  
  
2.  找到 **[SQL Server Reporting Services 服務]** ，然後按一下 [動作] 欄中的 **[啟動]** 。  
  
3.  Reporting Services 服務的狀態會從 **[已停止]** 變更為 **[已啟動]** 。 如果清單中沒有 Reporting Services 服務，請使用 PowerShell 安裝該服務。  
  
    > [!NOTE]  
    >  如果 Reporting Services 服務停留在 [**啟動**中] 狀態，而未變更為 [**已啟動**]，請確認已在 Windows 伺服器管理員中啟動「SharePoint 2010 系統管理」服務。  

##  <a name="bkmk_create_serrviceapplication"></a>建立 Reporting Services 服務應用程式  
 本節提供建立服務應用程式的步驟，以及屬性的描述 (如果您要檢閱現有的服務應用程式)。  
  
1.  在 SharePoint 管理中心的 **[應用程式管理]** 群組中，按一下 **[管理服務應用程式]** 。  
  
2.  在 SharePoint 功能區中，按一下 **[新增]** 按鈕。  
  
3.  在 [新增] 功能表中，按一下 **[SQL Server Reporting Services 服務應用程式]** 。  
  
    > [!WARNING]  
    >  如果 [[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]] 選項未出現在清單中，表示**未安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共用服務**。 檢閱上一節中，如何使用 PowerShell Cmdlt 來安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務的相關資訊。  
  
4.  在 **[建立新的 SQL Server Reporting Services 服務應用程式]** 頁面中，輸入應用程式的名稱。 如果您要建立多個 Reporting Services 服務應用程式，描述性名稱或命名慣例可協助您安排管理及管理作業工作。  
  
5.  在 **[應用程式集區]** 區段中，建立應用程式的新應用程式集區 (建議)。 針對新應用程式集區，使用與服務應用程式相同的名稱，可讓進行中的管理更容易。  
  
     請針對此應用程式集區選取或建立受管理的帳戶。 請務必指定網域使用者帳戶。 網域使用者帳戶會啟用 SharePoint 受管理帳戶功能，好讓您在一個地方更新密碼和帳戶資訊。 如果您計劃將部署向外延展，以包括在相同識別下執行的其他服務執行個體，也需要網域帳戶。  
  
6.  在 **[資料庫伺服器]** 中，您可以使用目前的伺服器或選擇不同的 SQL Server。  
  
7.  在 **[資料庫名稱]** 中，預設值是 `ReportingService_<guid>`，這是唯一的資料庫名稱。 若您要輸入新值，請輸入唯一值。  
  
8.  在 **[資料庫驗證]** 中，預設值是 Windows 驗證。 如果您選擇 **[SQL 驗證]** ，請參考 SharePoint 管理員指南，以了解有關如何在 SharePoint 部署中使用這個驗證類型的最佳作法。  
  
9. 在 **[Web 應用程式關聯]** 區段中，選取要佈建以供目前 Reporting Services 服務應用程式存取的 Web 應用程式。 您可以建立一個 Reporting Services 服務應用程式與一個 Web 應用程式的關聯。 如果目前所有的 Web 應用程式已有相關聯的 Reporting Services 服務應用程式，則會顯示警告訊息。  
  
10. 按一下 **[確定]** 。  
  
11. 服務應用程式的建立程序會需要數分鐘才能完成。 完成後，您會看到確認訊息及 **[提供訂閱和警示]** 頁面的連結。 如果您想使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱和警示功能，請完成佈建步驟。 如需詳細資訊，請參閱 [SSRS 服務應用程式的佈建訂閱及警示](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)。  
  
 ![PowerShell 相關內容](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell 相關內容")如需使用 PowerShell 建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式的詳細資訊，請參閱[使用 powershell 建立 Reporting Services 服務應用程式](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp)。  
  

  
##  <a name="bkmk_powerview"></a>啟動 Power View 網站集合功能。  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]是 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集的一項功能，它是網站集合功能。 將會針對根網站集合以及安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集之後所建立的網站集合自動啟用此功能。 如果您打算使用 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]，請確認此功能是否已啟用。  
  
 如果您在安裝 SharePoint 2010 產品之後安裝適用於 SharePoint 2010 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集，則只會針對根網站集合啟用報表伺服器整合功能和 Power View 整合功能。 如果是其他網站集合，請手動啟用這些功能。  
  
#### <a name="to-activate-the-power-view-feature"></a>若要啟用 Power View 功能  
  
1.  開啟瀏覽器，移至所要的 SharePoint 網站。  
  
2.  按一下 **[網站動作]** 。  
  
3.  按一下 **[站台設定]** 。  
  
4.  在網站集合管理群組中，按一下 **[網站集合功能]** 。  
  
5.  在清單中尋找 **[Power View 整合功能]** 。  
  
6.  按一下 **[啟用]** 。  
  
 每個網站集合都已完成這個程序。 如需詳細資訊，請參閱[在 SharePoint 中啟用報表伺服器和 Power View 整合功能](../../reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)。  
  
##  <a name="bkmk_additional_config"></a> 其他組態  
 本節描述多數 SharePoint 部署中重要的其他組態步驟。  
  
###  <a name="bkmk_provision_agent"></a> 提供訂閱和警示  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱和資料警示可能需要 SQL Server Agent 權限組態。 如果您看到錯誤訊息，指出需要 SQL Server Agent，且您已確認 SQL Server Agent 正在執行，則請更新權限。 您可以在成功建立服務應用程式頁面上，按一下 **[提供訂閱和警示]** 連結，以移至其他頁面並提供 SQL Server Agent。 如果您的部署跨電腦界限 (例如 SQL Server 資料庫執行個體位於其他電腦上)，則需要提供步驟。 如需詳細資訊，請參閱 [SSRS 服務應用程式的佈建訂閱及警示](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)。  
  

  
### <a name="configure-e-mail-for-a-service-application"></a>設定服務應用程式的電子郵件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料警示功能會以電子郵件訊息傳送警示。 若要傳送電子郵件，您可能需要設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式，以及修改服務應用程式的電子郵件傳遞延伸模組。 如果您計劃針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱功能使用電子郵件傳遞延伸模組，則需要電子郵件設定。 如需詳細資訊，請參閱[設定 Reporting Services 服務應用程式的電子郵件 &#40;SharePoint 2010 和 SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)。  
  

  
### <a name="add-reporting-services-content-types"></a>加入 Reporting Services 內容類型  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會提供預先定義的內容類型，可用來管理共用資料來源 (.rsds) 檔、報表模型 (.smdl) 檔，以及報表產生器的報表定義 (.rdl) 檔。 將 **[報表產生器報表]** 、 **[報表模型]** 和 **[報表資料來源]** 內容類型加入至文件庫會啟用 **[新增]** 命令，讓您能夠建立該類型的新文件。 如需詳細資訊，請參閱[將報表伺服器內容類型加入&#40;至 SharePoint 整合模式&#41;中 Reporting Services 的程式庫](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)。  
  

  
### <a name="activate-the-file-sync-feature"></a>啟用檔案同步處理功能  
 如果使用者經常直接上傳已發行的報表項目至 SharePoint 文件庫，報表伺服器檔案同步處理功能會很有協助。 檔案同步處理功能會更頻繁地同步處理報表伺服器目錄與文件庫中的項目。 如需詳細資訊，請參閱 [在 SharePoint 管理中心啟動報表伺服器檔案同步處理功能](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)。  
  
## <a name="see-also"></a>請參閱  
 [Reporting Services SharePoint 模式的 PowerShell Cmdlet](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)  版本支援的功能  
 [Reporting Services SharePoint 服務和服務應用程式](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)  
