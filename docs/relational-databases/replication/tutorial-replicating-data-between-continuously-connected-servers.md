---
title: 教學課程：設定兩個完全連線的伺服器之間的複寫 (異動) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorials [SQL Server replication]
- replication [SQL Server], tutorials
- wizards [SQL Server replication]
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fcb6a4d0468dc74bbc937a11fd60783897e402cf
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38047336"
---
# <a name="tutorial-configure-replication-between-two-fully-connected-servers-transactional"></a>教學課程：設定兩個完全連線的伺服器之間的複寫 (異動)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
異動複寫是處理持續連線伺服器之間移動資料問題的良好解決方案。 您可以使用 [複寫精靈]，輕鬆設定及管理複寫拓撲。 

本教學課程會為您示範，如何為持續連線的伺服器設定異動複寫拓撲。 如需異動複寫如何運作的詳細資訊，請參閱[異動複寫概觀](https://docs.microsoft.com/en-us/sql/relational-databases/replication/transactional/transactional-replication)。 
  
## <a name="what-you-will-learn"></a>學習內容  
本教學課程會教您如何使用異動複寫，從一個資料庫將資料發行到另一個資料庫。 

在本教學課程中，您將學會如何：
> [!div class="checklist"]
> * 透過異動複寫建立發行者。
> * 為交易式發行者建立訂閱者。
> * 驗證訂閱及測量延遲。
  
  
## <a name="prerequisites"></a>Prerequisites  
本教學課程適合熟悉基本資料庫作業，但對複寫經驗有限的使用者。 開始進行本教學課程之前，您必須先完成[教學課程：準備 SQL Server 進行複寫](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)。  
  
若要完成本教學課程，您需要 SQL Server、SQL Server Management Studio (SSMS) 以及 AdventureWorks 資料庫：  
  
- 在發行者伺服器 (來源) 安裝：  
  
   - 任何版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，除了 SQL Server Express 或 SQL Server Compact 以外， 因為這兩種版本無法充任複寫發行者。   
   - [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 範例資料庫。 為了加強安全性，依預設，不會安裝範例資料庫。  
  
- 在訂閱者伺服器 (目的地) 安裝任何版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，除了 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 以外， 因為 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 無法在異動複寫中充任訂閱者。  
  
- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases)。 有關在 SSMS 中還原資料庫的指示，請參閱[還原資料庫](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。 
 
>[!NOTE]
> - 相差兩個版本以上的 SQL Server 執行個體不支援複寫。 如需詳細資訊，請參閱 [Supported SQL Server Versions in Replication Topology](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/) (複寫拓撲中支援的 SQL Server 版本)。
> - 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，您用來與發行者和訂閱者連線的登入資料，必須是**系統管理員**固定伺服器角色的一員。 如需此角色的詳細資訊，請參閱[伺服器層級角色](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles)。  
  
  
**完成本教學課程的估計時間：60 分鐘**  
  
## <a name="configure-the-publisher-for-transactional-replication"></a>為異動複寫設定發行者
在本節中，您會使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 建立交易式發行集，以發行 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫中 **Product** 資料表的篩選子集。 此外，您也會將散發代理程式所使用的 SQL Server 登入新增至發行集存取清單 (PAL)。


### <a name="create-a-publication-and-define-articles"></a>建立發行集並定義發行項
1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者，然後展開伺服器節點。  
  
2. 以滑鼠右鍵按一下 [SQL Server Agent]，然後選取 [啟動]。 在建立發行集之前，您應該先執行 SQL Server Agent。 如果這樣無法啟動代理程式，您必須從 SQL Server 組態管理員以手動方式加以啟動。 
3. 展開 [複寫] 資料夾，然後以滑鼠右鍵按一下 [本機發行集] 資料夾，再選取 [新增發行集]。 此步驟會啟動新的發行集精靈：  

   ![啟動 [新增發行集精靈] 的選取範圍](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
  
3. 在 [發行集資料庫] 頁面上，選取 [[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]]，然後選取 [下一步]。  
  
4. 在 [發行集類型] 頁面上，選取 [交易式發行集]，然後選取 [下一步]：  

   ![已選取發行集類型的「發行集類型」頁面](media/tutorial-replicating-data-between-continuously-connected-servers/tranrepl.png)
  
5. 在 [發行項] 頁面中展開 [資料表] 節點，選取 [產品] 核取方塊。 然後展開 [產品] 並清除 [ListPrice] 和 [StandardCost] 旁的核取方塊。 選取 **[下一步]**。  

   ![「發行項」頁面，已選取要發行的發行項](media/tutorial-replicating-data-between-continuously-connected-servers/replarticles.png)
  
6. 在 [Filter Table Rows] \(篩選資料表資料列) 頁面上，選取 [新增]。   
  
7. 在 [新增篩選] 對話方塊中，選取 **SafetyStockLevel** 資料行。 選取向右箭號，將資料行新增至篩選查詢的篩選陳述式 WHERE 子句。 然後在 WHERE 子句修飾詞中手動鍵入以下內容：  
  
   ```sql  
   WHERE [SafetyStockLevel] < 500  
   ```
  
   ![「篩選資料表流程」頁面與「新增篩選」對話方塊](media/tutorial-replicating-data-between-continuously-connected-servers/filter.png)
  
8. 依序選取 [確定] 和 [下一步]。  
  
9. 選取 [立即建立快照集，並保留快照集為可使用狀態，以初始化訂閱] 核取方塊，然後選取 [下一步]：  

   ![已選取核取方塊的「快照集代理程式」頁面](media/tutorial-replicating-data-between-continuously-connected-servers/snapshot.png)
  
10. 在 [代理程式安全性] 頁面上，清除 [Use the security settings from the Snapshot Agent] \(使用快照集代理程式的安全性設定\) 核取方塊。   
  
    選取快照集代理程式的 [安全性設定]。 在 [Process account] \(處理帳戶\) 方塊中輸入 <*Publisher_Machine_Name*>**\repl_snapshot**，提供此帳戶的密碼並選取 [確定]。  

    ![「代理程式安全性」頁面與「快照集代理程式安全性」對話方塊](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagentsecurity.png)
  
12. 重複執行先前的步驟，將 <*Publisher_Machine_Name*>**\repl_logreader** 設定為記錄讀取器代理程式的處理帳戶。 然後選取 [確定]。  

    ![「記錄讀取器代理程式」對話方塊與「代理程式安全性」頁面](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentsecurity.png)   

  
13. 在 [完成精靈] 頁面的 [發行集名稱] 方塊中鍵入 **AdvWorksProductTrans**，然後選取 [完成]：  

    ![[完成精靈] 頁面與發行集名稱](media/tutorial-replicating-data-between-continuously-connected-servers/advworksproducttrans.png)
  
14. 建立發行集之後，選取 [關閉] 以完成精靈。 

若您在嘗試建立發行集時 SQL Server Agent 未處於執行中狀態，則可能會遇到下列錯誤。 此錯誤表示您的發行集已成功建立，但快照集代理程式無法啟動。 如果發生這種情況，您需要啟動 SQL Server Agent，然後手動啟動快照集代理程式。 下一節會提供指示。 

![快照集代理程式無法啟動的警告](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenterror.png)
    
  
### <a name="view-the-status-of-snapshot-generation"></a>檢視快照集產生的狀態  
  
1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者，展開伺服器節點，然後展開 [複寫] 資料夾。  
  
2. 在 [本機發行集] 資料夾中，以滑鼠右鍵按一下 [AdvWorksProductTrans]，然後選取 [檢視快照集代理程式狀態]：  
   ![快顯功能表上用於檢視快照集代理程式狀態的命令](media/tutorial-replicating-data-between-continuously-connected-servers/viewsnapshot.png)
  
3. 發行集快照集代理程式作業的目前狀態會隨即顯示。 確認快照集作業已成功，再繼續進行下一節。
          
若您在建立發行集時 SQL Server Agent 未處於執行中狀態，則當您查看發行集快照集代理程式狀態時，會看到快照集代理程式從未執行。 如果是這種情況，請選取 [啟動] 來啟動快照集代理程式： 

![[啟動] 按鈕，以及狀態訊息中表示快照集代理程式有執行的狀態訊息](media/tutorial-replicating-data-between-continuously-connected-servers/startsnapshotagent.png)
     
若您在此處看到錯誤，請參閱[針對快照集代理程式錯誤進行疑難排解](troubleshoot-tran-repl-errors.md#find-errors-with-the-snapshot-agent)。


  
### <a name="add-the-distribution-agent-login-to-the-pal"></a>將散發代理程式新增至 PAL  
  
1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者，展開伺服器節點，然後展開 [複寫] 資料夾。  
  
2. 在 [本機發行集] 資料夾中，以滑鼠右鍵按一下 [AdvWorksProductTrans]，然後選取 [屬性]。  [發行集屬性] 對話方塊會隨即顯示。    
  
   A. 選取 [發行集存取清單] 頁面，然後選取 [新增]。  
   B. 在 [新增發行集存取] 對話方塊中，選取 <*Publisher_Machine_Name*>**\repl_distribution**，然後選取 [確定]。
   
   ![將登入新增至發行集存取清單的選取範圍](media/tutorial-replicating-data-between-continuously-connected-servers/tranreplproperties.png)

如需詳細資訊，請參閱[複寫程式設計概念](../../relational-databases/replication/concepts/replication-programming-concepts.md)。  
  

## <a name="create-a-subscription-to-the-transactional-publication"></a>建立交易式發行集的訂閱
在本節中，您會將訂閱者新增至先前建立的發行集。 本教學課程使用了遠端訂閱者 (NODE2\SQL2016)，但您也可在本機將訂閱新增至發行者。 

### <a name="create-the-subscription"></a>建立訂閱  
  
1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者，展開伺服器節點，然後展開 [複寫] 資料夾。  
  
2. 在 [本機發行集] 資料夾中，以滑鼠右鍵按一下 **AdvWorksProductTrans** 發行集，然後選取 [新增訂閱]。 [新增訂閱精靈] 會隨即啟動： 
 
   ![啟動 [新增訂閱精靈] 的選取範圍](media/tutorial-replicating-data-between-continuously-connected-servers/newsub.png)     
  
3. 在 [發行集] 頁面上，選取 [AdvWorksProductTrans]，然後選取 [下一步]：  

   ![已選取發行集的「發行集」頁面](media/tutorial-replicating-data-between-continuously-connected-servers/selectpub.png)
  
4. 在 [散發代理程式位置] 頁面上，選取 [Run all agents at the Distributor] \(在散發者端執行所有代理程式\)，然後選取 [下一步]。  如須提取和推送訂閱的詳細資訊，請參閱[訂閱發行集](https://docs.microsoft.com/en-us/sql/relational-databases/replication/subscribe-to-publications)。

   ![「散發代理程式位置」頁面，以及選為在散發者端執行所有代理程式的選項](media/tutorial-replicating-data-between-continuously-connected-servers/runagentsatdist.png)
  
5. 在 [訂閱者] 頁面上，如未顯示訂閱者執行個體的名稱，請選取 [新增訂閱者]，然後從下拉式清單選取 [新增 SQL Server 訂閱者]。 此步驟會開啟 [連線至伺服器] 對話方塊。 輸入訂閱者執行個體的名稱，然後選取 [連線]。  
    
   在新增訂閱者後，選取您訂閱者執行個體名稱旁的核取方塊。 然後在 [訂閱資料庫] 下選取 [新增資料庫]。   

   ![具有新增訂閱者伺服器之選取項目的「訂閱者」頁面](media/tutorial-replicating-data-between-continuously-connected-servers/addsub.png)

7. [新增資料庫] 對話方塊會隨即開啟。 在 [資料庫名稱] 方塊中輸入 **ProductReplica**，依序選取 [確定] 和 [下一步]： 
  
   ![輸入訂閱資料庫的名稱](media/tutorial-replicating-data-between-continuously-connected-servers/productreplica.png)
  
8. 在 [散發代理程式安全性] 頁面上，選取省略符號 (**...**) 按鈕。 在 [Process account] \(處理帳戶) 方塊中輸入 <*Publisher_Machine_Name*>**\repl_distribution**，然後輸入此帳戶的密碼並選取 [確定]，然後選取 [下一步]。

   ![「散發代理程式安全性」對話方塊中的散發帳戶資訊](media/tutorial-replicating-data-between-continuously-connected-servers/adddistaccount.png)
  
9. 選取 [完成] 接受其餘頁面的預設值，並完成精靈。  
  
### <a name="set-database-permissions-at-the-subscriber"></a>在訂閱者端設定資料庫權限  
  
1. 連線至 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的訂閱者。 展開 [安全性] 並以滑鼠右鍵按一下 [登入]，然後選取 [新增登入]。     
  
   A. 在 [一般] 頁面的 [登入名稱] 下，選取 [搜尋] 並新增 <*Subscriber_Machine_Name*>**\repl_distribution** 的登入。

   B. 在 [使用者對應] 頁面上，授與 **ProductReplica** 資料庫的登入 **db_owner**。 

   ![設定訂閱者登入的選取範圍](media/tutorial-replicating-data-between-continuously-connected-servers/loginforsub.png)

2. 選取 [確定] 關閉 [新增登入] 對話方塊。 

  
### <a name="view-the-synchronization-status-of-the-subscription"></a>檢視訂閱的同步處理狀態  
  
1. 連線至 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者。 展開伺服器節點，並展開 [複寫] 資料夾。  
  
2. 在 [本機發行集] 資料夾中，展開 [AdvWorksProductTrans] 發行集，以滑鼠右鍵按一下 **ProductReplica** 資料庫中的訂閱，然後選取 [檢視同步處理狀態]。 目前的訂閱組織狀態會隨即顯示：

   ![開啟 [檢視同步處理狀態] 對話方塊的選取範圍](media/tutorial-replicating-data-between-continuously-connected-servers/viewsyncstatus.png)
3. 若在 [AdvWorksProductTrans] 下看不到訂閱，請選取 F5 鍵重新整理清單。  
  
如需詳細資訊，請參閱：  
- [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
- [建立發送訂閱](../../relational-databases/replication/create-a-push-subscription.md)  
- [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  

## <a name="measure-replication-latency"></a>測量複寫延遲
在本節中，您會使用追蹤 Token 來驗證複寫至訂閱者的變更，並判斷延遲。 延遲是發行者端做的變更出現在訂閱者端所花費的時間。
  
1. 連線至 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者。 展開伺服器節點，再以滑鼠右鍵按一下 [複寫] 資料夾，然後選取 [啟動複寫監視器]：

   ![快顯功能表上的 [啟動複寫監視器] 命令](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)

2. 在左窗格中展開發行者群組，展開發行者執行個體，然後選取 **AdvWorksProductTrans** 發行集。  
  
   A. 選取 [追蹤 Token] 索引標籤。  
   B. 選取 [插入追蹤]。    
   c. 在下列資料行中檢視追蹤 Token 的經過時間： **[發行者到散發者]**、 **[散發者到訂閱者]**、 **[延遲總計]**。 [Pending] \(暫止\) 值表示 Token 尚未到達指定點。

   ![追蹤 Token 的資訊](media/tutorial-replicating-data-between-continuously-connected-servers/tracertoken.png)


如需詳細資訊，請參閱： 
- [針對異動複寫測量延遲及驗證連線](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)
- [尋找具有異動複寫代理程式的錯誤](troubleshoot-tran-repl-errors.md)


## <a name="next-steps"></a>後續步驟
您已成功為您的異動複寫設定發行者和訂閱者。 您現在可以在發行者端的 **Product** 資料表插入、更新或刪除資料。 接著您可以查詢訂閱者端的 **Product** 資料表以檢視複寫的變更。 

下一篇文章會教導您如何設定合併式複寫：  

> [!div class="nextstepaction"]
> [教學課程：設定伺服器和行動用戶端之間的複寫 (合併)](tutorial-replicating-data-with-mobile-clients.md)
