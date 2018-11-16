---
title: 教學課程：準備 SQL Server 進行複寫 (發行者、散發者、訂閱者) | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: quickstart
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 39eac1be5a9e6479a7607364bb194b5aa5b8716f
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51672587"
---
# <a name="tutorial-prepare-sql-server-for-replication-publisher-distributor-subscriber"></a>教學課程：準備 SQL Server 進行複寫 (發行者、散發者、訂閱者)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在設定複寫拓撲之前，規劃安全性是很重要的步驟。 本教學課程說明如何更妥善地保護複寫拓撲。 同時說明如何設定散發，這是複寫資料的第一步。 您必須完成此教學課程，才能進行任何其他教學課程。  
  
> [!NOTE]  
> 若要在伺服器之間安全地複寫資料，必須實作[複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)中的所有建議。  
  
## <a name="what-you-will-learn"></a>學習內容  
此教學課程會教導您如何準備伺服器，以便在最低權限下安全地執行複寫。  

在本教學課程中，您將學會如何：
> [!div class="checklist"]
> * 建立用於複寫的 Windows 帳戶。
> * 準備快照集資料夾。
> * 設定散發。

## <a name="prerequisites"></a>Prerequisites
本教學課程是特別提供給熟悉基本資料庫作業但只稍微涉獵複寫作業的使用者。 

若要完成本教學課程，您需要 SQL Server、SQL Server Management Studio (SSMS) 以及 AdventureWorks 資料庫：  
  
- 在發行者伺服器 (來源) 安裝：  
  
   - 任何版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，除了 SQL Server Express 或 SQL Server Compact 以外， 因為這兩種版本無法充任複寫發行者。   
   - [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 範例資料庫。 為了加強安全性，依預設，不會安裝範例資料庫。  
  
- 在訂閱者伺服器 (目的地) 安裝任何版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，除了 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 以外， 因為 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 無法在異動複寫中充任訂閱者。  
  
- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases)。 有關在 SSMS 中還原資料庫的指示，請參閱[還原資料庫](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。 
    
>[!NOTE]
> - 相差兩個版本以上的 SQL Server 執行個體不支援複寫。 如需詳細資訊，請參閱 [Supported SQL Server Versions in Replication Topology](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/) (複寫拓撲中支援的 SQL Server 版本)。
> - 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，您用來與發行者和訂閱者連線的登入資料，必須是**系統管理員**固定伺服器角色的一員。 如需此角色的詳細資訊，請參閱[伺服器層級角色](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/server-level-roles)。  


**完成本教學課程的估計時間：30 分鐘**
  
## <a name="create-windows-accounts-for-replication"></a>建立用於複寫的 Windows 帳戶
在這一節中，您會建立 Windows 帳戶，以執行複寫代理程式。 您會在本機伺服器上，另外為下列代理程式建立 Windows 帳戶：  
  
|Agent|位置|帳戶名稱|  
|---------|------------|----------------|  
|快照集代理程式|發行者|<*電腦名稱*>\repl_snapshot|  
|記錄讀取器代理程式|發行者|<*電腦名稱*>\repl_logreader|  
|散發代理程式|發行者和訂閱者|<*電腦名稱*>\repl_distribution|  
|[合併代理程式]|發行者和訂閱者|<*電腦名稱*>\repl_merge|  
  
> [!NOTE]  
> 在複寫教學課程中，發行者和散發者會共用相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 (NODE1\SQL2016)。 訂閱者執行個體 (NODE2\SQL2016) 為遠端物件。 發行者和訂閱者可以共用相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，但這不是必要條件。 如果發行者和訂閱者共用相同的執行個體，則可略過在訂閱者上建立帳戶的步驟。  

### <a name="create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>在發行者端建立複寫代理程式的本機 Windows 帳戶
  
1. 在發行者端，從 [控制台] 中的 [系統管理工具] 開啟 [電腦管理]。  
  
2. 在 [系統工具] 中，展開 [本機使用者和群組]。  
  
3. 以滑鼠右鍵按一下 [使用者]，然後選取 [新增使用者]。  
     
4. 在 [使用者名稱] 方塊中輸入 **repl_snapshot**，並提供密碼和其他相關資訊，然後選取 [建立]，以建立 repl_snapshot 帳戶： 

   ![[新增使用者] 對話方塊](media/tutorial-preparing-the-server-for-replication/newuser.png)
  
5. 重複執行先前的步驟，以建立 repl_logreader、repl_distribution 和 repl_merge 帳戶：  
 
   ![複寫使用者清單](media/tutorial-preparing-the-server-for-replication/replusers.png)
  
6. 選取 [關閉]。  
  
### <a name="create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>在訂閱者端建立複寫代理程式的本機 Windows 帳戶  
  
1. 在訂閱者端，從 [控制台] 中的 [系統管理工具] 開啟 [電腦管理]。  
  
2. 在 [系統工具] 中，展開 [本機使用者和群組]。  
  
3. 以滑鼠右鍵按一下 [使用者]，然後選取 [新增使用者]。  
  
4. 在 [使用者名稱] 方塊中輸入 **repl_distribution**，並提供密碼和其他相關資訊，然後選取 [建立]，以建立 repl_distribution 帳戶。  
  
5. 重複執行先前的步驟，以建立 repl_merge 帳戶。  
  
6. 選取 [關閉]。  

如需詳細資訊，請參閱[複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)。  

## <a name="prepare-the-snapshot-folder"></a>準備快照集資料夾
在這一節中，您會設定用於建立及儲存發行集快照集的快照集資料夾。 

### <a name="create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>建立快照集資料夾的共用並指定權限  
  
1. 在檔案總管中，瀏覽至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料夾。 預設位置是 C:\Program Files\Microsoft SQL Server\MSSQL.X\MSSQL\Data。  
  
2. 建立名為 **repldata**的新資料夾。  
  
3. 以滑鼠右鍵按一下此資料夾，然後選取 [屬性]。  
  
   A. 在 [repldata Properties] \(複寫資料內容) 對話方塊的 [共用] 索引標籤上，選取 [進階共用]。  
  
   B. 在 [進階共用] 對話方塊中，選取 [Share this Folder] \(共用此資料夾\)，然後選取 [權限]。  

   ![共用 repldata 資料夾的選項](media/tutorial-preparing-the-server-for-replication/repldata.png)

6. 在 [Permissions for repldata] \(複寫資料權限) 對話方塊中選取 [新增]。 在 [Select User, Computers, Service Account, or Groups] \(選取使用者、電腦、服務帳戶或群組\) 方塊中，以 <發行者電腦名稱>**\repl_snapshot** 形式鍵入之前建立的快照集代理程式帳戶名稱。 選取 [檢查名稱]，然後選取 [確定]。  

   ![新增共用權限的選項](media/tutorial-preparing-the-server-for-replication/addshareperms.png)

7. 重複步驟 6，新增其他兩個之前已建立的帳戶：<發行者電腦名稱>**\repl_merge** 和 <發行者電腦名稱>**\repl_distribution**。

8. 新增三個帳戶之後，指派下列權限：      
   - repl_distribution：**讀取**  
   - repl_merge：**讀取**  
   - repl_snapshot：**完整控制**    

   ![每個帳戶的共用權限](media/tutorial-preparing-the-server-for-replication/sharedpermissions.png)

9. 正確設定共用權限之後，選取 [確定] 關閉 [Permissions for repldata] \(複寫資料權限\) 對話方塊。 選取 [確定] 關閉 [進階設定] 對話方塊。 

10. 在 [repldata Properties] \(複寫資料內容\) 對話方塊中，依序選取 [安全性] 索引標籤和 [編輯]：  

    ![[安全性] 索引標籤上的 [編輯] 按鈕](media/tutorial-preparing-the-server-for-replication/editsecurity.png)   

11. 在 [Permissions for repldata] \(複寫資料權限) 對話方塊中選取 [新增]。 在 [Select Users, Computers, Service Accounts, or Groups] \(選取使用者、電腦、服務帳戶或群組\) 方塊中，以 <發行者電腦名稱>**\repl_snapshot** 形式鍵入之前建立的快照集代理程式帳戶名稱。 選取 [檢查名稱]，然後選取 [確定]。  

    ![新增安全性權限的選項](media/tutorial-preparing-the-server-for-replication/addsecuritypermissions.png)

  
12. 重複上一個步驟，為散發代理程式 (例如 <發行者電腦名稱>**\repl_distribution**) 及合併代理程式 (例如 <發行者電腦名稱>**\repl_merge**) 新增權限。  
    
  
13. 確認允許下列權限：  
  
    - repl_distribution：**讀取**
    - repl_merge：**讀取**
    - repl_snapshot：**完整控制**   
 
    ![複寫資料的使用者權限](media/tutorial-preparing-the-server-for-replication/replpermissions.png) 

14. 再次選取 [共用] 索引標籤，並記下共用的**網路路徑**。 當您稍後設定快照集資料夾時，會需要此路徑。  

    ![[共用] 索引標籤上的網路路徑](media/tutorial-replicating-data-between-continuously-connected-servers/networkpath.png)

15. 選取 [確定] 關閉 [repldata Properties] \(複寫資料內容) 對話方塊。 
 
如需詳細資訊，請參閱[保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  

## <a name="configure-distribution"></a>設定散發
在這一節中，您會在發行者端設定散發，並在發行集和散發資料庫上設定所需權限。 如果您已經設定散發者，則必須停用發行和散發，再開始進行本節。 如果您必須保留現有的複寫拓撲，請勿執行上述動作，特別是在生產環境中。   
  
利用遠端散發者來設定發行者已超出本教學課程的範圍。  

### <a name="configure-distribution-at-the-publisher"></a>在發行者端設定散發  
  
1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者，然後展開伺服器節點。  
  
2. 以滑鼠右鍵按一下 [複寫] 資料夾，然後選取 [設定散發]：  

   ![捷徑功能表上的 [設定散發] 命令](media/tutorial-preparing-the-server-for-replication/configuredistribution.png)
  
   > [!NOTE]  
   > 如果您使用 **localhost** 而非實際伺服器名稱連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，系統會以警告提示您 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法連線到 **localhost**。 在警告對話方塊中選取 [確定]。 在 [連線到伺服器] 對話方塊中，將 [伺服器名稱] 從 **localhost** 變更為伺服器的名稱。 然後選取 [連線]。  
  
   [散發設定精靈] 會隨即啟動。  
  
3. 在 [散發者] 頁面上，選取 [<'伺服器名稱'> 將扮演本身的散發者; SQL Server 將建立散發資料庫和記錄]。 然後選取 [下一步]。  

   ![讓伺服器扮演自身散發者的選項](media/tutorial-preparing-the-server-for-replication/serverdistributor.png)
  
4. 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式未執行，請在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 啟動] 頁面上選取 [是，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務設定為自動啟動]。 選取 **[下一步]**。  

     
5. 在 [快照集資料夾] 方塊中輸入路徑 \\\\<發行者電腦名稱>**\repldata**，然後選取 [下一步]。 這個路徑應該符合您之前在設定共用內容之後，在複寫資料內容資料夾下的 [網路路徑] 中所見。 

   ![[repldata Properties] \(複寫資料內容\) 對話方塊與 [設定散發精靈] 中網路路徑的比較](media/tutorial-preparing-the-server-for-replication/repldatasnapshot.png)
  
6. 接受精靈其餘頁面上的預設值。  
    
   ![精靈的最後一頁](media/tutorial-preparing-the-server-for-replication/distributionwizarddefaults.png)
  
7. 選取 [完成]，以啟用散發。 

設定散發者時，您可能會看到下列錯誤。 它指出啟動 SQL Server Agent 帳戶所用的帳戶不是系統管理員。 您需要手動啟動 SQL Server Agent，將這些權限授與現有的帳戶，或修改 SQL Server Agent 要使用的帳戶。 

![設定 SQL Server Agent 的錯誤訊息](media/tutorial-preparing-the-server-for-replication/startingagenterror.png)

如果您的 SQL Server Management Studio 執行個體是以系統管理權限執行，您就可以從 SSMS 手動啟動 SQL Agent：  
    
![針對 SSMS 中的代理程式選取捷徑功能表上的 [啟動]](media/tutorial-preparing-the-server-for-replication/ssmsstartagent.png) 

>[!NOTE]
> 如果沒看到 SQL Agent 啟動，請在 SSMS 中以滑鼠右鍵按一下 SQL Server Agent，然後選取 [重新整理]。 如果它仍處於停止狀態，請從 SQL Server 組態管理員以手動方式啟動它。    
  
### <a name="set-database-permissions-at-the-publisher"></a>在發行者端設定資料庫權限  
  
1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中展開 [安全性]，並以滑鼠右鍵按一下 [登入]，然後選取 [新增登入]：  

   ![捷徑功能表上的 [新增登入] 命令](media/tutorial-preparing-the-server-for-replication/newlogin.png)
  
2. 在 [一般] 頁面中選取 [搜尋]。 在 [輸入物件名稱來選取] 方塊中輸入 <發行者電腦名稱>**\repl_snapshot**，選取 [檢查名稱]，然後選取 [確定]。  

   ![輸入物件名稱的選項](media/tutorial-preparing-the-server-for-replication/addsnapshotlogin.png)
  
3. 在 [使用者對應] 頁面上，從 [已對應到此登入的使用者] 清單中選取 **distribution** 和 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 這兩個資料庫。  
  
   在 [資料庫角色成員資格] 清單中，選取 [db_owner] 角色以登入這兩個資料庫。  

   ![選取資料庫及其角色](media/tutorial-preparing-the-server-for-replication/dbowner.png)
  
4. 選取 [確定] 建立登入。  
  
5. 重複步驟 1-4 來建立其他本機帳戶 (repl_distribution、repl_logreader 和 repl_merge) 的登入。 這些登入也必須對應至 **distribution** 和 **AdventureWorks** 資料庫中 **db_owner** 固定資料角色成員的使用者。  

   ![檢視 [物件總管] 中的所有四個帳戶](media/tutorial-preparing-the-server-for-replication/usersinssms.png)
  
  
如需詳細資訊，請參閱：
- [設定散發](../../relational-databases/replication/configure-distribution.md) 
- [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)  

## <a name="next-steps"></a>後續步驟
您的伺服器現已就緒可順利進行複寫。 下一篇文章會教導您如何設定異動複寫： 

> [!div class="nextstepaction"]
> [教學課程：設定兩個完全連線的伺服器之間的複寫 (異動)](tutorial-replicating-data-between-continuously-connected-servers.md)

  
  
