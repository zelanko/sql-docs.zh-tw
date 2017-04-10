---
title: "定義合併資料表發行項之間的邏輯記錄關聯性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "合併式複寫邏輯記錄 [SQL Server 複寫]"
  - "發行項 [SQL Server 複寫], 邏輯記錄"
  - "邏輯記錄 [SQL Server 複寫]"
ms.assetid: ff847b3a-c6b0-4eaf-b225-2ffc899c5558
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 定義合併資料表發行項之間的邏輯記錄關聯性
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中定義合併資料表發行項之間的邏輯記錄關聯性。  
  
 合併式複寫可讓您在不同資料表內定義相關資料列之間的關聯性。 然後這些資料列在同步處理期間，可以當做交易式單位來處理。 可以在兩個發行項之間定義邏輯記錄，不論這些發行項是否有聯結篩選關聯性。 如需詳細資訊，請參閱 [使用邏輯記錄的相關資料列群組變更](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要定義合併資料表發行項之間的邏輯記錄關聯性，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果您在初始化發行集的訂閱後，新增、修改或刪除邏輯記錄，則必須在進行變更後產生新的快照集並重新初始化所有訂閱。 如需屬性變更需求的詳細資訊，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 定義邏輯記錄中的 **加入聯結** 對話方塊中，也就是在新增發行集精靈和 **發行集屬性-\< 發行集>** 對話方塊。 如需使用精靈，並存取此對話方塊的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md) 和 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
 只有將邏輯記錄套用至合併式發行集中的聯結篩選，並且該發行集符合使用預先計算的資料分割要求時，方可在 **[加入聯結]** 對話方塊中定義這些邏輯記錄。 若要定義未套用至聯結篩選的邏輯記錄，並在邏輯記錄層級設定衝突偵測和解決方案，您必須使用預存程序。  
  
#### 若要定義邏輯記錄關聯性  
  
1.  在 **篩選資料表資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，選取一個資料列篩選中 **已篩選的資料表** 窗格。  
  
     邏輯記錄關聯性與聯結篩選相關聯，這會擴充資料列篩選。 因此，您必須在使用聯結擴充篩選並套用邏輯記錄關聯性之前，先定義資料列篩選。 定義好一個聯結篩選後，您可以以另一個聯結篩選擴充這個聯結篩選。 如需定義聯結篩選的詳細資訊，請參閱＜ [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)＞。  
  
2.  按一下 **[加入]**，然後按一下 **[加入聯結以擴充選取的篩選]**。  
  
3.  在 **[加入聯結]** 對話方塊中定義聯結篩選，然後選取 **[邏輯記錄]**核取方塊。  
  
4.  如果您是在 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **確定** 儲存並關閉對話方塊。  
  
#### 若要刪除邏輯記錄關聯性  
  
-   僅刪除邏輯記錄關聯性，或刪除邏輯記錄關聯性及與其相關聯的聯結篩選。  
  
     若要僅刪除邏輯記錄關聯性：  
  
    1.  在 **篩選的資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>** 對話方塊中選取聯結篩選相關聯的邏輯記錄關聯性 **已篩選的資料表** ] 窗格中，然後再按一下 **編輯**。  
  
    2.  在 **[編輯聯結]** 對話方塊中，清除 **[邏輯記錄]**核取方塊。  
  
    3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     若要刪除邏輯記錄關聯性及與其關聯的聯結篩選：  
  
    -   在 **篩選的資料列** 新的發行集精靈] 頁面或 **發行集屬性-\< 發行集>** 對話方塊中，選取篩選器中的 **已篩選的資料表** ] 窗格中，然後再按一下 **刪除**。 如果您刪除的聯結篩選本身已由其他聯結擴充，也會一併刪除這些聯結。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序，以程式設計方式指定發行項之間的邏輯記錄關聯性。  
  
#### 定義沒有相關聯結篩選的邏輯記錄關聯性  
  
1.  如果發行集包含任何篩選的發行項，執行 [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), ，並記下的值 **use_partition_groups** 結果集中。  
  
    -   如果這個值是 **1**，則表示已經使用預先計算的資料分割。  
  
    -   如果值為 **0**, ，然後執行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 於發行集資料庫的發行者端。 指定的值為 **use_partition_groups** 的 **@property** 且值為 **true** 的 **@value**。  
  
        > [!NOTE]  
        >  如果發行集不支援預先計算的資料分割，將無法使用邏輯記錄。 如需詳細資訊，請參閱使用預先計算的資料分割的需求 > 主題中 [最佳化 Parameterized Filter Performance with Precomputed Partitions](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)。  
  
    -   如果此值為 NULL，則必須執行快照集代理程式，才能為發行集產生初始快照集。  
  
2.  如果組成此邏輯記錄的文章不存在，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 於發行集資料庫的發行者端。 針對此邏輯記錄指定下列其中一個衝突偵測和解決選項：  
  
    -   若要偵測及解決邏輯記錄中相關資料列內所發生的衝突，指定其值為 **true** 的 **@logical_record_level_conflict_detection** 和 **@logical_record_level_conflict_resolution**。  
  
    -   若要使用的標準資料列或資料行層級衝突偵測和解決方式，指定其值為 **false** 的 **@logical_record_level_conflict_detection** 和 **@logical_record_level_conflict_resolution**, ，這是預設值。  
  
3.  針對組成此邏輯記錄的每一個發行項重複步驟 2。 您必須針對此邏輯記錄中的每一個發行項使用相同的衝突偵測和解決選項。 如需詳細資訊，請參閱 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md)。  
  
4.  在發行集資料庫的發行者，執行 [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)。 指定 **@publication**, ，關聯性中的一個發行項名稱 **@article**, ，第二個發行項名稱 **@join_articlename**, ，關聯性的名稱 **@filtername**, ，定義兩者之間的關聯性子句的文件的 **@join_filterclause**, ，聯結的類型 **@join_unique_key** 和下列其中一個值 **@filter_type**:  
  
    -   **2** -定義邏輯關聯性。  
  
    -   **3** -定義邏輯關聯性與聯結篩選。  
  
    > [!NOTE]  
    >  如果未使用聯結篩選，則兩個發行項之間的關聯性方向就不是那麼重要。  
  
5.  針對發行集中每一個剩餘的邏輯記錄關聯性重複步驟 2。  
  
#### 變更邏輯記錄的衝突偵測和解決方式  
  
1.  若要偵測及解決邏輯記錄中相關資料列內所發生的衝突：  
  
    -   在發行集資料庫的發行者，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定的值為 **logical_record_level_conflict_detection** 的 **@property** 且值為 **true** 的 **@value**。 指定的值為 **1** 的 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**。  
  
    -   在發行集資料庫的發行者，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定的值為 **logical_record_level_conflict_resolution** 的 **@property** 且值為 **true** 的 **@value**。 指定的值為 **1** 的 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**。  
  
2.  若要使用標準資料列層級或資料行層級的衝突偵測與解決方式：  
  
    -   在發行集資料庫的發行者，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定的值為 **logical_record_level_conflict_detection** 的 **@property** 且值為 **false** 的 **@value**。 指定的值為 **1** 的 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**。  
  
    -   在發行集資料庫的發行者，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定的值為 **logical_record_level_conflict_resolution** 的 **@property** 且值為 **false** 的 **@value**。 指定的值為 **1** 的 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**。  
  
#### 移除邏輯記錄關聯性  
  
1.  在發行集資料庫的發行者上，執行下列查詢來傳回有關針對指定之發行集定義之所有邏輯記錄關聯性的資訊：  
  
     [!code-sql[HowTo#sp_ReturnMergeLogicalRecords](../../../relational-databases/replication/codesnippet/tsql/define-a-logical-record-_1.sql)]  
  
     請注意從結果集中 **filtername** 資料行所移除的邏輯記錄關聯性名稱。  
  
    > [!NOTE]  
    >  此查詢會傳回相同的資訊 [sp_helpmergefilter](../../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md); 不過，此系統預存程序，只傳回邏輯記錄關聯性的相關資訊也屬於聯結篩選。  
  
2.  在發行集資料庫的發行者，執行 [sp_dropmergefilter](../../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)。 指定 **@publication**、關聯性中 **@article**的其中一個發行項名稱，以及步驟 1 中 **@filtername**的關聯性名稱。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 這個範例會在現有的發行集上啟用預先計算的資料分割，並針對 `SalesOrderHeader` 和 `SalesOrderDetail` 資料表建立組成兩個新發行項的邏輯記錄。  
  
 [!code-sql[HowTo#sp_AddMergeLogicalRecord](../../../relational-databases/replication/codesnippet/tsql/define-a-logical-record-_2.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
  
> [!NOTE]  
>  合併式複寫可允許您指定在邏輯記錄層級追蹤及解決衝突，但這些選項無法使用 RMO 來設定。  
  
#### 定義沒有相關聯結篩選的邏輯記錄關聯性  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別中，設定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 發行集，並設定屬性 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 在步驟 1 中建立的連接屬性。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  如果 <xref:Microsoft.SqlServer.Replication.MergePublication.PartitionGroupsOption%2A> 屬性設定為 <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.False>, ，將它設定為 <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.True>。  
  
5.  如果組成此邏輯記錄的文章不存在，則建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergeArticle> 類別，並設定下列屬性︰  
  
    -   發行項名稱 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>。  
  
    -   發行集名稱 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>。  
  
    -   （選擇性）水平篩選發行項，如果指定的資料列篩選子句 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 屬性。 使用此屬性可指定靜態或參數化資料列篩選器。 如需詳細資訊，請參閱 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
     如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Article.Create%2A> 方法。  
  
7.  針對組成此邏輯記錄的每一個發行項重複執行步驟 5 和 6。  
  
8.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 類別來定義發行項之間的邏輯記錄關聯性。 然後，設定下列屬性：  
  
    -   邏輯記錄關聯性中的子發行項名稱 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.ArticleName%2A> 屬性。  
  
    -   邏輯記錄關聯性中的現有父發行項名稱 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinArticleName%2A> 屬性。  
  
    -   邏輯記錄關聯性的名稱 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterName%2A> 屬性。  
  
    -   定義關聯性的運算式 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinFilterClause%2A> 屬性。  
  
    -   值為 <xref:Microsoft.SqlServer.Replication.FilterTypes.LogicalRecordLink> 的 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterTypes%2A> 屬性。 如果邏輯記錄關聯性也是聯結篩選，指定值為 <xref:Microsoft.SqlServer.Replication.FilterTypes.JoinFilterAndLogicalRecordLink> 這個屬性。 如需詳細資訊，請參閱 [使用邏輯記錄的相關資料列群組變更](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
9. 呼叫 <xref:Microsoft.SqlServer.Replication.MergeArticle.AddMergeJoinFilter%2A> 物件，表示關聯性中的子發行項的方法。 傳遞 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 步驟 8 定義關聯性中的物件。  
  
10. 針對發行集中每一個剩餘的邏輯記錄關聯性重複步驟 8 和 9。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 這個範例會針對 `SalesOrderHeader` 和 `SalesOrderDetail` 資料表建立組成兩個新發行項的邏輯記錄。  
  
 [!code-csharp[HowTo#rmo_CreateLogicalRecord](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createlogicalrecord)]  
  
 [!code-vb[HowTo#rmo_vb_CreateLogicalRecord](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createlogicalrecord)]  
  
## 另請參閱  
 [定義和修改合併發行項之間的聯結篩選](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [針對合併發行項定義及修改參數化資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [使用邏輯記錄分組相關資料列的變更](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)   
 [使用預先計算的資料分割最佳化參數化篩選效能](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)   
 [使用邏輯記錄分組相關資料列的變更](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)  
  
  