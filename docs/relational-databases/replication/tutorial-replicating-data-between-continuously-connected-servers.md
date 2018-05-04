---
title: 教學課程：設定兩個完全連線的伺服器之間的複寫 (異動) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
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
ms.workload: On Demand
ms.openlocfilehash: de374f4372f62741ff3c49a9433cf339cecf3d26
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-configure-replication-between-two-fully-connected-servers-transactional"></a>教學課程：設定兩個完全連線的伺服器之間的複寫 (異動)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
異動複寫是處理持續連線伺服器之間移動資料問題的良好解決方案。 您可以使用 [複寫精靈]，輕鬆設定及管理複寫拓撲。 本教學課程告訴您，如何為持續連線的伺服器設定異動複寫拓撲。 如需異動複寫如何運作的詳細資訊，請參閱[異動複寫概觀](https://docs.microsoft.com/en-us/sql/relational-databases/replication/transactional/transactional-replication)。 
  
## <a name="what-you-will-learn"></a>學習內容  
本教學課程告訴您如何使用異動複寫，從一個資料庫將資料發行到另一個資料庫。 

在本教學課程中，您將學會如何：
> [!div class="checklist"]
> * 透過異動複寫建立發行者
> * 為交易式發行者建立訂閱者
> * 驗證訂閱及測量延遲
> * 錯誤疑難排解方法
  
  
## <a name="prerequisites"></a>Prerequisites  
本教學課程是特別提供給熟悉基本資料庫作業但對複寫經驗有限的使用者。 本教學課程要求您，先完成上一個教學課程 [準備伺服器進行複寫](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)。  
  
若要使用本教學課程，您的系統必須有 SQL Server Management Studio (SSMS) 和這些元件：  
  
-   在發行者伺服器 (來源)：  
  
    -   任何版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，SQL Server Express 或 SQL Compact 除外。 這兩種版本無法做為複寫發行者。   
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 範例資料庫。 為了加強安全性，依預設，不會安裝範例資料庫。  
  
-   訂閱者伺服器 (目的地)：  
  
    -   任何版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，除了 [!INCLUDE[ssEW](../../includes/ssew-md.md)]以外。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 在異動複寫中不能是訂閱者。  
  
- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases)。 如需在 SSMS 中還原資料庫的指示，請參閱[還原資料庫](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。 
 
>[!NOTE]
> - 不支援版本相差兩個以上的 SQL Server 複寫。 如需詳細資訊，請參閱 [Supported SQL Versions in Repl Topology](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/) (複寫技術支援的 SQL 版本)。
> - 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，您必須使用 **系統管理員 (sysadmin)** 固定伺服器角色成員的登入，連接到發行者和訂閱者。 如需系統管理員角色的詳細資訊，請參閱[伺服器層級角色](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles)。  
  
  
**完成本教學課程的估計時間：60 分鐘。**  
  
## <a name="configure-the-publisher-for-transactional-replication"></a>為異動複寫設定發行者
在本節中，您會使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 建立交易式發行集，以發行 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫中 **Product** 資料表的篩選子集。 此外，您也會將散發代理程式所使用的 SQL Server 登入加入至發行集存取清單 (PAL)。 開始進行此教學課程之前，必須先完成上一個教學課程 [準備伺服器進行複寫](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)。


### <a name="create-a-publication-and-define-articles"></a>建立發行集並定義發行項
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。  
  
2. 以滑鼠右鍵按一下 **SQL Server Agent**，然後選取 [開始]。 在建立發行集之前，您應該先執行 SQL Server Agent。 如果這樣無法啟動代理程式，您必須從 **SQL Server 組態管理員**以手動方式啟動它。 
3. 展開 [複寫] 資料夾，然後以滑鼠右鍵按一下 [本機發行集] 資料夾，再選取 [新增發行集]。  這會啟動 [發行集設定精靈]：  

    ![新增發行集](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
  
3. 在 [發行集資料庫] 頁面上，選取 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，然後選取 [下一步]。  
  
4. 在 [發行集類型] 頁面上，選取 [交易式發行集]，然後選取 [下一步]：  

    ![異動複寫](media/tutorial-replicating-data-between-continuously-connected-servers/tranrepl.png)
  
5. 在 [發行項] 頁面中展開 [資料表] 節點，選取 [產品] 核取方塊。 然後展開 [產品] 並清除 [ListPrice] 和 [StandardCost] 旁的核取方塊。 選取 [下一步]：  

    ![要發行的發行項](media/tutorial-replicating-data-between-continuously-connected-servers/replarticles.png)
  
6. 在 [篩選資料表的資料列] 頁面上，選取 [新增]。   
  
7. 在 [新增篩選] 對話方塊中，選取 [SafetyStockLevel] 資料行，再選取向右鍵將資料行新增至篩選查詢的篩選陳述式 WHERE 子句中。 然後在 WHERE 子句修飾詞中手動鍵入以下內容：  
  
    ```sql  
    WHERE [SafetyStockLevel] < 500  
    ```
  
    ![篩選陳述式](media/tutorial-replicating-data-between-continuously-connected-servers/filter.png)
  
8. 依序選取 [確定] 和 [下一步]。  
  
9. 選取 [立即建立快照集，並保留快照集為可使用狀態，以初始化訂閱] 核取方塊，然後選取 [下一步]：  

    ![快照集代理程式](media/tutorial-replicating-data-between-continuously-connected-servers/snapshot.png)
  
10. 在 [代理程式安全性] 頁面上，清除 [使用快照集代理程式的安全性設定] 核取方塊。   
  
    A. 選取快照集代理程式的 [安全性設定]，在 [處理帳戶] 方塊中輸入 <*發行者電腦名稱>***\repl_snapshot**，提供此帳戶的密碼，然後選取 [確定]：  

    ![快照集代理程式安全性](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagentsecurity.png)
  
12. 重複執行先前的步驟，將 <*發行者電腦名稱*>**\repl_logreader** 設定為記錄讀取器代理程式的處理帳戶，然後選取 [確定]：  

    ![記錄讀取器代理程式安全性](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentsecurity.png)   

  
13. 在 [完成精靈] 頁面的 [發行集名稱] 方塊中鍵入 **AdvWorksProductTrans**，然後選取 [完成]：  

    ![命名發行集](media/tutorial-replicating-data-between-continuously-connected-servers/advworksproducttrans.png)
  
14. 建立發行集之後，選取 [關閉] 以完成精靈。 

    如果在您嘗試建立發行集時您的 SQL Server Agent 未執行，您可能會遇到下列錯誤。 這表示，您的發行集已成功建立，但快照集代理程式無法啟動。 如果發生這種情況，您需要啟動 SQL Server Agent，然後手動啟動快照集代理程式。 下一節會討論有關此作業的指示： 

    ![無法啟動快照集代理程式](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenterror.png)
    
  
### <a name="to-view-the-status-of-snapshot-generation"></a>檢視快照集產生的狀態  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的「發行者」，展開伺服器節點，然後展開 **[複寫]** 資料夾。  
  
2.  在 [本機發行集] 資料夾中，以滑鼠右鍵按一下 [AdvWorksProductTrans]，然後選取 [檢視快照集代理程式狀態]：  

    ![快照集代理程式狀態](media/tutorial-replicating-data-between-continuously-connected-servers/viewsnapshot.png)
  
3.  發行集之快照集代理程式作業的目前狀態隨即顯示。 確認快照集作業已成功，再繼續進行下一節。
          
    如果在您最初建立發行集時，您的 SQL Server Agent 未執行，當您勾選您發行集的 [快照集代理程式狀態] 時，您會看到快照集代理程式「從未執行」。 如果是這種情況，請選取 [啟動] 來啟動快照集代理程式： 

       ![啟動快照集代理程式](media/tutorial-replicating-data-between-continuously-connected-servers/startsnapshotagent.png)
     
       如果在此看到錯誤，請參閱[針對快照集代理程式錯誤進行疑難排解](#troubleshoot-erros-with-snapshot-agent)。 

  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>將散發代理程式登入加入 PAL  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的「發行者」，展開伺服器節點，然後展開 **[複寫]** 資料夾。  
  
2.  在 [本機發行集] 資料夾中，以滑鼠右鍵按一下 [AdvWorksProductTrans]，然後選取 [屬性]。  [發行集屬性] 對話方塊隨即顯示。    
  
    A. 選取 [發行集存取清單] 頁面，然後選取 [新增]。  
    B. 在 [新增發行集存取] 對話方塊中，選取 <*發行者電腦名稱>***\repl_distribution**，然後選取 [確定]。 選取 [確定]：

   
   ![將登入新增至 PAL 清單](media/tutorial-replicating-data-between-continuously-connected-servers/tranreplproperties.png)

**另請參閱**︰  
[複寫程式設計概念](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  

## <a name="create-a-subscription-to-the-transactional-publication"></a>建立交易式發行集的訂閱
在本節中，您要將訂閱者新增至之前建立的發行集。 本教學課程使用遠端訂閱者 (NODE2\SQL2016)，但也可以在本機將訂閱新增至發行者。 

### <a name="to-create-the-subscription"></a>建立訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的「發行者」，展開伺服器節點，然後展開 **[複寫]** 資料夾。  
  
2.  在 [本機發行集] 資料夾中，以滑鼠右鍵按一下 **AdvWorksProductTrans** 發行集，然後選取 [新增訂閱]。  [新增訂閱精靈]隨即啟動： 
 
    ![[新增訂閱]](media/tutorial-replicating-data-between-continuously-connected-servers/newsub.png)     
  
3.  在 [發行集] 頁面上，選取 [AdvWorksProductTrans]，然後選取 [下一步]：  

    ![選取 Tran 發行者](media/tutorial-replicating-data-between-continuously-connected-servers/selectpub.png)
  
4.  在 [散發代理程式位置] 頁面上，選取 [在散發者端執行所有代理程式]，然後選取 [下一步]。  如需提取和推送訂閱的詳細資訊，請參閱[訂閱發行集](https://docs.microsoft.com/en-us/sql/relational-databases/replication/subscribe-to-publications)：

    ![在 Dist 執行代理程式](media/tutorial-replicating-data-between-continuously-connected-servers/runagentsatdist.png)
  
5.  在 [訂閱者] 頁面上，如未顯示訂閱者執行個體的名稱，請選取 [新增訂閱者]，然後從下拉式清單選取 [新增 SQL Server 訂閱者]。 這會啟動 [連線到伺服器] 對話方塊。 輸入訂閱者執行個體的名稱，然後選取 [連線]。  
    
    A. 一旦新增訂閱者，請勾選您訂閱者執行個體名稱旁的方塊。 然後選取 [訂閱資料庫] 下的 [新增資料庫]：   

  ![新增訂閱者伺服器](media/tutorial-replicating-data-between-continuously-connected-servers/addsub.png)

7. 這會啟動 [新增資料庫] 對話方塊。 在 [資料庫名稱] 方塊中輸入 **ProductReplica**，依序選取 [確定] 和 [下一步]： 
  
    ![產品複本資料庫](media/tutorial-replicating-data-between-continuously-connected-servers/productreplica.png)
  
8.  在 [散發代理程式安全性] 對話方塊中選取省略符號 (**…**) 按鈕。 在 [處理帳戶] 方塊中輸入 <*發行者電腦名稱>***\repl_distribution**，再輸入此帳戶的密碼，然後依序選取 [確定] 和 [下一步]：

    ![新增發佈帳戶](media/tutorial-replicating-data-between-continuously-connected-servers/adddistaccount.png)
  
9. 選取 [完成] 接受其餘頁面的預設值，並完成精靈。  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>在訂閱者端設定資料庫權限  
  
1.  連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的訂閱者，展開 [安全性]，並以滑鼠右鍵按一下 [登入]，然後選取 [新增登入]。     
  
    A. 在 [一般] 頁面的 [登入名稱] 下，選取 [搜尋] 並新增 <*訂閱者電腦名稱>***\repl_distribution** 的登入。
    B. 在 [使用者對應] 頁面上，授與 **ProductReplica** 資料庫的登入 **db_owner**： 

    ![訂閱者的登入](media/tutorial-replicating-data-between-continuously-connected-servers/loginforsub.png)

2. 選取 [確定] 關閉 [新增登入] 對話方塊。 

  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>檢視訂閱的同步處理狀態  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的「發行者」，展開伺服器節點，然後展開 **[複寫]** 資料夾。  
  
2.  在 [本機發行集] 資料夾中，展開 [AdvWorksProductTrans] 發行集，以滑鼠右鍵按一下 **ProductReplica** 資料庫中的訂閱，然後選取 [檢視同步處理狀態]。 訂閱的目前訂閱狀態隨即顯示：  
    ![檢視同步處理的狀態](media/tutorial-replicating-data-between-continuously-connected-servers/viewsyncstatus.png)
3.  如果 **[AdvWorksProductTrans]** 之下看不到訂閱，請按 F5 重新整理清單。  
  
**另請參閱**︰  
[使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)  
[訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  

## <a name="measuring-replication-latency"></a>測量複寫延遲
在本節中，您要使用追蹤 Token，確認變更正複寫至訂閱者並決定延遲。 延遲是發行者端做的變更出現在訂閱者端所花費的時間。
  
1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者，展開伺服器節點，再以滑鼠右鍵按一下 [複寫] 資料夾，然後選取 [啟動複寫監視器]：

    ![啟動複寫監視器](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)

2. 在左窗格中展開發行者群組，展開發行者執行個體，然後選取 **AdvWorksProductTrans** 發行集。  
  
    A. 選取 [追蹤 Token] 索引標籤。  
    B. 選取 [插入追蹤]。    
    c. 在下列資料行中檢視追蹤 Token 的經過時間： **[發行者到散發者]**、 **[散發者到訂閱者]**、 **[延遲總計]**。 [暫止] 表示 Token 尚未到達指定點：


   ![追蹤 Token](media/tutorial-replicating-data-between-continuously-connected-servers/tracertoken.png)


**另請參閱**   
[針對異動複寫測量延遲及驗證連接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

## <a name="error-troubleshooting-methodology"></a>錯誤疑難排解方法
本節將教導您如何針對基本的複寫同步處理失敗進行疑難排解。 請注意，本節旨在帶您巡覽複寫元件，目的在進行疑難排解。 不過，您實際遇到的錯誤可能不同於此處討論的內容，而它們可能需要不同的解決方式。 如果發生這種情況，進一步的疑難排解是必要的，但不在本教學課程的範圍內。 


### <a name="troubleshoot-errors-with-snapshot-agent"></a>針對快照集代理程式錯誤進行疑難排解
**快照集代理程式**是產生快照集並將它寫入至指定快照集資料夾的代理程式。 

1. 若要檢視您的快照集代理程式狀態，請展開複寫下的 [本機發行集] 節點，直接選取發行集 [AdvWorksProductTrans] >  [檢視快照集代理程式的狀態]。 
2. 如果 [快照集代理程式狀態] 回報錯誤，您可在**快照集代理程式**的作業歷程記錄中找到更多詳細資料。 若要存取這個對話方塊，請展開 [物件總管] 的 **SQL Server Agent**，然後開啟 [作業活動監視器]。 

    A. 依據**分類**排序，並依分類 ' REPL Snapshot' 找出**快照集代理程式**。 

    B. 以滑鼠右鍵按一下**快照集代理程式**並 [檢視記錄]： 

   ![快照集代理程式記錄](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenthistory.png)
    
1. 在 [快照集代理程式記錄] 中選取相關的記錄項目。 這通常是在回報錯誤項目的「前」一或兩行 (錯誤會以紅色 X 表示)。  檢閱記錄檔下文字方塊中的訊息文字： 

    ![快照集代理程式拒絕存取](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotaccessdenied.png)

        The replication agent had encountered an exception.
        Exception Message: Access to path '\\node1\repldata.....' is denied.


  如果您未正確設定您快照集資料夾的 Windows 權限，您會看到**快照集代理程式**發生「拒絕存取」錯誤。 您需要在您的 repldata 資料夾中驗證 <*發行者電腦名稱>***\repl_snapshot** 帳戶的權限。 如需詳細資訊，請參閱[建立快照集資料夾的共用並指派權限](tutorial-preparing-the-server-for-replication.md#create-a-share-for-the-snapshot-folder-and-assign-permissions)。

### <a name="troubleshoot-errors-with-log-reader-agent"></a>針對記錄讀取器代理程式錯誤進行疑難排解
**記錄讀取器代理程式**會連線到您的發行者資料庫，掃描交易記錄是否有標示為「供複寫」的任何交易。 接著它會將這些交易新增至**散發**資料庫。 

1.  連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者，展開伺服器節點，再以滑鼠右鍵按一下 [複寫] 資料夾，然後選取 [啟動複寫監視器]：  

    ![啟動複寫監視器](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)
  
    複寫監視器隨即啟動：![複寫監視器](media/tutorial-replicating-data-between-continuously-connected-servers/replmonitor.png) 
   
2. 紅色 X 表示發行集未執行同步處理。 展開左側的 [我的發行者]，再展開相關的發行者伺服器。  
  
3.  在左側選取 [AdvWorksProductTrans] 發行集，然後在其中一個索引標籤中尋找紅色 X，找出問題所在。 在本例中，紅色 X 出現在 [代理程式] 索引標籤上，表示其中一個代理程式發生錯誤： 

    ![代理程式錯誤](media/tutorial-replicating-data-between-continuously-connected-servers/agenterror.png)

4. 選取 [代理程式] 索引標籤找出發生錯誤的代理程式： 

    ![記錄讀取器失敗](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentfailure.png)


5. 此檢視會向您顯示兩個代理程式，**快照集代理程式**和**記錄讀取器代理程式**。 發生錯誤的代理程式會有紅色 X。在本例中，**記錄讀取器代理程式**是具有紅色 X 的代理程式，表示它發生了問題。 在報告錯誤的行上按兩下，本例中是**記錄讀取器代理程式**。 這會啟動您已選取之代理程式的**代理程式記錄**，本例中為**記錄讀取器代理程式**記錄。 這會提供有關錯誤的詳細資訊： 
    
    ![記錄讀取器錯誤](media/tutorial-replicating-data-between-continuously-connected-servers/logreadererror.png)

       Status: 0, code: 20011, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.
       The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.
       Status: 0, code: 15517, text: 'Cannot execute as the database principal because the principal "dbo" does not exist, this type of principal cannot be impersonated, or you do not have permission.'.
       Status: 0, code: 22037, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.        

6. 前述錯誤發生的原因通常是因為未正確設定發行者資料庫的擁有者。 這通常是發生在還原資料庫之後。 若要確認這種情況，請展開 [物件總管] 中的 [資料庫] > 以滑鼠右鍵按一下 [AdventureWorks2012] > [屬性]。 確認擁有者位在 [檔案] 頁面之下。 如果此欄位為空白，這可能就是問題的原因： 

    ![資料庫屬性](media/tutorial-replicating-data-between-continuously-connected-servers/dbproperties.png)

7. 如果 [檔案] 頁面上的擁有者為空白，請在 **AdventureWorks2012** 資料庫的內容中開啟 [新增查詢視窗]。 執行下列 T-SQL 程式碼片段︰

    ```sql
    -- set the owner of the database to 'sa' or a specific user account, without the brackets. 
    EXEC sp_changedbowner '<useraccount>'
    -- example for sa: exec sp_changedbowner 'sa'
    -- example for user account: exec sp_changedbowner 'sqlrepro\administrator' 
    ```

8. 您需要重新啟動**記錄讀取器代理程式**。 若要執行此作業，請展開 [物件總管] 的 [SQL Server Agent] 節點，然後開啟**作業活動監視器**。 依據**分類**排序，並依 **'REPL-LogReader'** 分類找出**記錄讀取器代理程式**。 以滑鼠右鍵按一下**記錄讀取器代理程式**和 [從下列步驟啟動作業]： 

    ![重新啟動記錄讀取器代理程式](media/tutorial-replicating-data-between-continuously-connected-servers/startjobatstep.png)

9. 再次開啟**複寫監視器**，以驗證您的發行集現在可否執行同步處理。 如果它尚未開啟，只要以滑鼠右鍵按一下 [物件總管] 中的 [複寫] 即可找到它。 
10. 依序選取 [AdvWorksProductTrans] 發行集和 [代理程式] 索引標籤，再按兩下選取**記錄讀取器代理程式**來開啟代理程式記錄。 您現在應會看到**記錄讀取器代理程式**執行中，且正在複寫命令或其有「無複寫交易」:

    ![記錄讀取器執行中](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderrunning.png)

### <a name="troubleshoot-errors-with-distribution-agent"></a>針對散發代理程式錯誤進行疑難排解
**散發代理程式**採用它在**散發**資料庫中找到的資料，然後將它套用到訂閱者。 

1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者，展開伺服器節點，再以滑鼠右鍵按一下 [複寫] 資料夾，然後選取 [啟動複寫監視器]。  
2. 在**複寫監視器**中選取 [AdvWorksProductTrans] 發行集，然後選取 [所有訂閱] 索引標籤。以滑鼠右鍵按一下 [訂閱] 和 [檢視詳細資料]：

    ![檢視 Dist 詳細資料](media/tutorial-replicating-data-between-continuously-connected-servers/viewdetails.png)

2. [散發者到訂閱者] 記錄對話方塊隨即開啟，並會釐清代理程式發生哪些錯誤： 

     ![Dist 代理程式記錄錯誤](media/tutorial-replicating-data-between-continuously-connected-servers/disthistoryerror.png)
    
        Error messages:
        Agent 'NODE1\SQL2016-AdventureWorks2012-AdvWorksProductTrans-NODE2\SQL2016-7' is retrying after an error. 89 retries attempted. See agent job history in the Jobs folder for more details.

3. 此錯誤指出**散發代理程式**正在重試。 若要尋找詳細資訊，請展開 [物件總管] 中的 [SQL Server Agent] > [作業活動監視器]。 依**分類**排序作業。 

    A. 依分類 **'REPL-Distribution'** 找出**散發代理程式**。 以滑鼠右鍵按一下代理程式並 [檢視記錄]：

    ![檢視 Dist 代理程式記錄](media/tutorial-replicating-data-between-continuously-connected-servers/viewdistagenthistory.png)

5. 選取其中一個錯誤項目，檢視視窗底部的錯誤文字：  

    ![Dist 代理程式的密碼錯誤](media/tutorial-replicating-data-between-continuously-connected-servers/distpwwrong.png)
    
        Message:
        Unable to start execution of step 2 (reason: Error authenticating proxy NODE1\repl_distribution, system error: The user name or password is incorrect.)

6. 這個錯誤指出**散發代理程式**所用的密碼不正確。 若要解決此問題，請展開 [物件總管] 中的 [複寫] 節點，以滑鼠右鍵按一下 [訂閱] > [屬性]。 選取**代理程式處理帳戶**旁的省略符號 (...) 並修改密碼：

    ![修改 Dist 代理程式的密碼](media/tutorial-replicating-data-between-continuously-connected-servers/distagentpwchange.png)

7. 再次檢查您的**複寫監視器**，以滑鼠右鍵按一下 [物件總管] 中的 [複寫] 就可以找到它。 [所有訂閱] 下的紅色 X 指出我們的**散發代理程式**仍有錯誤。 以滑鼠右鍵按一下**複寫監視器** > [檢視詳細資料] 中的 [訂閱]，開啟 [Distribution to Subscriber] \(發佈到訂閱者) 記錄。 現在錯誤變得不一樣了： 

    ![Dist 代理程式無法連線](media/tutorial-replicating-data-between-continuously-connected-servers/distagentcantconnect.png)
           
        Connecting to Subscriber 'NODE2\SQL2016'        
        Agent message code 20084. The process could not connect to Subscriber 'NODE2\SQL2016'.
        Number:  18456
        Message: Login failed for user 'NODE2\repl_distribution'.

8. 此錯誤指出**散發代理程式**無法連線到訂閱者，因為使用者 **NODE2\repl_distribution** 登入失敗。 若要進一步調查，請連線到訂閱者並開啟 [物件總管] 中 [管理] 節點下「目前的」**SQL 錯誤記錄檔**： 

    ![訂閱者登入失敗](media/tutorial-replicating-data-between-continuously-connected-servers/loginfailed.png)：如果您看到這個錯誤表示訂閱者遺失登入。 若要解決此問題，請參閱[在訂閱者端設定資料庫權限](#setting-database-permissions-at-the-subscriber)。

9. 登入錯誤解決後，請再次檢查**複寫監視器**。 如果所有問題都獲得解決，您應該會在**發行集名稱**旁看到一個綠色箭號，而且 [所有訂閱] 下的狀態為 [執行中]。 再以滑鼠右鍵按一下 [訂閱] 以啟動**散發者到訂閱者**記錄，確認是否成功。 如果這是散發代理程式第一次執行，您會看到快照集已大量複製到訂閱者，如下圖所示： 

     ![Dist 代理程式成功](media/tutorial-replicating-data-between-continuously-connected-servers/distagentsuccess.png)   

  ## <a name="next-steps"></a>後續步驟
您已成功為您的異動複寫設定發行者和訂閱者。  您現在可以在發行者端的 **Product** 資料表插入、更新或刪除資料。 接著您可以查詢訂閱者端的 **Product** 資料表以檢視複寫的變更。 下一篇文章會教導您如何設定合併式複寫。  

請前往下一篇文章來進一步了解
> [!div class="nextstepaction"]
> [後續步驟](tutorial-replicating-data-with-mobile-clients.md)

  
