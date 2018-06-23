---
title: 將 SQL Server Database 部署到 Microsoft Azure 虛擬機器 | Microsoft 件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.deploymentwizard.deploymentsettings.f1
- sql12.swb.deploymentwizard.progress.f1
- sql11.swb.usevmdialog.f1
- sql11.swb.deploymentwizard.f1
- sql12.swb.deploymentwizard.azuresignin.f1
- sql11.swb.deploymentwizard.summary.f1
- sql11.swb.deploymentwizard.azuresignin.f1
- sql12.swb.deploymentwizard.f1
- sql12.swb.sqlvmdialog.f1
- sql11.swb.newvmdialog.f1
- sql12.swb.deploymentwizard.results.f1
- sql11.swb.deploymentwizard.progress.f1
- sql12.swb.newvmdialog.f1
- sql12.swb.deploymentwizard.sourcesettings.f1
- sql12.swb.usevmdialog.f1
- sql11.swb.deploymentwizard.sourcesettings.f1
- sql11.swb.deploymentwizard.results.f1
- sql12.swb.deploymentwizard.summary.f1
- sql11.swb.deploymentwizard.deploymentsettings.f1
helpviewer_keywords:
- Deploy a database
- Deploy to Azure VM
- Migrate to Azure
- Windows Azure virtual machine
- Migrate to Azure VM
- Migrate to the cloud
- SQL Server Management Studio
- SSMS
- Deploy database wizard
- Deploy a SQL Server database to Azure
- Azure VM
ms.assetid: 5e82e66a-262e-4d4f-aa89-39cb62696d06
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 976bd24095536f6ae13cf40fab8129154b14864b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134644"
---
# <a name="deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine"></a>將 SQL Server Database 部署到 Microsoft Azure 虛擬機器
  使用 [Deploy a SQL Server Database to a Windows Azure VM Wizard (將 SQL Server 資料庫部署到 Windows Azure VM 精靈)]，將 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體中的資料庫部署到 Windows Azure 虛擬機器 (VM) 中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 此精靈會利用完整的資料庫備份作業，因此它一定會從 SQL Server 使用者資料庫複製完整的資料庫結構描述和資料。 此精靈也會為您執行所有的 Azure VM 組態設定，因此不需要進行 VM 的預先組態設定。  
  
 您不能針對差異備份使用此精靈，因為此精靈將不會覆寫資料庫名稱相同的現有資料庫。 若要取代 VM 上現有的資料庫，您必須先卸除現有資料庫或變更資料庫的名稱。 如果進行中部署作業的資料庫名稱與 VM 上的現有資料庫發生名稱衝突，此精靈將會建議針對進行中的資料庫附加資料庫名稱，好讓您完成作業。  
  
##  <a name="before_you_begin"></a> 開始之前  
 若要完成這個精靈，您必須提供下列資訊並且完成以下組態設定：  
  
-   與您的 Windows Azure 訂用帳戶相關聯的 Microsoft 帳戶詳細資料。  
  
-   您的 Windows Azure 發行設定檔。  
  
    > [!CAUTION]  
    >  SQL Server 目前支援發行設定檔 2.0 版。 若要下載發行設定檔的支援版本，請參閱＜ [下載發行設定檔 2.0](http://go.microsoft.com/fwlink/?LinkId=396421)＞。  
  
-   上傳至您的 Windows Azure 訂用帳戶的管理憑證。  
  
-   儲存到精靈執行所在電腦上個人憑證存放區中的管理憑證。  
  
-   您必須有暫時儲存位置，以供裝載 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的電腦使用。 此暫時儲存位置也必須提供給執行此精靈的電腦使用。  
  
-   如果您將資料庫部署到現有 VM，則必須設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體來接聽 TCP/IP 通訊埠。  
  
-   您打算用來建立 VM 的 Windows Azure VM 或映像庫映像必須已設定 SQL Server 雲端配接器且於執行中。  
  
-   您必須在採用私用連接埠 11435 的 Windows Azure 閘道上，為您的 SQL Server 雲端配接器設定開放式端點。  
  
 此外，如果您打算將資料庫部署到現有的 Windows Azure VM，您也必須能夠提供：  
  
-   裝載 VM 之雲端服務的 DNS 名稱。  
  
-   VM 的系統管理員認證。  
  
-   來自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的來源執行個體，具有您打算部署之資料庫的備份操作員權限的認證。  
  
 如需 Windows Azure 虛擬機器中執行 SQL Server 的詳細資訊，請參閱[準備移轉到 Windows Azure 虛擬機器中 SQL Server](http://msdn.microsoft.com/library/dn133142.aspx)。  
  
 您在執行 Windows Server 作業系統的電腦上，必須使用下列組態設定執行此精靈：  
  
-   關閉增強式安全性設定：使用 [伺服器管理員] > [本機伺服器]，將 Internet Explorer 增強式安全性設定 (ESC) 設為 [關閉]。  
  
-   啟用 JavaScript：[Internet Explorer] > [網際網路選項] > [安全性] > [自訂等級] > [指令碼處理] > [動態指令碼處理]：[啟用]。  
  
###  <a name="limitations"></a> 限制事項  
 此作業的資料庫大小限制為 1 TB。  
  
 適用於 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]的 SQL Server Management Studio 中提供此部署功能。  
  
 這個部署功能只能搭配使用者資料庫使用，不支援部署系統資料庫。  
  
 此部署功能不支援與相似性群組相關聯的託管服務。 例如，不能選取與相似性群組相關聯的儲存體帳戶用於此精靈的 [部署設定]  頁面。  
  
 在 VM 中的 SQL Server 版本必須是與來源 SQL Server 版本相同或更新的版本。 可以使用此精靈部署到 Windows Azure VM 的 SQL Server 資料庫版本：  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 Windows Azure VM 資料庫中執行的 SQL Server 資料庫版本可以部署至：  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 如果進行中部署作業的資料庫名稱與 VM 上的現有資料庫發生名稱衝突，此精靈將會建議針對進行中的資料庫附加資料庫名稱，好讓您完成作業。  
  
###  <a name="filestream"></a> 將啟用 FILESTREAM 的資料庫部署至 Azure VM 的考量  
 所部署資料庫的 FILESTREAM 物件中有儲存的 BLOBS 時，請注意下列指導方針和限制：  
  
-   部署功能無法將啟用 FILESTREAM 的資料庫部署至新的 VM。 如果在您執行精靈之前，FILESTREAM 未在 VM 中啟用，則資料庫還原作業將會失敗，而且精靈作業將無法順利完成。 若要成功部署使用 FILESTREAM 的資料庫，請在啟動精靈之前，於主 VM 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中啟用 FILESTREAM。 如需詳細資訊，請參閱 [FILESTREAM (SQL Server)](http://msdn.microsoft.com/library/gg471497.aspx)。  
  
-   如果您的資料庫使用記憶體中 OLTP，則不需對資料庫進行任何修改，就可將資料庫部署到 Azure VM。 如需詳細資訊，請參閱 [In-Memory OLTP (記憶體中最佳化)](http://msdn.microsoft.com/library/dn133186\(SQL.120\).aspx)。  
  
###  <a name="geography"></a> 資產地理分佈的考量  
 請注意，下列資產必須位於同一個地理區域：  
  
-   雲端服務  
  
-   VM 位置  
  
-   資料磁碟儲存體服務  
  
 如果上列資產並非位於相同位置，則精靈將無法順利完成。  
  
###  <a name="configuration_settings"></a> 精靈組態設定  
 使用下列組態詳細資料修改設定，讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫部署至 Azure VM。  
  
-   **組態檔的預設路徑** - %LOCALAPPDATA%\SQL Server\Deploy to SQL in WA VM\DeploymentSettings.xml  
  
-   **組態檔結構**  
  
    -   \<DeploymentSettings>  
  
        -   <OtherSettings  
  
            -   TraceLevel="偵錯" \<!-- 記錄層次 -->  
  
            -   BackupPath="\\\\[伺服器名稱]\\[磁碟區]\\" \<!-- 上次使用的備份路徑。 做為精靈中的預設值使用。 -->  
  
            -   CleanupDisabled = False /> \<!-- 精靈不會刪除中繼檔和 Windows Azure 物件 (VM、CS、SA)。 -->  
  
        -   <PublishProfile \<!-- 上次使用的發行設定檔資訊。 -->  
  
            -   Certificate="12A34B567890123ABCD4EF567A8" \<!-- 精靈中使用的憑證。 -->  
  
            -   Subscription="1a2b34c5-67d8-90ef-ab12-xxxxxxxxxxxxx" \<!-- 精靈中使用的訂閱。 -->  
  
            -   Name="My Subscription" \<!-- 訂閱的名稱。 -->  
  
            -   Publisher="" />  
  
    -   \</DeploymentSettings>  
  
 **組態檔值**  
  
###  <a name="permissions"></a> Permissions  
 部署的資料庫必須處於正常狀態、資料庫必須可供執行此精靈的使用者帳戶存取，而且使用者帳戶必須擁有執行備份作業的權限。  
  
##  <a name="launch_wizard"></a> 使用將資料庫部署到 Windows Azure VM 精靈  
 **若要啟動此精靈，請使用下列步驟：**  
  
1.  使用 SQL Server Management Studio 連接到具有您想要部署之資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
2.  在 **[物件總管]** 中，展開執行個體名稱，然後展開 **[資料庫]** 節點。  
  
3.  以滑鼠右鍵按一下您要部署的資料庫，選取 **[工作]**，然後選取 **[將資料庫部署到 Windows Azure VM]**。  
  

  
##  <a name="Introduction"></a> 簡介頁面  
 此頁面描述 **[將 SQL Server 資料庫部署至 Windows Azure VM]** 精靈。  
  
 **選項。**  
  
-   **不要再顯示此頁面。** - 按一下此核取方塊可不再顯示 [簡介] 頁面。  
  
-   **下一步** - 繼續進行 **[來源設定]** 頁面。  
  
-   **取消** - 取消作業並關閉精靈。  
  
-   **說明** - 啟動精靈的 MSDN 說明主題。  
  
##  <a name="Source_settings"></a> 來源設定  
 使用此頁面可連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，此執行個體會裝載您要部署至 Windows Azure VM 的資料庫。 您也將指定一個暫存位置給要從本機電腦儲存的檔案使用，然後檔案才會傳送到 Windows Azure。 這個位置可以是共用的網路位置。  
  
 **選項。**  
  
-   按一下 **[連接]** ，然後針對裝載要部署之資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體指定連接詳細資料。  
  
-   使用 **[選取資料庫]** 下拉式清單來指定要部署的資料庫。  
  
-   在 **[其他設定]** 欄位中，指定可供 Windows Azure VM 服務存取的共用資料夾。  
  
##  <a name="Azure_sign-in"></a> Windows Azure 登入  
 使用此頁面可連接到 Windows Azure，並提供管理憑證或發行設定檔詳細資料。  
  
 **選項。**  
  
-   **管理憑證** – 使用這個選項可從本機憑證存放區指定憑證，該憑證符合 Windows Azure 中的管理憑證。  
  
-   **發行設定檔** – 如果您已擁有下載到電腦上的發行設定檔，請使用這個選項。  
  
-   **登入** – 使用這個選項可透過 Microsoft 帳戶登入 Windows Azure (例如 Live ID 或 Hotmail 帳戶)，以便產生並下載新的管理憑證。 請注意，每個訂用帳戶的憑證數目有限。  
  
-   **訂用帳戶** – 選取、輸入或貼上符合本機憑證存放區或發行設定檔之管理憑證的 Windows Azure 訂用帳戶 ID。  
  
##  <a name="Deployment_settings"></a> 部署設定頁面  
 使用此頁面來指定目的地伺服器以及提供新資料庫的詳細資料。  
  
 **選項。**  
  
-   **Azure 虛擬機器** – 針對將裝載 SQL Server 資料庫的 VM 指定詳細資料：  
  
-   **雲端服務名稱** – 指定裝載 VM 的服務名稱。 若要建立新的雲端服務，請為新的雲端服務指定名稱。  
  
-   **虛擬機器名稱** – 指定將裝載 SQL Server 資料庫的 VM 名稱。 若要建立新的 Windows Azure VM，請為新的 VM 指定名稱。  
  
-   **設定** – 使用 [設定] 按鈕來建立可裝載 SQL Server 資料庫的新 VM。 如果您要使用現有的 VM，您提供的資訊將會用來驗證您的認證。  
  
-   **儲存體帳戶** – 從下拉式清單中選取儲存體帳戶。 若要建立新的儲存體帳戶，請為新帳戶指定名稱。 請注意，與相似性群組相關聯的儲存體帳戶將不會在下拉式清單中提供。  
  
-   **目標資料庫** – 指定目標資料庫的詳細資料。  
  
-   **伺服器連接** – 伺服器的連接詳細資料。  
  
-   **資料庫** – 指定或確認新資料庫的名稱。 如果目的地 SQL Server 執行個體上已經有該資料庫名稱存在，建議您指定另一個修改的資料庫名稱。  
  
##  <a name="Summary"></a> 摘要頁面  
 使用此頁面可檢閱此作業的指定設定。 若要使用指定的設定來完成部署作業，請按一下 **[完成]**。 若要取消部署作業並結束精靈，請按一下 **[取消]**。  
  
 將資料庫詳細資料部署到 Windows Azure VM 上的 SQL Server 資料庫可能需要進行手動步驟。 我們將會詳細說明這些步驟。  
  
##  <a name="Results"></a> 結果頁面  
 此頁面會報告部署作業成功或失敗，並顯示每個動作的結果。 發生錯誤的所有動作都會在 **[結果]** 資料行中指出。 按一下連結，即可檢視該動作的錯誤報告。  
  
 按一下 **[完成]** 關閉精靈。  
  
## <a name="see-also"></a>另請參閱  
 [適用 SQL Server 的雲端配接器](../../database-engine/cloud-adapter-for-sql-server.md)   
 [資料庫生命週期管理](../database-lifecycle-management.md)   
 [匯出資料層應用程式](../data-tier-applications/export-a-data-tier-application.md)   
 [匯入 BACPAC 檔案以建立新的使用者資料庫](../data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)   
 [Azure SQL Database 備份及還原](https://msdn.microsoft.com/library/azure/jj650016.aspx)   
 [Windows Azure 虛擬機器上的 SQL Server 部署](http://msdn.microsoft.com/library/dn133141.aspx)   
 [準備移轉到 Windows Azure 虛擬機器中的 SQL Server](http://msdn.microsoft.com/library/dn133142.aspx)  
  
  