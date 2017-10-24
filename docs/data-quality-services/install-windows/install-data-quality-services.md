---
title: "安裝 Data Quality Services | Microsoft Docs"
ms.custom: 
ms.date: 09/11/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 486e4216-a946-4c6e-828c-61bc905f7ec1
caps.latest.revision: 49
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1df54edd5857ac2816fa4b164d268835d9713638
ms.openlocfilehash: 6162b52153b29fbe1069f62361fa89eac234dc1c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/12/2017

---
# <a name="install-data-quality-services"></a>安裝 Data Quality Services
  [!INCLUDE[ssDQSnoversionLong](../../includes/ssdqsnoversionlong-md.md)] (DQS) 包含以下兩個元件： **[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]** 和 **[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]**。  
  
|DQS 元件|描述|  
|-------------------|-----------------|  
|[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]|[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 會安裝在 [!INCLUDE[ssNoversion](../../includes/ssNoVersion-md.md)] Database Engine 之上，並且包含三個資料庫：DQS_MAIN、DQS_PROJECTS 和 DQS_STAGING_DATA。 DQS_MAIN 包含 DQS 預存程序、DQS 引擎和已發行的知識庫。 DQS_PROJECTS 包含資料品質專資訊。 DQS_STAGING_DATA 是暫存區域，您可以從中複製來源資料以執行 DQS 作業，然後匯出已處理的資料。|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] 是可以用於連接到 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]的獨立應用程式，其提供高直覺性的圖形化使用者介面，讓您可以執行資料品質作業，以及其他與 DQS 相關的管理工作。|  
  
> [!IMPORTANT]  
>  除了上述兩項 DQS 元件之外，您也可以：  
>   
>  使用 Integration Services 中的 DQS 清理轉換，在 Integration Services 封裝程序中執行資料清除；當您安裝 Integration Services 時，系統會自動安裝此元件。 如需安裝 Integration Services 的資訊，請參閱 [安裝 Integration Services](../../integration-services/install-windows/install-integration-services.md)。  
>   
>  在 Master Data Services 中啟用 DQS 整合，以便在 Master Data Services Add-in for Excel 中使用 DQS 相符的功能。 如需相關資訊，請參閱 [啟用 Data Quality Services 與 Master Data Services 的整合](../../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md)。  
  
 DQS 安裝程序包含三個部分：  
  
-   [安裝前工作](#PreInstallationTasks)：安裝 DQS 之前，先確認系統需求。  
  
-   [Data Quality Services 安裝工作](#DQSInstallation)︰使用 SQL Server 安裝程式安裝 DQS。  
  
-   [安裝後工作](#PostInstallationTasks)：完成 SQL Server 安裝程式之後，執行這些工作來完成安裝 DQS。  
  
> [!NOTE]  
>  本主題不包含從命令列執行安裝程式的指示。 如需安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 和用戶端之命令列選項的資訊，請參閱[從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Feature) 中的[功能參數](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
##  <a name="PreInstallationTasks"></a> 安裝前工作  
 安裝 DQS 之前，請先確認您的電腦符合最低系統需求。 下表提供 DQS 元件之最低系統需求的相關資訊：  
  
|DQS 元件|最低系統需求|  
|-------------------|---------------------------------|  
|[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]|記憶體 (RAM)：最低需求︰2 GB / 建議值︰4 GB 以上<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] Database Engine。 如需詳細資訊，請參閱 [安裝 SQL Server Database Engine](../../database-engine/install-windows/install-sql-server-database-engine.md)。|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|.NET Framework 4.0 (若未安裝，將會在安裝 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] 期間加以安裝)<br /><br /> Internet Explorer 6.0 SP1 或更新的版本|  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 和 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] 可以安裝在同一部電腦或不同的電腦上。 這兩個元件可以任意順序個別進行安裝。 但如果要使用 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]，必須安裝可供連接的 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 。  
>   
>  您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 的最新版或舊版以及 DQS 清理轉換來連接到 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 的 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] 版本。 如需將 DQS 現有版本升級至 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]的相關資訊，請參閱 [升級 Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md)。  
>   
>  儘管 Microsoft Excel 不是安裝 Data Quality Client 的必要條件，仍須將 Microsoft Excel 2003 安裝在 Data Quality Client 電腦上以執行各種用戶端應用程式中的作業，例如從 Excel 檔案匯入定義域值，或是針對知識探索、清理或比對活動對應 Excel 檔案中的來源資料。  
  
 如需安裝 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 之最低系統需求的詳細資訊，請參閱[安裝 SQL Server 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。  
  
##  <a name="DQSInstallation"></a> Data Quality Services 安裝工作  
 您必須使用 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 安裝程式安裝 DQS 元件。 當您執行 SQL Server 安裝程式時，必須執行一連串的安裝精靈頁面，依據您的需求選取適當的選項。 下表只列出安裝精靈中的部分頁面，您在這些頁面中選取的選項將會影響 DQS 的安裝：  
  
|頁面|動作|  
|----------|------------|  
|特徵選取|選取：<br /><br /> [Database Engine Services] 底下的 [Data Quality Services] 以安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]。 <br />如果您選取 [Data Quality Services] 核取方塊，SQL Server 安裝程式會複製位於電腦上 SQL Server 執行個體目錄底下的 Installer 檔案 DQSInstaller.exe。 在您完成 SQL Server 安裝程式之後，必須執行這個檔案才能「完成」[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 的安裝。 此外，您也必須執行一些額外的步驟來設定 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]，然後才能使用它。 如需詳細資訊，請參閱[安裝後工作](#PostInstallationTasks)。<br /><br /> [Data Quality Client] 以安裝 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]。<br /><br /> (建議) [管理工具 - 基本] 底下的 [管理工具 - 完整]，以安裝 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 此工具可為您提供圖形使用者介面以管理 SQL Server 執行個體，並且協助您在安裝後執行額外的工作，如下一節中所列。|  
|Database Engine 組態|按一下 [加入目前使用者]，將使用者的 Windows 帳戶加入系統管理員固定伺服器角色。 您稍後必須能夠執行 DQSInstaller.exe 檔案以完成 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 安裝。|  
  
##  <a name="PostInstallationTasks"></a> 安裝後工作  
 完成 SQL Server 安裝精靈之後，您必須執行本節所述的額外步驟，才能完成 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 的安裝、進行設定，然後使用它。  
  
1.  若要完成 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 安裝，請執行 DQSInstaller.exe 檔案。 執行 DQSInstaller.exe 檔案時：  
  
    -   會建立 DQS_MAIN、DQS_PROJECTS 及 DQS_STAGING_DATA 資料庫。  
  
    -   會建立 ##MS_dqs_db_owner_login## 及 ##MS_dqs_service_login## 登入。  
  
    -   會在 DQS_MAIN 資料庫中建立 dqs_administrator、dqs_kb_editor 及 dqs_kb_operator 角色。  
  
    -   master 資料庫中會建立 DQInitDQS_MAIN 預存程序。  
  
    -   通常會在 C:\Program Files\Microsoft SQL Server\MSSQL13.<執行個體名稱>\MSSQL\Log 資料夾中建立 DQS_install.log 檔案。 此檔案包含執行 DQSInstaller.exe 檔案時所執行之動作相關的資訊。  
  
    -   如果 Master Data Services 當做 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]，存在於相同的 SQL Server 執行個體中，則會建立對應到 Master Data Services 登入的使用者，並且授與該使用者 DQS_MAIN 資料庫的 dqs_administrator 角色。  
  
     這樣就完成 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 安裝。  
  
     如需詳細資訊，請參閱 [執行 DQSInstaller.exe 完成 Data Quality Server 安裝](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)。  
  
2.  對使用者授與 DQS 角色：  
  
     若要使用 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 登入 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]，使用者必須具備 DQS_MAIN 資料庫的下列三個角色之一：  
  
    -   **dqs_administrator**  
  
    -   **dqs_kb_editor**  
  
    -   **dqs_kb_operator**  
  
     根據預設，如果您的使用者帳戶是系統管理員 (sysadmin) 固定伺服器角色的成員，即使沒有將任何 DQS 角色授與您的使用者帳戶，還是可以使用 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 登入 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] 。 如需有關三個 DQS 角色的詳細資訊，請參閱＜ [DQS 安全](../../data-quality-services/dqs-security.md)＞。  
  
     如需詳細資訊，請參閱 [對使用者授與 DQS 角色](../../data-quality-services/install-windows/grant-dqs-roles-to-users.md)。  
  
    > [!NOTE]  
    >  這三個 DQS 角色不適用於 DQS_PROJECTS 和 DQS_STAGING_DATA 資料庫。  
  
3.  讓您的資料可用於 DQS 作業。 確認您可以存取 DQS 作業的來源資料，並且能夠將已處理的資料匯出到資料庫中的某個資料表。  
  
     如需詳細資訊，請參閱  
                    [存取用於 DQS 作業的資料](../../data-quality-services/install-windows/access-data-for-the-dqs-operations.md)。  
  
## <a name="see-also"></a>另請參閱  
 [視訊：安裝和設定 DQS](http://go.microsoft.com/fwlink/?LinkId=238241)   
 [在 .NET Framework 更新之後升級 SQLCLR 組件](../../data-quality-services/install-windows/upgrade-sqlclr-assemblies-after-net-framework-update.md)   
 [使用 DQSInstaller.exe 匯出及匯入 DQS 知識庫](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)   
 [升級 Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md)   
 [移除 Data Quality Server 物件](../../sql-server/install/remove-data-quality-server-objects.md)   
 [安裝 SQL Server Business Intelligence 功能](../../sql-server/install/install-sql-server-business-intelligence-features.md)   
 [解除安裝 SQL Server](../../sql-server/install/uninstall-sql-server.md)   
 [Data Quality Services](../../data-quality-services/data-quality-services.md)   
 [針對 DQS 中的安裝和組態問題進行疑難排解](http://social.technet.microsoft.com/wiki/contents/articles/3776.aspx)  
  
  
