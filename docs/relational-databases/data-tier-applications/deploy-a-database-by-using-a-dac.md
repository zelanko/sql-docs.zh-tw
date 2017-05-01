---
title: "使用 DAC 部署資料庫 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dbdeployment.settings.f1
- sql13.swb.dbdeployment.progress.f1
- sql13.swb.dbdeployment.summary.f1
- sql13.swb.dbdeployment.results.f1
- sql13.swb.dbdeployment.welcome.f1
helpviewer_keywords:
- deploy database wizard
- database deploy [SQL Server]
ms.assetid: 08c506e8-4ba0-4a19-a066-6e6a5c420539
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 57703923bd142330e2a46e72eb4faaee18fa7285
ms.lasthandoff: 04/11/2017

---
# <a name="deploy-a-database-by-using-a-dac"></a>使用 DAC 來部署資料庫
  使用 [將資料庫部署到 SQL Azure]  精靈，在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體與 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 伺服器之間部署資料庫，或在兩個 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]伺服器之間部署資料庫。  
  
##  <a name="BeforeBegin"></a> 開始之前  
 精靈會使用資料層應用程式 (DAC) BACPAC 封存檔案，來部署資料和資料庫物件的定義。 它會從來源資料庫執行 DAC 匯出作業並對目的地資料庫執行 DAC 匯入。  
  
###  <a name="DBOptSettings"></a> 資料庫選項和設定  
 根據預設，部署期間建立的資料庫將會擁有 CREATE DATABASE 陳述式中的預設值。 例外是資料庫定序和相容性層級會設定為來源資料庫中的值。  
  
 資料庫選項 (例如 TRUSTWORTHY、DB_CHAINING 和 HONOR_BROKER_PRIORITY) 無法在部署過程中調整。 實體屬性 (如檔案群組數目或檔案數目和大小) 無法在部署過程中更改。 部署完成之後，您可以使用 ALTER DATABASE 陳述式、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 來修改資料庫。  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
 **[部署資料庫]** 精靈支援在下列項目上部署資料庫：  
  
-   從 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體至 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。  
  
-   從 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 至 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體。  
  
-   兩個 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 伺服器之間。  
  
 精靈不支援在兩個 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體之間部署資料庫。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體必須執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) 或更新版本，才能使用精靈。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體上的資料庫物件不受 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]支援，則無法使用此精靈將資料庫部署到 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。 如果 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 上的資料庫物件不受 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援，則無法使用此精靈將資料庫部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。  
  
###  <a name="Security"></a> 安全性  
 為了提高安全性，SQL Server 驗證登入會儲存在 DAC BACPAC 檔案中，而且沒有密碼。 當您匯入 BACPAC 之後，此登入會建立為停用的登入，而且會產生密碼。 若要啟用登入，請使用具有 ALTER ANY LOGIN 權限的登入進行登入，並使用 ALTER LOGIN 來啟用登入，然後指派可以傳達給使用者的新密碼。 Windows 驗證登入不需要這項處理，因為這類登入的密碼不是由 SQL Server 所管理。  
  
#### <a name="permissions"></a>Permissions  
 精靈需要來源資料庫的 DAC 匯出權限。 登入至少需要 ALTER ANY LOGIN 和資料庫範圍 VIEW DEFINITION 權限，以及 **sys.sql_expression_dependencies**的 SELECT 權限。 匯出 DAC 可以透過 securityadmin 固定伺服器角色的成員來完成，這個角色的成員也是匯出 DAC 之來源資料庫中 database_owner 固定資料庫角色的成員。 系統管理員固定伺服器角色的成員或內建 SQL Server 系統管理員帳戶 **sa** 也可以匯出 DAC。  
  
 精靈需要目的地執行個體或伺服器的 DAC 匯入權限。 登入必須是 **系統管理員 (sysadmin)** 或 **伺服器管理員 (serveradmin)** 固定伺服器角色的成員，或是具有 **dbcreator** 固定伺服器角色及擁有 ALTER ANY LOGIN 權限。 名為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sa **的內建** 系統管理員帳戶也可以匯入 DAC。 將具有登入的 DAC 匯入至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ，需要 loginmanager 或 serveradmin 角色的成員資格。 將不具有登入的 DAC 匯入至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ，需要 dbmanager 或 serveradmin 角色的成員資格。  
  
##  <a name="UsingDeployDACWizard"></a> 使用部署資料庫精靈  
 **若要使用部署資料庫精靈移轉資料庫**  
  
1.  連接至您要部署的資料庫位置。 您可以指定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體或 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 伺服器。  
  
2.  在 **[物件總管]**中，展開含有資料庫的執行個體的節點。  
  
3.  展開 **[資料庫]** 節點。  
  
4.  以滑鼠右鍵按一下您要部署的資料庫，選取 **[工作]**，然後選取 **[將資料庫部署到 SQL Azure]**。  
  
5.  完成精靈對話方塊：  
  
    -   [簡介頁面](#Introduction)  
  
    -   [部署設定](#Deployment_settings)  
  
    -   [摘要頁面](#Summary)  
  
    -   [進度](#Progress)  
    
    -   [結果](#Results)  
  
##  <a name="Introduction"></a> 簡介頁面  
 此頁面描述 **[部署資料庫]** 精靈的步驟。  
  
 **選項**  
  
-   **不要再顯示此頁面。** - 按一下此核取方塊，之後就不會再顯示 [簡介] 頁面。  
  
-   **下一步** - 繼續進行 **[部署設定]** 頁面。  
  
-   **取消** - 取消作業並關閉精靈。  
  
##  <a name="Deployment_settings"></a> 部署設定頁面  
 使用此頁面來指定目的地伺服器以及提供新資料庫的詳細資料。  
  
 **本機主機：**  
  
-   **伺服器連接** - 指定伺服器連接的詳細資料，然後按一下 **[連接]** 來驗證連接。  
  
-   **新資料庫名稱** - 指定新資料庫的名稱。  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 資料庫設定：**  
  
-   **[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 版本** - 從下拉式功能表中選取 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的版本。  
  
-   **資料庫大小上限** - 從下拉式功能表中選取資料庫大小上限。  
  
 **其他設定：**  
  
-   指定暫存檔 (即 BACPAC 封存檔案) 的本機目錄。 請注意，檔案將在指定的位置上建立，而且作業完成之後，將保留在該位置。  
  
##  <a name="Summary"></a> 摘要頁面  
 您可以使用此頁面來檢閱作業的指定來源和目標設定。 若要使用指定的設定來完成部署作業，請按一下 **[完成]**。 若要取消部署作業並結束精靈，請按一下 **[取消]**。  
  
##  <a name="Progress"></a> 進度頁面  
 此頁面會顯示進度列，指出作業的狀態。 若要檢視詳細狀態，請按一下 **[檢視詳細資料]** 選項。  
  
##  <a name="Results"></a> 結果頁面  
 此頁面會報告部署作業成功或失敗，並顯示每個動作的結果。 發生錯誤的所有動作在 **[結果]** 資料行中都會有一個連結。 按一下連結，即可檢視該動作的錯誤報告。  
  
 按一下 **[完成]** 關閉精靈。  
  
## <a name="using-a-net-framework-application"></a>使用 .Net Framework 應用程式  
 **在 .Net Framework 應用程式中使用 DacStoreExport() 與 Import() 方法，以部署資料庫。**  
  
 若要檢視程式碼範例，請下載 [Codeplex](http://go.microsoft.com/fwlink/?LinkId=219575)上的 DAC 範例應用程式。  
  
1.  建立 SMO Server 物件，並將它設定為包含要部署之資料庫的執行個體或伺服器。  
  
2.  開啟 **ServerConnection** 物件，並連接到相同的執行個體。  
  
3.  使用 **Export** 類型的 **Microsoft.SqlServer.Management.Dac.DacStore** 方法，將資料庫匯出至 BACPAC 檔案。 指定要匯出之資料庫的名稱，以及要放置 BACPAC 檔案之資料夾的路徑。  
  
4.  建立 SMO Server 物件，並將它設定為目的地執行個體或伺服器。  
  
5.  開啟 **ServerConnection** 物件，並連接到相同的執行個體。  
  
6.  使用 **Import** 類型的 **Microsoft.SqlServer.Management.Dac.DacStore** 方法，匯入 BACPAC。 指定匯出所建立的 BACPAC 檔案。  
  
## <a name="see-also"></a>另請參閱  
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [匯出資料層應用程式](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)   
 [匯入 BACPAC 檔案以建立新的使用者資料庫](../../relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)  
  
  
