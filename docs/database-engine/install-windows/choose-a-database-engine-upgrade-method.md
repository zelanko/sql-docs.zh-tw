---
title: "選擇 Database Engine 升級方法 | Microsoft Docs"
ms.custom: ""
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5e57a427-2e88-4ef6-b142-4ccad97bcecc
caps.latest.revision: 23
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 23
---
# 選擇 Database Engine 升級方法
  當您為了讓停機時間及風險減到最少，而打算將 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 從舊版 SQL Server 升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時，有多種方法可以考慮。 您可以就地執行升級、遷移到新的安裝或執行輪流升級。 下圖將協助您在這些方法中做出選擇。 下方也將討論圖表中的各個方法。 為協助您了解圖表中的決策點，另請檢閱 [Plan and Test the Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)。  
  
 ![Database Engine Upgrade Method Decision Tree](../../database-engine/install-windows/media/database-engine-upgrade-method-decision-tree.png "Database Engine Upgrade Method Decision Tree")  
  
 **下載**  
  
-   若要下載 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，請前往  **[評估中心](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**。  
  
-   有 Azure 帳戶嗎？  接著前往 **[這裡](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016ctp2evaluationwindowsserver2012r2/?wt.mc_id=sqL16_vm)** ，來加速已安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的虛擬機器。  
  
> [!NOTE]  
>  您也可以考慮在升級計畫中升級 Azure SQL Database，或將您的 SQL Server 環境虛擬化。 這些主題不在本主題範圍內，但此處提供幾個連結：[SQL Server 2016 混合式雲端簡介](../Topic/Introduction%20to%20SQL%20Server%202016%20Hybrid%20Cloud.md)、[在 Azure 虛擬機器上開始使用 SQL Server](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/)、[Azure SQL Database](https://azure.microsoft.com/en-us/services/sql-database/) 以及[在 Azure 中選取 SQL Server 選項](https://azure.microsoft.com/documentation/articles/data-management-azure-sql-database-and-sql-server-iaas/)。  
  
##  <a name="UpgradeInPlace"></a> 就地升級  
 透過此方法，SQL Server 安裝程式會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 位元取代現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 位元，然後升級每個系統及使用者資料庫，藉此升級現有的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝。  就地升級方法最簡易，其需要停機一段時間，需要後援時也會花費較長時間，而且未受所有案例支援。 如需支援與未支援的就地升級案例詳細資訊，請參閱[支援的版本與版本升級](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)。  
  
 此方法通常用在下列案例中：  
  
-   沒有高可用性 (HA) 組態的開發環境。  
  
-   可容許停機時間，並執行於最新硬體及軟體的非任務關鍵性生產環境。 停機時間取決於您的資料庫大小，以及 I/O 子系統的速度。 在記憶體最佳化資料表使用中時升級 SQL Server 2014 將會花費額外時間。 如需詳細資訊，請參閱 [Plan and Test the Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)。  
  
> [!WARNING]  
>  執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體會因為執行升級前檢查而停止並重新啟動。  
  
> [!CAUTION]  
>  當您升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，會覆寫先前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，所以它不再存在於電腦上。 升級之前，請備份 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫以及與先前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體相關聯的其他物件。  
  
 下圖提供 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 就地升級必要步驟的整體概觀。  
  
 ![Database Engine Upgrade Non-HA In-Place Upgrade](../../database-engine/install-windows/media/database-engine-upgrade-non-ha-in-place-upgrade.png "Database Engine Upgrade Non-HA In-Place Upgrade")  
  
 如需詳細步驟，請參閱[使用安裝精靈升級為 SQL Server 2016 &#40;Setup&#41;](../../database-engine/install-windows/upgrade-to-sql-server-2016-using-the-installation-wizard-setup.md)。  
  
##  <a name="NewInstallationUpgrade"></a> 遷移到新的安裝  
 透過此方法，您可以在建置新 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 環境的同時保有目前環境，前者通常在新的硬體上，並使用新版作業系統。 在新環境中安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 後，您可以執行幾個步驟讓新環境就緒，以便將現有使用者資料庫從現有環境遷移到新環境，並盡可能縮短停機時間。 這些步驟包括遷移下列項目：  
  
-   **系統物件：**某些應用程式相依於超出單一使用者資料庫範圍的資訊、實體和/或物件。 一般而言，應用程式相依於 master 和 msdb 資料庫以及使用者資料庫。 如果有資料庫正確運作所需的任何項目儲存在使用者資料庫外部，則必須設法讓目的地伺服器執行個體也能提供。 例如，應用程式的登入在 master 資料庫中儲存為中繼資料，就必須在目的地伺服器上加以重新建立。 若應用程式或資料庫維護計畫相依於 SQL Server Agent 作業，而其中繼資料儲存於 msdb 資料庫，則必須在目的地伺服器執行個體上重新建立那些作業。 伺服器層級觸發程序的中繼資料也同樣儲存在 master 中。  
    當您將應用程式的資料庫移動到其他伺服器執行個體時，您必須在目的地伺服器執行個體上重新建立 master 和 msdb 中相依實體及物件的所有中繼資料。 例如，如果資料庫應用程式使用伺服器層級觸發程序，僅在新系統上附加或還原資料庫是不夠的。 除非您以手動方式為 master 資料庫中的那些觸發程序重新建立中繼資料，否則資料庫無法如預期一般運作。 如需詳細資訊，請參閱[在另一個伺服器執行個體上提供可用的資料庫時，管理中繼資料 &#40;SQL Server&#41;](../../relational-databases/databases/manage metadata when making a database available on another server.md)。  
  
-   **儲存於 MSDB 的 Integration Services 封裝：** 若您將封裝儲存在 MSDB 中，就必須使用 [dtutil Utility](../../integration-services/dtutil-utility.md) 編寫那些封裝的指令碼，或將其重新佈署到新的伺服器。 您必須先將封裝升級成 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，然後才能在新的伺服器上使用封裝。 如需詳細資訊，請參閱 [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md)。  
  
-   **Reporting Services 加密金鑰：**在報表伺服器組態中，建立用於加密機密資訊的對稱金鑰備份副本是很重要的一部分。 許多例行作業都需要金鑰的備份副本，這備份副本可以讓您在新安裝中重複使用現有的報表伺服器資料庫。 如需詳細資訊，請參閱[備份與還原 Reporting Services 加密金鑰](../../reporting-services/install-windows/back-up-and-restore-reporting-services-encryption-keys.md)以及[升級和移轉 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)。  
  
 一旦新的   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 環境擁有與現有環境相同的系統物件，您就可以將使用者資料庫從現有系統遷移到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體，在某種程度上將現有系統的停機時間減到最少。 您可以使用備份與還原完成資料庫遷移，若您處於 SAN 環境中，也可以藉由重新指出 LUN 來完成。 下圖描述這兩種方法的步驟。  
  
> [!CAUTION]  
>  停機時間取決於您的資料庫大小，以及 I/O 子系統的速度。 在記憶體最佳化資料表使用中時升級 SQL Server 2014 將會花費額外時間。 如需詳細資訊，請參閱 [Plan and Test the Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)。  
  
 在遷移使用者資料庫後，您可以使用多種方法其中之一 (例如將伺服器重新命名、使用 DNS 項目、修改連接字串) 向新使用者指出新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  與就地升級相較之下，新的安裝方法可減少風險及停機時間，並有助於硬體及作業系統升級與 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的更新同時進行。  
  
> [!NOTE]  
>  若您已經就地擁有高可用性 (HA) 解決方案或其他多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體環境，請前往[輪流升級](#RollingUpgrade)。 若您未就地擁有高可用性解決方案，則可以考慮暫時設定[資料庫鏡像](http://msdn.microsoft.com/library/ms190941.aspx)進一步縮短停機時間以加速升級，或利用此機會設定 [AlwaysOn 可用性群組](http://msdn.microsoft.com/library/hh510260.aspx)當作永久 HA 解決方案。  
  
 例如，您可以使用此方法來升級：  
  
-   不支援之作業系統上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝。  
  
-   在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不支援 x86 安裝時的 SQL Server x86 安裝。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 新硬體和/或新版作業程式。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不支援將 SQL Server 2005 就地升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時的 SQL Server 2005。 如需詳細資訊，請參閱 [Are you upgrading from SQL Server 2005?](../../database-engine/install-windows/are-you-upgrading-from-sql-server-2005.md)。  
  
 新安裝升級的必要步驟會依據您使用連接儲存體還是 SAN 儲存體而有些微不同。  
  
-   **連接儲存體環境：** 若您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境使用連接儲存體，下圖及圖中連結會引導您完成 [!INCLUDE[ssDE](../../includes/ssde-md.md)]新安裝升級的必要步驟。  
  
     ![New installation upgrade method using backup and restore for attached storage](../../database-engine/install-windows/media/new-installation-upgrade-method-using-backup-and-restore-for-attached-storage.png "New installation upgrade method using backup and restore for attached storage")  
  
-   **SAN 儲存體環境：**  若您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境使用 SAN 儲存體，下圖及圖中連結會引導您完成 [!INCLUDE[ssDE](../../includes/ssde-md.md)]新安裝升級的必要步驟。  
  
     ![New installation upgrade method using detach and attach for SAN storage](../../database-engine/install-windows/media/new-installation-upgrade-method-using-detach-and-attach-for-san-storage.png "New installation upgrade method using detach and attach for SAN storage")  
  
##  <a name="RollingUpgrade"></a> 輪流升級  
 當 SQL Server 解決方案環境涉及必須以特定順序升級的多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，便需要輪流升級，盡可能增加執行時間、減少風險並保留功能。 輪流升級基本上是有特定順序的多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的升級，會在現有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體執行就地升級，或執行新的安裝升級，加速升級專案中硬體和/或作業系統的升級。 在許多案例中，您都需要使用輪流升級方法。 這些案例記載於以下主題中：  
  
-   Always-On 可用性群組：如需在此環境中執行輪流升級的詳細步驟，請參閱[升級 AlwaysOn 可用性群組複本執行個體](../../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)。  
  
-   容錯移轉叢集執行個體：如需在此環境中執行輪流升級的詳細步驟，請參閱[升級 SQL Server 容錯移轉叢集執行個體](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md) 。  
  
-   鏡像執行個體：如需在此環境中執行輪流升級的詳細步驟，請參閱[升級鏡像執行個體](../../database-engine/database-mirroring/upgrading-mirrored-instances.md)。  
  
-   記錄傳送執行個體：如需在此環境中執行輪流升級的詳細步驟，請參閱[將記錄傳送升級至 SQL Server 2016 &#40;Transact-SQL&#41;](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)。  
  
-   複寫環境：如需在此環境中執行輪流升級的詳細步驟，請參閱 [Upgrade Replicated Databases](../../database-engine/install-windows/upgrade-replicated-databases.md)。  
  
-   SQL Server Reporting Services 向外延展環境：如需在此環境中執行輪流升級的詳細步驟，請參閱[升級和移轉 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)。  
  
## 這篇文章對您有幫助嗎？ 我們會持續聽取您的意見  
 您要尋找哪些資訊？找到了嗎？ 我們會持續聽取您的意見來改進內容。 請將您的意見提交到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Choose%20a%20Database%20Engine%20Upgrade%20Method%20page)  
  
## 另請參閱  
 [計劃和測試資料庫引擎升級計劃](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)   
 [完成資料庫引擎升級](../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
  