---
title: "檢視及修改發行集屬性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "檢視複寫屬性"
  - "修改複寫屬性, 發行項"
  - "發行項 [SQL Server 複寫], 修改"
  - "發行集 [SQL Server 複寫]，屬性"
  - "發行項 [SQL Server 複寫], 屬性"
  - "修改複寫屬性，發行集"
  - "發行集 [SQL Server 複寫]，修改"
ms.assetid: 27d72ea4-bcb6-48f2-b4aa-eb1410da7efc
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 檢視及修改發行集屬性
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中檢視及修改發行集屬性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
-   **若要檢視及修改發行集屬性，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   有些屬性在建立了發行集後無法再修改，而另一些當存在發行集的訂閱時便無法修改。 無法修改的屬性以唯讀顯示。  
  
###  <a name="Recommendations"></a> 建議  
  
-   建立發行集之後，某些屬性變更需要新的快照集。 如果發行集有訂閱，則某些變更還需要重新初始化所有訂閱。 如需詳細資訊，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) 和 [新增和卸除現有的發行集的文章](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 檢視及修改發行集屬性，在 **發行集屬性-\< 發行集>** 對話方塊中，可在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 和複寫監視器。 如需啟動複寫監視器的詳細資訊，請參閱 [啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
  **發行集屬性-\< 發行集>** 對話方塊包含下列頁面︰  
  
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
  
#### 若要在 Management Studio 中檢視和修改發行集屬性  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  發行集，以滑鼠右鍵按一下，然後按一下 **屬性**。  
  
4.  必要時修改任何屬性，然後按一下 **[確定]**。  
  
#### 若要在複寫監視器中檢視和修改發行集屬性  
  
1.  展開「複寫監視器」左窗格中的「發行者」群組，然後展開一個「發行者」。  
  
2.  發行集，以滑鼠右鍵按一下，然後按一下 **屬性**。  
  
3.  必要時修改任何屬性，然後按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式修改發行集及傳回其屬性。 您使用的預存程序將根據發行集的類型而定。  
  
#### 檢視快照式或交易式發行集的屬性  
  
1.  執行 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md), ，指定的發行集名稱 **@publication** 參數。 如果您不指定這個參數，就會傳回發行者上與所有發行集有關的資訊。  
  
#### 變更快照式或交易式發行集的屬性  
  
1.  執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), ，指定要變更的發行集屬性 **@property** 參數，這個屬性的新值 **@value** 參數。  
  
    > [!NOTE]  
    >  如果此變更將需要產生新的快照集，您也必須指定值為 **1** 的 **@force_invalidate_snapshot**, ，如果此變更將需要重新初始化訂閱者，您必須指定的值和 **1** 的 **@force_reinit_subscription**。 如需詳細資訊的屬性，變更時需要新的快照集或重新初始化，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
#### 檢視合併式發行集的屬性  
  
1.  執行 [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), ，指定的發行集名稱 **@publication** 參數。 如果您不指定這個參數，就會傳回發行者上與所有發行集有關的資訊。  
  
#### 變更合併式發行集的屬性  
  
1.  執行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), ，指定變更發行集屬性 **@property** 參數，這個屬性的新值 **@value** 參數。  
  
    > [!NOTE]  
    >  如果此變更將需要產生新的快照集，您也必須指定值為 **1** 的 **@force_invalidate_snapshot**, ，如果此變更將需要重新初始化訂閱者，您必須指定的值和 **1** 的 **@force_reinit_subscription** 如需詳細資訊的屬性，變更時需要新的快照集或重新初始化，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
#### 檢視快照集的屬性  
  
1.  執行 [sp_helppublication_snapshot](../../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md), ，指定的發行集名稱 **@publication** 參數。  
  
#### 變更快照集的屬性  
  
1.  執行 [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md), ，指定一或多個適當的快照集參數的新快照集屬性。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 這個異動複寫範例會傳回發行集的屬性。  
  
 [!code-sql[HowTo#sp_helppublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_1.sql)]  
  
 這個異動複寫範例會停用發行集的結構描述複寫。  
  
 [!code-sql[HowTo#sp_changepublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_2.sql)]  
  
 這個合併式複寫範例會傳回發行集的屬性。  
  
 [!code-sql[HowTo#sp_helpmergepublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_3.sql)]  
  
 這個合併式複寫範例會停用發行集的結構描述複寫。  
  
 [!code-sql[HowTo#sp_changemergepublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_4.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式修改發行集及存取其屬性。 用來檢視或修改發行集屬性的 RMO 類別，將取決於發行集的類型而定。  
  
#### 檢視或修改快照式或交易式發行集的屬性  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別中，設定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 發行集，並設定屬性 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 在步驟 1 中建立的連接屬性。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  (選擇性) 若要變更屬性，請針對一或多個可設定的屬性設定新的值。 使用邏輯 AND 運算子 (**&** 在 Microsoft Visual C# 和 **和** Microsoft Visual Basic 中) 以判斷給定 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 值設定為 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性。 使用包含的邏輯 OR 運算子 (**|** Visual C# 中和 **或者** 在 Visual Basic 中) 和排除的邏輯 OR 運算子 (**^** Visual C# 和 **Xor** 在 Visual Basic 中) 變更 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 值 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性。  
  
5.  （選擇性）如果您指定的值 **true** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您指定的值 **false** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （預設值），變更會立即傳送至伺服器。  
  
#### 檢視或修改合併式發行集的屬性  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別中，設定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 發行集，並設定屬性 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 在步驟 1 中建立的連接屬性。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  (選擇性) 若要變更屬性，請針對一或多個可設定的屬性設定新的值。 使用邏輯 AND 運算子 (**&** Visual C# 和 **和** 在 Visual Basic 中) 來判斷給定 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 值設定為 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性。 使用包含的邏輯 OR 運算子 (**|** Visual C# 中和 **或者** 在 Visual Basic 中) 和排除的邏輯 OR 運算子 (**^** Visual C# 和 **Xor** 在 Visual Basic 中) 變更 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 值 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 屬性。  
  
5.  （選擇性）如果您指定的值 **true** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您指定的值 **false** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （預設值），變更會立即傳送至伺服器。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會設定交易式發行集的發行集屬性。 這些變更在明確傳送到伺服器之前，會先加以快取。  
  
 [!code-csharp[HowTo#rmo_ChangeTranPub_cached](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changetranpub_cached)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeTranPub_cached](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changetranpub_cached)]  
  
 此範例會停用合併式發行集的 DDL 複寫。  
  
 [!code-csharp[HowTo#rmo_ChangeMergePub_ddl](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergepub_ddl)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergePub_ddl](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergepub_ddl)]  
  
## 另請參閱  
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [對發行集資料庫進行結構描述變更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [從發行集和 #40; 加入和卸除發行項SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)   
 [檢視資訊並執行工作的發行集與 #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [檢視和修改發行項屬性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  