---
title: "檢視和修改發行項屬性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_changearticle"
  - "sp_helparticle"
  - "檢視複寫屬性"
  - "sp_changemergearticle"
  - "sp_helpmergearticle"
  - "修改複寫屬性, 發行項"
  - "發行項 [SQL Server 複寫], 修改"
  - "發行項 [SQL Server 複寫], 屬性"
ms.assetid: e71831fa-3d39-4e4a-9706-4d3a497082cc
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 檢視和修改發行項屬性
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中檢視及修改發行項屬性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
-   **若要檢視和修改發行項屬性，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   有些屬性在建立了發行集後無法再修改，而另一些當存在發行集的訂閱時便無法修改。 無法修改的屬性以唯讀顯示。  
  
###  <a name="Recommendations"></a> 建議  
  
-   建立發行集之後，某些屬性變更需要新的快照集。 如果發行集有訂閱，則某些變更還需要重新初始化所有訂閱。 如需詳細資訊，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) 和 [新增和卸除現有的發行集的文章](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 檢視及修改發行項屬性在 **發行集屬性-\< 發行集>** 對話方塊中，可在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 和複寫監視器。 如需啟動複寫監視器的詳細資訊，請參閱 [啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
-   **[一般]** 頁面包含發行集名稱和描述、發行集類型以及訂閱過期設定。  
  
-   **[發行項]** 頁面對應「新增發行集精靈」中的 **[發行項]** 頁面。 此頁面用於新增及刪除發行項，以及變更發行項的屬性與資料行篩選。  
  
-   **[篩選資料列]** 頁面對應「新增發行集精靈」中的 **[篩選資料表的資料列]** 頁面。 此頁面用於新增、編輯和刪除所有類型發行集的靜態資料列篩選，以及新增、編輯和刪除合併式發行集的參數化資料列篩選器和聯結篩選。  
  
-   **[快照集]** 頁面允許您指定快照集的格式和位置、是否應壓縮快照集，以及套用快照集前後要執行的指令碼。  
  
-    **FTP 快照集** 頁面 （針對快照式和交易式發行集，以及執行 SQL Server 2005 之前的版本 「 發行者 」 的合併式發行集） 可讓您指定 「 訂閱者 」 是否可以下載快照集檔案透過檔案傳輸通訊協定 (FTP)。  
  
-    **FTP 快照集和網際網路** 頁面 （適用於執行 SQL Server 2005 或更新版本的 「 發行者 」 的合併式發行集） 可讓您指定 「 訂閱者 」 是否可以下載快照集檔案，透過 FTP，和 「 訂閱者 」 可以同步處理訂閱透過 HTTPS。  
  
-   **[訂閱選項]** 頁面允許您設定套用至所有訂閱的一些選項。 選項視發行集類型的不同而不同。  
  
-   **[發行集存取清單]** 頁面允許您指定可存取發行集的登入和群組。  
  
-   **[代理程式安全性]** 頁面允許您存取執行以下代理程式之帳戶的設定，並與複寫拓撲中的電腦建立連接：所有發行集的「快照集代理程式」；所有交易式發行集的「記錄讀取器代理程式」；及允許佇列更新訂閱之交易式發行集的「佇列讀取器代理程式」。  
  
-    **資料分割** 頁面 （針對執行 SQL Server 2005 或更新版本的 「 發行者 」 的合併式發行集） 可讓您指定是否無法使用，使用參數化篩選的發行集的訂閱者是否可以要求快照集。 它還允許您為一個或多個資料分割一次性或按循環排程產生快照集。  
  
#### 若要檢視和修改發行項屬性  
  
1.  在 **文章** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，選取文件，然後按一下 **發行項屬性**。  
  
2.  選取應套用發行項屬性變更的物件︰  
  
    -   按一下 [ **設定的反白顯示屬性 \< ObjectType> 文章** 啟動 **發行項屬性-\< ObjectName>** ] 對話方塊中，屬性在此對話方塊中所做的變更只會套用到的物件，會在 [物件] 窗格上反白顯示 **文章** 頁面。  
  
    -   按一下 [ **設定屬性的所有 \< ObjectType> 文章**, ，以啟動 **所有屬性 \< ObjectType> 文章** ] 對話方塊中，屬性在此對話方塊中所做的變更套用至該類型的物件] 窗格的所有物件上 **文章** ] 頁面上，包括尚未選取 [發行集。  
  
        > [!NOTE]  
        >  屬性中所做的變更 **所有屬性 \< ObjectType> 文章** 對話方塊覆寫任何先前所做的 **發行項屬性-\< o b j>** 對話方塊。 例如，若要設定所有屬於某物件類型之發行項的一些預設值，但同時要設定個別物件的某些屬性，則請先設定所有發行項的預設值， 然後再設定個別物件的屬性。  
  
3.  必要時修改任何屬性，然後按一下 **[確定]**。  
  
4.  按一下 [ **確定** 上 **發行集屬性-\< 發行集>** 對話方塊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式修改發行項及傳回其屬性。 使用哪些預存程序要依發行項所屬的發行集類型而定。  
  
#### 檢視屬於快照式或交易式發行集之發行項的屬性  
  
1.  執行 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md), ，指定的發行集名稱 **@publication** 參數和名稱的發行項的 **@article** 參數。 如果您不指定 **@article**，將會傳回發行集中所有發行項的資訊。  
  
2.  執行 [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) 列出基底資料表中可用的所有資料行的資料表發行項。  
  
#### 修改屬於快照式或交易式發行集之發行項的屬性  
  
1.  執行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md), ，指定變更發行項屬性 **@property** 參數，這個屬性的新值 **@value** 參數。  
  
    > [!NOTE]  
    >  如果該變更需要產生新的快照集，您也必須指定值為 **1** 的 **@force_invalidate_snapshot**, ，如果該變更需要重新初始化訂閱者，您也必須指定的值和 **1** 的 **@force_reinit_subscription**。 如需詳細資訊的屬性，變更時需要新的快照集或重新初始化，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
#### 檢視屬於合併式發行集之發行項的屬性  
  
1.  執行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md), ，指定的發行集名稱 **@publication** 參數和名稱的發行項的 **@article** 參數。 如果您不指定這些參數，將會傳回發行集中或發行者上所有發行項的資訊。  
  
2.  執行 [sp_helpmergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-helpmergearticlecolumn-transact-sql.md) 列出基底資料表中可用的所有資料行的資料表發行項。  
  
#### 修改屬於合併式發行集之發行項的屬性  
  
1.  執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), ，指定變更發行項屬性 **@property** 參數，這個屬性的新值 **@value** 參數。  
  
    > [!NOTE]  
    >  如果該變更需要產生新的快照集，您也必須指定值為 **1** 的 **@force_invalidate_snapshot**, ，如果該變更需要重新初始化訂閱者，您也必須指定的值和 **1** 的 **@force_reinit_subscription**。 如需詳細資訊的屬性，變更時需要新的快照集或重新初始化，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
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
  
#### 檢視或修改屬於快照式或交易式發行集之發行項的屬性  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransArticle> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, ，<xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 屬性。  
  
4.  設定步驟 1 中的連接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的發行項屬性定義不正確，或者該發行項不存在。  
  
6.  （選擇性）若要變更屬性，設定新值的其中一個 <xref:Microsoft.SqlServer.Replication.TransArticle> 可以設定屬性。  
  
7.  （選擇性）如果您指定的值 **true** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您指定的值 **false** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （預設值），變更會立即傳送至伺服器。  
  
#### 檢視或修改屬於合併式發行集之發行項的屬性  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergeArticle> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, ，<xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 屬性。  
  
4.  設定步驟 1 中的連接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的發行項屬性定義不正確，或者該發行項不存在。  
  
6.  （選擇性）若要變更屬性，設定新值的其中一個 <xref:Microsoft.SqlServer.Replication.MergeArticle> 可以設定屬性。  
  
7.  （選擇性）如果您指定的值 **true** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您指定的值 **false** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （預設值），變更會立即傳送至伺服器。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會變更合併發行項，以指定此發行項所使用的商務邏輯處理常式。  
  
 [!code-csharp[HowTo#rmo_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## 另請參閱  
 [為合併發行項實作商務邏輯處理常式](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [進階合併式複寫衝突偵測與解決](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  