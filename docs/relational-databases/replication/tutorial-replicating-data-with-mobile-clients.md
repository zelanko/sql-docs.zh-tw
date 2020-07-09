---
title: 教學課程：設定合併式複寫
description: 此教學課程教您如何設定 SQL Server 和行動用戶端之間的合併式複寫。
ms.custom: seo-lt-2019
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: quickstart
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4110d523762a147a569caaf03d71dbdc4567c5c3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720695"
---
# <a name="tutorial-configure-replication-between-a-server-and-mobile-clients-merge"></a>教學課程：設定伺服器和行動用戶端之間的複寫 (合併式)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
對於在中央伺服器與只是偶爾連線的行動用戶端之間移動資料的問題，合併式複寫是一個很好的解決方案。 您可以使用複寫精靈，輕鬆設定及管理合併式複寫拓撲。 

本教學課程告訴您，如何為行動用戶端設定複寫拓撲。 如需合併式複寫的詳細資訊，請參閱[合併式複寫概觀](https://docs.microsoft.com/sql/relational-databases/replication/merge/merge-replication)。
  
## <a name="what-you-will-learn"></a>學習內容  
本教學課程會教導您如何使用合併式複寫，從中央資料庫發行資料給一或多個行動使用者，讓每一個使用者都取得獨一無二篩選的資料子集。 

在本教學課程中，您將學會如何：
> [!div class="checklist"]
> * 設定合併式複寫的發行者。
> * 新增合併式發行集的行動訂閱者。
> * 同步處理合併式發行集的訂閱。
  
## <a name="prerequisites"></a>Prerequisites  
本教學課程是特別提供給熟悉基本資料庫作業但對複寫經驗有限的使用者。 開始進行本教學課程之前，您必須先完成[教學課程：準備 SQL Server 進行複寫](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)。  
  
若要完成本教學課程，您需要 SQL Server、SQL Server Management Studio (SSMS) 以及 AdventureWorks 資料庫： 
  
- 在發行者伺服器 (來源) 安裝：  
  
   - 任何版本的 SQL Server，SQL Server Express 或 SQL Server Compact 除外。 這兩種版本無法作為複寫發行者。   
   - [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫。 為了加強安全性，依預設，不會安裝範例資料庫。  
  
- 除 SQL Server Express 或 SQL Server Compact 之外，在訂閱者伺服器 (目的地) 安裝任何版本的 SQL Server。 在本教學課程中建立的發行集不支援 SQL Server Express 或 SQL Server Compact。 

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases)。 有關在 SSMS 中還原資料庫的指示，請參閱[還原資料庫](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。  
 
  
>[!NOTE]
> - 相差兩個版本以上的 SQL Server 執行個體不支援複寫。 如需詳細資訊，請參閱 [Supported SQL Server Versions in Replication Topology](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/) (複寫拓撲中支援的 SQL Server 版本)。
> - 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，您用來與發行者和訂閱者連線的登入資料，必須是**系統管理員**固定伺服器角色的一員。 如需此角色的詳細資訊，請參閱[伺服器層級角色](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/server-level-roles)。  
  
  
**完成此教學課程的估計時間：60 分鐘**  
  
## <a name="configure-a-publisher-for-merge-replication"></a>設定合併式複寫的發行者
在這一節中，您會使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 建立合併式發行集，以發行 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫中 **Employee**、**SalesOrderHeader** 和 **SalesOrderDetail** 資料表的子集。 這些資料表是以參數化資料列篩選器加以篩選，讓每一個訂閱包含唯一的資料分割。 此外，您也會將合併代理程式所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入新增至發行集存取清單 (PAL)。  
  
### <a name="create-merge-publication-and-define-articles"></a>建立合併式發行集並定義發行項  
  
1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者，然後展開伺服器節點。  
  
2. 以滑鼠右鍵按一下 [物件總管] 中的 SQL Server Agent 來啟動它，然後選取 [啟動]  。 如果此步驟無法啟動代理程式，您必須從 SQL Server 組態管理員以手動方式啟動它。  
3. 展開 [複寫]  資料夾，然後以滑鼠右鍵按一下 [本機發行集]  ，再選取 [新增發行集]  。 [新增發行集精靈] 會隨即啟動：  

   ![啟動 [新增發行集精靈] 的選項](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
3. 在 [發行集資料庫]  頁面上，選取 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，然後選取 [下一步]  。 

      
4. 在 [發行集類型]  頁面上，選取 [合併式發行集]  ，然後選取 [下一步]  。  
   
5. 在 [訂閱者類型]  頁面上，確定只選取 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本，然後選取 [下一步]  ： 

    ![[發行集類型] 和 [訂閱者類型] 頁面](media/tutorial-replicating-data-with-mobile-clients/mergerpl.png)
  
   
6. 在 [發行項]  頁面上，展開 [資料表]  節點。 選取下列三個資料表：**Employee**、**SalesOrderHeader** 和 **SalesOrderDetail**。 選取 [下一步]  。  

   ![[發行項] 頁面上的 [資料表] 選項](media/tutorial-replicating-data-with-mobile-clients/mergearticles.png)

   >[!NOTE]
   > **Employee** 資料表包含的資料行 (**OrganizationNode**) 具有 **hierarchyid** 資料類型。 此資料類型僅受 SQL Server 2017 中的複寫支援。 
   >
   > 如果您使用的組建早於 SQL Server 2017，畫面底部會出現訊息，通知您在雙向複寫中使用此資料行可能會遺失資料。 為達到本教學課程的目的，您可以忽略此訊息。 不過，除非您使用的是受支援的組建，否則不應該在生產環境中複寫此資料類型。
   > 
   > 如需複寫 **hierarchyid** 資料類型的詳細資訊，請參閱[在複寫中使用 hierarchyid 資料行](https://docs.microsoft.com/sql/t-sql/data-types/hierarchyid-data-type-method-reference#using-hierarchyid-columns-in-replicated-tables)。
    
  
7. 在 [篩選資料表的資料列]  頁面上，選取 [新增]  ，然後選取 [新增篩選]  。  
  
8. 在 [新增篩選]  對話方塊中，選取 [選取要篩選的資料表]  中的 [Employee (HumanResources)]  。 選取 [LoginID]  資料行，再選取向右鍵將資料行新增至篩選查詢的 WHERE 子句中，並依照下列方式修改 WHERE 子句：  
  
   ```sql 
    WHERE [LoginID] = HOST_NAME()  
   ```  
  
   選取 [這個資料表中的一個資料列只會提供給一個訂閱]  ，然後選取 [確定]  。  
 
   ![新增篩選的選項](media/tutorial-replicating-data-with-mobile-clients/mergeaddfilter.png)

    
  
10. 在 [篩選資料表的資料列]  頁面上，依序選取 [Employee (Human Resources)]  、[新增]  和 [Add Join to Extend the Selected Filter] \(新增聯結以展開選取的篩選\)  。  
  
    a. 在 [新增聯結]  對話方塊中，選取 [聯結的資料表]  下的 [Sales.SalesOrderHeader]  。 選取 [手動寫入聯結陳述式]  並完成聯結陳述式，如下所示：  
  
    ```sql  
    ON [Employee].[BusinessEntityID] =  [SalesOrderHeader].[SalesPersonID] 
    ```  
  
    b. 在 [指定聯結選項]  中，選取 [唯一索引鍵]  ，然後選取 [確定]  。

    ![將聯結新增至篩選的選項](media/tutorial-replicating-data-with-mobile-clients/mergeaddjoin.png)

  
13. 在 [篩選資料表的資料列]  頁面上，依序選取 [SalesOrderHeader]  、[新增]  和 [Add Join to Extend the Selected Filter] \(新增聯結以展開選取的篩選\)  。  
  
    a. 在 [加入聯結]  對話方塊中，選取 [聯結的資料表]  之下的 [Sales.SalesOrderDetail]  。    
    b. 選取 [使用產生器建立陳述式]  。  
    c. 在 [預覽]  方塊中確認聯結陳述式，如下所示：  
  
    ```sql  
    ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID] 
    ```  
  
    d. 在 [指定聯結選項]  中，選取 [唯一索引鍵]  ，然後選取 [確定]  。 選取 [下一步]  。 

    ![為銷售訂單新增另一個聯結的選項](media/tutorial-replicating-data-with-mobile-clients/joinsalestables.png)
  
21. 選取 [立即建立快照集]  ，清除 [排程快照集代理程式在下列時間執行]  ，然後選取 [下一步]  ：  

    ![立即建立快照集的選項](media/tutorial-replicating-data-with-mobile-clients/snapshotagent.png)
  
22. 在 [代理程式安全性]  頁面上，選取 [安全性設定]  。 在 [處理帳戶]  方塊中輸入 <發行者電腦名稱  > **\repl_snapshot**，提供此帳戶的密碼並選取 [確定]  。 選取 [下一步]  。  

    ![設定快照集代理程式安全性的選項](media/tutorial-replicating-data-with-mobile-clients/snapshotagentsecurity.png)
  
23. 在 [完成精靈]  頁面的 [發行集名稱]  方塊中輸入 **AdvWorksSalesOrdersMerge**，然後選取 [完成]  ：  

    ![[完成精靈] 頁面與發行集名稱](media/tutorial-replicating-data-with-mobile-clients/namemergerepl.png)
  
24. 建立發行集之後，選取 [關閉]  。 在 [物件總管]  的 [複寫]  節點 下，以滑鼠右鍵按一下 [本機發行集]  ，然後選取 [重新整理]  以檢視您的新合併式複寫。  
  
### <a name="view-the-status-of-snapshot-generation"></a>檢視快照集產生的狀態  
  
1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者，展開伺服器節點，然後展開 [複寫]  資料夾。  
  
2. 在 [本機發行集]  資料夾中，以滑鼠右鍵按一下 **AdvWorksSalesOrdersMerge**，然後選取 [檢視快照集代理程式的狀態]  ：  

   ![檢視快照集代理程式狀態的選項](media/tutorial-replicating-data-with-mobile-clients/viewsnapshotagentstatus.png)
  
3. 發行集快照集代理程式作業的目前狀態會隨即顯示。 確認快照集作業已成功，再繼續進行下一課。  
  
### <a name="add-the-merge-agent-login-to-the-pal"></a>將合併代理程式登入新增至 PAL  
  
1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者，展開伺服器節點，然後展開 [複寫]  資料夾。  
  
2. 在 [本機發行集]  資料夾中，以滑鼠右鍵按一下 **AdvWorksSalesOrdersMerge**，然後選取 [屬性]  。  
  
   a. 選取 [發行集存取清單]  頁面，然後選取 [新增]  。 
  
   b. 在 [新增發行集存取]  對話方塊中，選取 <發行者電腦名稱  > **\repl_merge**，然後選取 [確定]  。 再次選取 [確定]  。 

   ![新增合併代理程式登入的選項](media/tutorial-replicating-data-with-mobile-clients/mergepal.png) 

  
如需詳細資訊，請參閱  
- [篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md) 
- [參數化資料列篩選](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
- [定義發行項](../../relational-databases/replication/publish/define-an-article.md)  
  
  
## <a name="create-a-subscription-to-the-merge-publication"></a>建立合併式發行集的訂閱
在這一節中，您會將訂閱新增至您之前建立的合併式發行集。 本教學課程使用遠端訂閱者 (NODE2\SQL2016)。 接著，您會在訂閱資料庫上設定權限，並手動為新訂閱產生已篩選資料快照集。   
  
### <a name="add-a-subscriber-for-merge-publication"></a>新增合併式發行集的訂閱者
  
1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的訂閱者，然後展開伺服器節點。 展開 [複寫]  資料夾，然後以滑鼠右鍵按一下 [本機發行集]  資料夾，再選取 [新增訂閱]  。 [新增訂閱精靈] 會隨即啟動：

   ![啟動 [新增訂閱精靈] 的選項](media/tutorial-replicating-data-with-mobile-clients/newsub.png)
  
2. 在 [發行集]  頁面上，選取 [發行者]  清單中的 [尋找 SQL Server 發行者]  。  
  
   在 [連線到伺服器]  對話方塊的 [伺服器名稱]  方塊中，輸入發行者執行個體的名稱，然後選取 [連線]  。 

   ![新增發行者的選項](media/tutorial-replicating-data-with-mobile-clients/publication.png)
  
4. 選取 [AdvWorksSalesOrdersMerge]  ，然後選取 [下一步]  。  
  
5. 在 [合併代理程式位置]  頁面上，選取 [在訂閱者端執行每一個代理程式]  ，然後選取 [下一步]  ：  

   ![[在訂閱者端執行每一個代理程式] 選項](media/tutorial-replicating-data-with-mobile-clients/pullsub.png)
  
6. 在 [訂閱者]  頁面上，選取訂閱者伺服器的執行個體名稱。 在 [訂閱資料庫]  下，從清單中選取 [新增資料庫]  。  
  
   在 [新增資料庫]  對話方塊的 [資料庫名稱]  方塊中，輸入 **SalesOrdersReplica**。 依序選取 [確定]  和 [下一步]  。 

   ![將資料庫新增至訂閱者的選項](media/tutorial-replicating-data-with-mobile-clients/addsubdb.png)
  
8. 在 [合併代理程式安全性]  頁面上，選取省略符號 ( **...** ) 按鈕。 在 [處理帳戶]  方塊中輸入 <訂閱者電腦名稱  > **\repl_merge**，並提供此帳戶的密碼。 依序選取 [確定]  和 [下一步]  ，然後再次選取 [下一步]  。  

   ![[合併代理程式安全性] 的選項](media/tutorial-replicating-data-with-mobile-clients/mergeagentsecurity.png)

9. 在 [同步處理排程]  頁面上，將 [代理程式排程]  設為 [視需要執行]  。 選取 [下一步]  。  

   ![代理程式的 [視需要執行] 選項](media/tutorial-replicating-data-with-mobile-clients/mergesyncschedule.png)
  
9. 在 [初始化訂閱]  頁面上，從 [初始化時機]  清單中選取 [第一次同步處理時]  。 選取 [下一步]  繼續前往 [訂閱類型]  頁面，然後選取適當的訂閱類型。 本教學課程使用 [用戶端]  。 選取訂閱類型之後，再次選取 [下一步]  。 

   ![第一次同步處理時初始化訂閱的選項](media/tutorial-replicating-data-with-mobile-clients/firstsync.png)

10. 在 [HOST_NAME 值]  頁面的 [HOST_NAME 值]  方塊中，輸入 **adventure-works\pamela0**值。 然後選取 [完成]  。  

    ![[HOST_NAME 值] 頁面](media/tutorial-replicating-data-with-mobile-clients/hostname.png)
  
11. 再次選取 [完成]  。 建立訂閱之後，選取 [關閉]  。  

### <a name="set-server-permissions-at-the-subscriber"></a>在訂閱者端設定伺服器權限  
  
1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的訂閱者。 展開 [安全性]  並以滑鼠右鍵按一下 [登入]  ，然後選取 [新增登入]  。  
  
   在 [一般]  頁面中選取 [搜尋]  ，然後在 [輸入物件名稱]  方塊中輸入 <訂閱者電腦名稱  > **\repl_merge**。 選取 [檢查名稱]  ，然後選取 [確定]  。 
    
   ![設定登入的選項](media/tutorial-replicating-data-with-mobile-clients/sublogin.png)
  
1. 在 [使用者對應]  頁面上，選取 [SalesOrdersReplica]  資料庫，並選取 [db_owner]  角色。 在 [安全性實體]  頁面上，授與 [改變追蹤]  的 [明確]  權限。 選取 [確定]  。

   ![[使用者對應] 和 [安全性實體] 頁面](media/tutorial-replicating-data-with-mobile-clients/setdbo.png)
  
### <a name="create-the-filtered-data-snapshot-for-the-subscription"></a>為訂閱建立已篩選資料快照集  
  
1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者，展開伺服器節點，然後展開 [複寫]  資料夾。  
  
2. 在 [本機發行集]  資料夾中，以滑鼠右鍵按一下 [AdvWorksSalesOrdersMerge]  發行集，然後選取 [屬性]  。  
   
   a. 選取 [資料分割]  頁面，然後選取 [新增]  。   
   b. 在 [新增資料分割]  對話方塊的 [HOST_NAME 值]  方塊中，輸入 **adventure-works\pamela0**，然後選取 [確定]  。  
   c. 選取最近新增的資料分割，選取 [立即產生選取的快照集]  ，然後選取 [確定]  。 

   ![新增資料分割的選項](media/tutorial-replicating-data-with-mobile-clients/partition.png)
  
  
如需詳細資訊，請參閱  
- [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
- [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)  
- [含參數化篩選之合併式發行集的快照集](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  

## <a name="synchronize-the-subscription-to-the-merge-publication"></a>同步處理合併式發行集的訂閱

在這一節中，您會啟動合併代理程式，使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來初始化訂閱。 此外，您會使用此程序與發行者進行同步處理。   
  
### <a name="start-synchronization-and-initialize-the-subscription"></a>啟動同步處理並初始化訂閱  
  
1. 連線到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的訂閱者。  
2. 請確定 SQL Server Agent 正在執行。 如未執行，請以滑鼠右鍵按一下 [物件總管] 中的 SQL Server Agent，然後選取 [啟動]  。 如果此步驟無法啟動代理程式，您必須使用 SQL Server 組態管理員以手動方式啟動它。 
  
2. 展開 [複寫]  資料夾。 在 [本機訂閱]  資料夾中，以滑鼠右鍵按一下 **SalesOrdersReplica** 資料庫中的訂閱，然後選取 [檢視同步處理的狀態]  。  
  
   選取 [啟動]  初始化訂閱。 

   ![同步處理狀態與 [啟動] 按鈕](media/tutorial-replicating-data-with-mobile-clients/mergesyncstatus.png)
    
  
  
## <a name="next-steps"></a>後續步驟  
您已成功為您的合併式複寫設定發行者和訂閱者。 您也可以：

1. 在發行者或訂閱者端插入、更新或刪除 **SalesOrderHeader** 或 **SalesOrderDetail** 資料表中的資料。
2. 在可以使用網路連線來同步處理發行者與訂閱者之間的資料時，重複此程序。
3. 在其他伺服器上查詢 **SalesOrderHeader** 或 **SalesOrderDetail** 資料表，以檢視複寫的變更。  
  
如需詳細資訊，請參閱   
- [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
- [同步處理資料](../../relational-databases/replication/synchronize-data.md)  
- [同步處理提取訂閱](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
  
  
  
