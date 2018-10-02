---
title: 檢視和修改發行項屬性 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changearticle
- sp_helparticle
- viewing replication properties
- sp_changemergearticle
- sp_helpmergearticle
- modifying replication properties, articles
- articles [SQL Server replication], modifying
- articles [SQL Server replication], properties
ms.assetid: e71831fa-3d39-4e4a-9706-4d3a497082cc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9ccee2c8fd7fe02ff038105bd4bc934201ed861c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710406"
---
# <a name="view-and-modify-article-properties"></a>檢視和修改發行項屬性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中檢視及修改發行項屬性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
-   **若要檢視和修改發行項屬性，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   有些屬性在建立了發行集後無法再修改，而另一些當存在發行集的訂閱時便無法修改。 無法修改的屬性以唯讀顯示。  
  
###  <a name="Recommendations"></a> 建議  
  
-   建立發行集之後，某些屬性變更需要新的快照集。 如果發行集有訂閱，則某些變更還需要重新初始化所有訂閱。 如需詳細資訊，請參閱[變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)和[在現有發行集中新增和卸除發行項](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 您可以在位於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 和複寫監視器的 [發行集屬性 - \<發行集>] 對話方塊中，檢視及修改發行項屬性。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
-   **[一般]** 頁面包含發行集名稱和描述、發行集類型以及訂閱過期設定。  
  
-   **[發行項]** 頁面對應「新增發行集精靈」中的 **[發行項]** 頁面。 此頁面用於新增及刪除發行項，以及變更發行項的屬性與資料行篩選。  
  
-   **[篩選資料列]** 頁面對應「新增發行集精靈」中的 **[篩選資料表的資料列]** 頁面。 此頁面用於新增、編輯和刪除所有類型發行集的靜態資料列篩選，以及新增、編輯和刪除合併式發行集的參數化資料列篩選器和聯結篩選。  
  
-   **[快照集]** 頁面允許您指定快照集的格式和位置、是否應壓縮快照集，以及套用快照集前後要執行的指令碼。  
  
-   **[FTP 快照集]** 頁面 (針對快照式和交易式發行集，以及執行 SQL Server 2005 之前版本之「發行者」的合併式發行集) 允許您指定「訂閱者」是否可以透過「檔案傳輸通訊協定」(FTP) 下載快照集檔案。  
  
-   **[FTP 快照集和網際網路]** 頁面 (針對執行 SQL Server 2005 或更新版本之「發行者」的合併式發行集) 允許您指定「訂閱者」是否可以透過 FTP 下載快照集檔案，以及「訂閱者」是否可以透過 HTTP 同步處理訂閱。  
  
-   **[訂閱選項]** 頁面允許您設定套用至所有訂閱的一些選項。 選項視發行集類型的不同而不同。  
  
-   **[發行集存取清單]** 頁面允許您指定可存取發行集的登入和群組。  
  
-   **[代理程式安全性]** 頁面允許您存取執行以下代理程式之帳戶的設定，並與複寫拓撲中的電腦建立連接：所有發行集的「快照集代理程式」；所有交易式發行集的「記錄讀取器代理程式」；及允許佇列更新訂閱之交易式發行集的「佇列讀取器代理程式」。  
  
-   **[資料分割]** 頁面 (針對執行 SQL Server 2005 或更新版本之「發行者」的合併式發行集) 允許您指定至含參數化篩選之發行集的「訂閱者」是否可以在一個快照集不可用時要求另一個快照集。 它還允許您為一個或多個資料分割一次性或按循環排程產生快照集。  
  
#### <a name="to-view-and-modify-article-properties"></a>若要檢視和修改發行項屬性  
  
1.  在 [發行集屬性 - \<發行集>]  對話方塊的 [發行項] 頁面上，選取一個發行項，然後按一下 [發行項屬性]。  
  
2.  選取應套用發行項屬性變更的物件︰  
  
    -   按一下 [設定反白顯示 \<物件類型> 發行項的屬性]  啟動 [發行項屬性 - \<物件名稱>] 對話方塊；在這個對話方塊中所做的屬性變更，只會套用至 [發行項] 頁面的物件窗格中反白顯示的物件。  
  
    -   按一下 [設定所有 \<物件類型> 發行項的屬性] 啟動 [所有 \<物件類型> 發行項的屬性] 對話方塊；在這個對話方塊中所做的屬性變更，會套用至 [發行項] 頁面的物件窗格中屬於該類型的所有物件，包括尚未選取發行的物件。  
  
        > [!NOTE]  
        >  在 [所有 \<物件類型> 發行項的屬性] 對話方塊中所做的屬性變更，會覆寫之前在 [發行項屬性 - \<物件名稱>] 對話方塊中所做的任何變更。 例如，若要設定所有屬於某物件類型之發行項的一些預設值，但同時要設定個別物件的某些屬性，則請先設定所有發行項的預設值， 然後再設定個別物件的屬性。  
  
3.  必要時修改任何屬性，然後按一下 **[確定]**。  
  
4.  在 [發行集屬性 - \<發行集>] 對話方塊上，按一下 [確定]。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式修改發行項及傳回其屬性。 使用哪些預存程序要依發行項所屬的發行集類型而定。  
  
#### <a name="to-view-the-properties-of-an-article-belonging-to-a-snapshot-or-transactional-publication"></a>檢視屬於快照式或交易式發行集之發行項的屬性  
  
1.  執行 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)，針對 **@publication** 參數指定發行集的名稱，並針對 **@article** 參數指定發行項的名稱。 如果您不指定 **@article**，將會傳回發行集中所有發行項的資訊。  
  
2.  針對資料表發行項執行 [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) ，以列出基底資料表中可用的所有資料行。  
  
#### <a name="to-modify-the-properties-of-an-article-belonging-to-a-snapshot-or-transactional-publication"></a>修改屬於快照式或交易式發行集之發行項的屬性  
  
1.  執行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)，在 **@property** 參數中指定變更的發行項屬性，並在 **@value** 參數指定發行項的名稱。  
  
    > [!NOTE]  
    >  如果此變更需要產生新的快照集，您也必須針對 **@force_invalidate_snapshot** 指定 **@force_invalidate_snapshot**的值，而如果此變更需要重新初始化訂閱者，您也必須針對 **@force_invalidate_snapshot** 指定 **@force_reinit_subscription**。 如需當變更時需要新的快照集或重新初始化之屬性的詳細資訊，請參閱[變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
#### <a name="to-view-the-properties-of-an-article-belonging-to-a-merge-publication"></a>檢視屬於合併式發行集之發行項的屬性  
  
1.  執行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)，針對 **@publication** 參數指定發行集的名稱，並針對 **@article** 參數指定發行項的名稱。 如果您不指定這些參數，將會傳回發行集中或發行者上所有發行項的資訊。  
  
2.  針對資料表發行項執行 [sp_helpmergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-helpmergearticlecolumn-transact-sql.md) ，以列出基底資料表中可用的所有資料行。  
  
#### <a name="to-modify-the-properties-of-an-article-belonging-to-a-merge-publication"></a>修改屬於合併式發行集之發行項的屬性  
  
1.  執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)，在 **@property** 參數中指定變更的發行項屬性，並在 **@value** 參數指定發行項的名稱。  
  
    > [!NOTE]  
    >  如果此變更需要產生新的快照集，您也必須針對 **@force_invalidate_snapshot** 指定 **@force_invalidate_snapshot**的值，而如果此變更需要重新初始化訂閱者，您也必須針對 **@force_invalidate_snapshot** 指定 **@force_reinit_subscription**。 如需當變更時需要新的快照集或重新初始化之屬性的詳細資訊，請參閱[變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
###  <a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
 這個異動複寫範例會傳回已發行之發行項的屬性。  
  
 [!code-sql[HowTo#sp_helptranarticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_1.sql)]  
  
 這個異動複寫範例會變更已發行之發行項的結構描述選項。  
  
 [!code-sql[HowTo#sp_changetranarticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_2.sql)]  
  
 這個合併式複寫範例會傳回已發行之發行項的屬性。  
  
 [!code-sql[HowTo#sp_helpmergearticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_3.sql)]  
  
 這個合併式複寫範例會變更已發行之發行項的衝突偵測設定。  
  
 [!code-sql[HowTo#sp_changemergearticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_4.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式修改發行項及存取其屬性。 用來檢視或修改發行項屬性的 RMO 類別，將取決於發行項所屬的發行集類型而定。  
  
#### <a name="to-view-or-modify-properties-of-an-article-that-belongs-to-a-snapshot-or-transactional-publication"></a>檢視或修改屬於快照式或交易式發行集之發行項的屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransArticle> 類別的執行個體。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 屬性。  
  
4.  針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定步驟 1 中的連接。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的發行項屬性定義不正確，或者該發行項不存在。  
  
6.  (選擇性) 若要變更屬性，請針對其中一個可設定的 <xref:Microsoft.SqlServer.Replication.TransArticle> 屬性設定新的值。  
  
7.  (選擇性) 如果您已針對 **P:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges** 指定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>的值，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您已針對 **false** 指定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 的值 (預設值)，則會立即將變更傳送到伺服器。  
  
#### <a name="to-view-or-modify-properties-of-an-article-that-belongs-to-a-merge-publication"></a>檢視或修改屬於合併式發行集之發行項的屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergeArticle> 類別的執行個體。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 屬性。  
  
4.  針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定步驟 1 中的連接。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的發行項屬性定義不正確，或者該發行項不存在。  
  
6.  (選擇性) 若要變更屬性，請針對其中一個可設定的 <xref:Microsoft.SqlServer.Replication.MergeArticle> 屬性設定新的值。  
  
7.  (選擇性) 如果您已針對 **P:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges** 指定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>的值，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您已針對 **false** 指定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 的值 (預設值)，則會立即將變更傳送到伺服器。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會變更合併發行項，以指定此發行項所使用的商務邏輯處理常式。  
  
 [!code-cs[HowTo#rmo_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## <a name="see-also"></a>另請參閱  
 [為合併發行項實作商務邏輯處理常式](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
