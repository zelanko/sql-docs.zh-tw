---
title: "Master Data Services 安裝和組態 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: f6cd850f-b01b-491f-972c-f966b9fe4190
caps.latest.revision: 44
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: da09783f5d8bdcd491f73a1b46390918bbb7dd8d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="master-data-services-installation-and-configuration"></a>Master Data Services 安裝和組態
  本文說明如何在 Windows Server 2012 R2 電腦上安裝 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 、設定 MDS 資料庫與網站，以及部署範例模型和資料。 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) 可讓您的組織管理受信任的資料版本。   
  
> [!NOTE] 
> 當您使用現在支援 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 的 Developer 版本時，可以在 Windows 10 電腦上安裝 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]。 
>>如需不同 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 版本之作業系統支援的詳細資訊，請參閱[安裝 SQL Server 2016 的硬體與軟體需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。 

如需如何在 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]中整理資料的概觀，請參閱 [Master Data Services 概觀 (MDS)](../master-data-services/master-data-services-overview-mds.md)。     
  
 如需 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 新功能的資訊，請參閱[新功能 &#40;Master Data Services&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md)。  
 
如需協助您了解 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 之影片和其他訓練資源的連結，請參閱[了解 Master Data Services](../master-data-services/learn-sql-server-master-data-services.md)。 
  
> **下載**  
>-   若要下載 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]，請前往  **[Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2017-ctp/)**。  
>-   有 Azure 帳戶嗎？  接著前往**[這裡](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**來啟動已安裝 SQL Server 的虛擬機器。  
 
> **無法建立 MDS 網站？**
>>如需如何解決此問題的指示，請參閱這份 Microsoft 技術支援文件。
[無法透過 SQL Server 2016 中的低權限帳戶建立 MDS 網站](https://aka.ms/mdssupport) 

## <a name="internet-explorer-and-silverlight"></a>Internet Explorer 和 Silverlight
- 當您在 Windows Server 2012 電腦上安裝 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 時，可能需要設定 Internet Explorer 增強式安全性，以允許 Web 應用程式網站的指令碼。 否則，瀏覽至伺服器電腦上的網站將會失敗。
- 若要在 Web 應用程式中工作，用戶端電腦必須安裝 Silverlight 5。 如果您沒有必要的 Silverlight 版本，系統將會在您巡覽至需要 Silverlight 的 Web 應用程式區域時提示安裝 Silverlight。 您可以從**這裡[](https://www.microsoft.com/silverlight/)**安裝 Silverlight 5。

## <a name="includessmdsshortmdincludesssmdsshort-mdmd-on-an-azure-virtual-machine"></a>Azure 虛擬機器上的 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]
根據預設，當您啟動已安裝 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 的 Azure 虛擬機器時，也會一併安裝 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]。 

您的下一個步驟是安裝 Internet Information Services (IIS)。 請參閱[安裝和設定 IIS](#InstallIIS) 一節。 

如果您想要變更 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 安裝，請在預設位置 `<drive>`:\SQLServer_13.0_Full 中找到 setup.exe 檔案。
  
## <a name="InstallMDS"></a> 安裝 Master Data Services  
 您可以使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝程式或命令提示字元來安裝 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]。  
  
 **在 Windows Server 2012 R2 電腦上使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝程式安裝 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]**  
  
1.  按兩下 Setup.exe，並遵循安裝精靈中的步驟。  
  
2.  在 [功能選擇] 頁面中，選取 [共用功能] 底下的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]。  
  
     隨即安裝 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]、組件、Windows PowerShell 嵌入式管理單元，以及 Web 應用程式與服務的資料夾和檔案。  
  
     ![mds_SQLServer2016Setup_FeatureSelection](../master-data-services/media/mds-sqlserver2016setup-featureselection.png "mds_SQLServer2016Setup_FeatureSelection")  
  
3.  完成安裝精靈。  

## <a name="InstallIIS"></a> 安裝和設定 IIS
  
1.  在 [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]中，按一下 **桌面** 工作列上的 **伺服器管理員**圖示。  
  
     ![Windows Server 2012 工作列中的伺服器管理員圖示](../master-data-services/media/mds-windowsservertaskbar-servermanagericon.png "Windows Server 2012 工作列中的伺服器管理員圖示")  
  
5.  在 [伺服器管理員] 中，按一下 [管理] 功能表上的 [新增角色及功能]。  
   
     ![[伺服器管理] 中的 [新增角色及功能] 功能表命令](../master-data-services/media/mds-servermanagerdashboard-addrolesfeaturesmenu.png "[伺服器管理] 中的 [新增角色及功能] 功能表命令")  
  
6.  在 [新增角色及功能精靈] 的 [安裝類型]  頁面中，接受預設值 ([角色型或功能型安裝])，然後按一下 [下一步]。  
  
7.  按一下 [從伺服器集區選取伺服器]，然後按一下已安裝 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 的伺服器。  
  
     ![mds_AddRolesFeaturesWizard_ServerSelectionPage](../master-data-services/media/mds-addrolesfeatureswizard-serverselectionpage.png) 
  
8. 在 [伺服器角色] 頁面上，按一下 [網頁伺服器]，然後按一下 [下一步]。 

   ![mds_AddRolesFeaturesWizard_ServerRolesPage](../master-data-services/media/mds-addrolesfeatureswizard-serverrolespage.png)
   
9. 在 [功能] 頁面上，確認已選取下列功能，然後按一下 [下一步]。 在 [!INCLUDE[winblue_server_2_md](../includes/winblue-server-2-md.md)] 上，[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 需要這些功能。
  
    |功能|功能|  
    |--------------|--------------|  
    |![mds_AddRolesFeaturesWizard_FeaturesPage](../master-data-services/media/mds-addrolesfeatureswizard-featurespage.png)|![mds_AddRolesFeaturesWizard_FeaturesPage_WindowsProcActive](../master-data-services/media/mds-addrolesfeatureswizard-featurespage-windowsprocactive.png)|  

10. 在左窗格中，按一下 [網頁伺服器角色 (IIS)]，然後按一下 [角色服務]。
11. 在 [角色服務] 頁面上，確認已選取下列服務，然後按一下 [下一步]。 在 [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)] 上，[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 需要這些功能。

    > [!WARNING]  
    >  請不要安裝 WebDAV 發佈角色服務。 因為，WebDAV 發佈與 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]不相容。  
  
     |角色服務|角色服務|  
    |-----------------------------|-----------------------------|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_PerformSecurity](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-performsecurity.png)|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage_AppDevsection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-appdevsection.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_ManageToolssection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-managetoolssection.png)|  
    |||  
  
     如需其他作業系統之必要功能和角色服務的清單，請參閱 [Web 應用程式需求 &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)。   
  
 如需使用安裝程式來安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的詳細資訊，請參閱[從安裝精靈 &#40;安裝程式&#41; 安裝 SQL Server 2016](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。  
  
 如需使用命令提示字元安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的詳細資訊，請參閱[從命令提示字元安裝 SQL Server 2016](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。 當您使用命令提示字元時， [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 可當做功能參數。  
  
 如需安裝前工作的簡短描述與詳細資訊連結，請參閱 [安裝 Master Data Services](../master-data-services/install-windows/install-master-data-services.md)。  
  
##  <a name="SetUpWeb"></a> 設定資料庫和網站  
 **使用 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]設定資料庫和網站**  

 
> [!WARNING]  
    >  您必須先[安裝 IIS](#InstallIIS)，再啟動 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 組態管理員。 否則，組態管理員會顯示 Internet Information Services 錯誤，並且無法建立 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Web 應用程式。  
    
> **瀏覽器需求**
>>[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Web 應用程式僅適用於 Internet Explorer (IE) 9 或更新版本。 不支援 IE 8 和更早版本、Microsoft Edge 和 Chrome。    
  
1.  啟動 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]，並按一下左窗格的 [資料庫組態]。  
  
2.  按一下 [建立資料庫]，然後按一下 [建立資料庫精靈] 中的 [下一步]。  
  
3.  在 [資料庫伺服器] 頁面上，選取 [驗證類型]，然後按一下 [測試連接] 確認您可以使用所選驗證類型的認證連接到資料庫。 按一下 **[下一步]**。
  
    > [!NOTE]  
    >  若您選取 [目前使用者 - 整合式安全性] 做為驗證類型，[使用者名稱] 方塊會是唯讀的，並顯示登入電腦的 Windows 使用者帳戶名稱。 如果您要在 Azure 虛擬機器 (VM) 上執行 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]，則 [使用者名稱] 方塊會顯示 VM 名稱以及 VM 上本機系統管理員帳戶的使用者名稱。 

    ![mds_2016ConfigManager_CreateDatabaseWizard_ServerPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-serverpage.png)  
  
4.  在 [資料庫名稱] 欄位中輸入名稱。 (選擇性) 若要選取 Windows 定序，請清除 [SQL Server 預設定序] 核取方塊，然後按一下一或多個可用選項 (例如 [區分大小寫])。 按一下 **[下一步]**。

    ![mds_2016ConfigManager_CreateDatabaseWizard_DatabasePage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-databasepage.png)  
  
     如需 Windows 定序的詳細資訊，請參閱 [Windows 定序名稱 (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx)。  
  
5.  在 [使用者名稱] 欄位中，指定要成為預設 Master Data Services 進階使用者的 Windows 使用者帳戶。 進階使用者具有所有功能區域的存取權，並可新增、刪除及更新所有模型。  

    ![mds_2016ConfigManager_CreateDatabaseWizard_AdminPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-adminpage.png)  
  
6.  按一下 [下一步] 檢視 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的設定摘要，然後按一下 [下一步] 建立資料庫。 [進度和完成] 頁面隨即出現。

7. 建立和設定資料庫時，請按一下 [完成]。  
  
     如需 [建立資料庫精靈] 中的設定詳細資訊，請參閱[建立資料庫精靈 &#40;Master Data Services 組態管理員&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md)。  
  
7.  在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 的 [資料庫組態] 頁面上，按一下 [選取資料庫]。  
  
8.  按一下 [連接]，並選取您在步驟 7 中建立的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫，然後按一下 [確定]。 

    ![mds_2016ConfigManager_SelectDatabaseButton_ConnectToDatabaseDialog](../master-data-services/media/mds-2016configmanager-selectdatabasebutton-connecttodatabasedialog.png)  
  
     您已完成資料庫的設定程序。 現在，[資料庫組態] 頁面即會顯示您為 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]已建立的資料庫和目前的資料庫版本連接的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體。  

    ![mds_2016ConfigManager_DatabaseConfig_Completed](../master-data-services/media/mds-2016configmanager-databaseconfig-completed.png)   
  
9. 在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中，按一下左窗格的 [Web 組態]。  
  
10. 在 [網站] 清單方塊中，按一下 [預設的網站]，然後按一下 [建立] 以建立 Web 應用程式。  
  
    > [!NOTE]  
    >  當您選取 [預設的網站] 時，必須建立 Web 應用程式。 如果您選取清單方塊中的 [建立新網站]，即會自動建立應用程式。  

     ![mds_2016ConfigManager_WebConfig](../master-data-services/media/mds-2016configmanager-webconfig.png)  
  
11. 在 [應用程式集區] 區段中，執行下列其中一個動作：  
  
    -   輸入您在步驟 5 中為資料庫 [系統管理員帳戶] 輸入的相同使用者名稱，並輸入密碼，然後按一下 [確定]。  
  
         **-或-**  
  
    -   選取其他使用者名稱，並輸入密碼，然後按一下 [確定]。  
  
         您可以使用與建立資料庫和 Web 應用程式時所用的不同帳戶。  

        ![mds_2016ConfigManager_WebConfig_CreateWebApplication](../master-data-services/media/mds-2016configmanager-webconfig-createwebapplication.png)   
  
     如需 [建立 Web 應用程式] 對話方塊的詳細資訊，請參閱[建立 Web 應用程式對話方塊 &#40;Master Data Services 組態管理員&#41;](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md)。  
  
12. 在 [Web 組態] 頁面的 [Web 應用程式] 方塊中，按一下您已建立的應用程式，然後按一下 [將應用程式與資料庫產生關聯] 區段中的 [選取]。  
  
13. 按一下 [連接]，並選取您想要與 Web 應用程式產生關聯的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫，然後按一下 [確定]。  
  
     您已完成網站的設定程序。 現在，[Web 組態] 頁面即會顯示您所選的網站、所建立的 Web 應用程式以及資料庫的相關聯 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 應用程式。  

     ![mds_2016ConfigManager_WebConfig_Completed](../master-data-services/media/mds-2016configmanager-webconfig-completed.png)  
 
     
15. 按一下 **[套用]**。 [組態完成] 訊息方塊隨即顯示。 按一下訊息方塊中的 [確定]，以啟動 Web 應用程式。 網站網址為 http://*伺服器名稱*/*Web 應用程式*/。 


![mds_2016ConfigurationComplete_MessageBox](../master-data-services/media/mds-2016configurationcomplete-messagebox.png) 
  
     For more information about the settings on the Web Configuration page, see [Web Configuration Page &#40;Master Data Services Configuration Manager&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
 您也可以使用 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 指定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫之相關聯 Web 應用程式與服務的其他設定。 例如，您可以指定載入資料的頻率，或傳送驗證電子郵件的頻率。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)。  
  
##  <a name="deploySample"></a> 部署範例模型和資料  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]包含下列三個範例模型套件。   這些範例模型都含有資料。 **範例模型套件的預設位置是 %programfiles%\Microsoft SQL Server\140\Master Data Services\Samples\Packages。**
  
-   chartofaccounts_en.pkg  
  
-   customer_en.pkg  
  
-   product_en.pkg  
  
 您可以使用 MDSModelDeploy 工具來部署套件。 MDSModelDeploy 工具的預設位置是 <磁碟機>\Program Files\Microsoft SQL Server\ 140\Master Data Services\Configuration。  
  
 如需執行此工具之必要條件的詳細資訊，請參閱 [使用 MDSModelDeploy 部署模型部署封裝](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)。  
  
 如需可支援 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中新功能的資料更新資訊，請參閱 [SQL Server 範例︰模型部署套件 (MDS)](../master-data-services/sql-server-samples-model-deployment-packages-mds.md)。  
  
 **部署範例模型**  
  
1.  將範例模型套件複製到 *drive*\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration。  
  
2.  執行下列命令，以開啟 [系統管理員:] 命令提示字元，並導覽至 MDSModelDeploy.exe。  
  
    ```  
    cd c:\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration  
    ```  
  
3.  執行下列每一個命令，以將每個範例模型部署至 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 。  
  
    > [!IMPORTANT]  
    >  在下列範例中，會指定 `MDS1` 服務值。 如果您在設定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 網站時選取了 [預設的網站]，請使用這個值 。  請參閱[設定資料庫和網站](#SetUpWeb)一節。  
    >   
    >  如果您已建立新的網站或選取了其他現有的網站，請先執行下列命令，以判斷正確的服務值。  
    >   
    >  `MDSModelDeploy listservices`  
    >   
    >  傳回的值清單中的第一個服務值，就是您指定要部署模型的目標。  
    >
    > [!NOTE]
    > 若要深入了解範例模型的中繼資料資訊，請參閱下列位置中的讀我檔案："c:\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration"
    >
   
     **部署 chartofaccounts_en.pkg 範例模型**  
  
    ```  
    MDSModelDeploy deploynew -package chartofaccounts_en.pkg -model ChartofAccounts -service MDS1  
    ```  
  
     **部署 customer_en.pkg 範例模型**  
  
    ```  
    MDSModelDeploy deploynew -package customer_en.pkg -model Customer -service MDS1  
    ```  
  
     **部署 product_en.pkg 範例模型**  
  
    ```  
    MDSModelDeploy deploynew -package product_en.pkg -model Product -service MDS1  
  
    ```  
  
     成功部署模型時，即會顯示 [MDSModelDeploy 作業成功完成] 訊息。  
  
     下圖顯示部署 product_en.pkg 範例模型的命令。  
  
     ![部署產品範例模型的命令列](../master-data-services/media/mds-commandprompt-deployingsamplemodel-product.png "部署產品範例模型的命令列")  
  
4.  若要檢視範例模型，請執行下列動作：  
  
    1.  瀏覽至您設定的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 網站。 請參閱 [設定資料庫和網站](#SetUpWeb) 一節。  
  
         網站網址為 http://*伺服器名稱*/*Web 應用程式*/。  
  
    2.  從 [模型] 清單方塊中選取一個模型，然後按一下 [總管]。  
  
         ![MDS 網站、首頁。](../master-data-services/media/mds-mdswebsite-homepage-selectsamplemodel.png "MDS 網站、首頁。")  
  
## <a name="next-step"></a>下一個步驟  
 為資料建立新的模型和實體。 請參閱[建立模型 &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md) 和[建立實體 &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)。  
  
 如需如何在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中使用模型和實體來建立資料結構的概觀，請參閱 [Master Data Services 概觀 &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)。  
  
## <a name="did-this-article-help-you-were-listening"></a>這篇文章對您有幫助嗎？ 我們會持續聽取您的意見  
 您要尋找哪些資訊？找到了嗎？ 我們會持續聽取您的意見來改進內容。 請將您的意見傳送到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Get%20Started%20with%20Master%20Data%20Services)  
  
## <a name="see-also"></a>另請參閱  
 [Master Data Services 資料庫](../master-data-services/master-data-services-database.md)   
 [主資料管理員 Web 應用程式](../master-data-services/master-data-manager-web-application.md)   
 [資料庫組態頁面 &#40;Master Data Services 組態管理員&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Master Data Services &#40;MDS&#41; 的新功能](../master-data-services/what-s-new-in-master-data-services-mds.md)  
  
  

