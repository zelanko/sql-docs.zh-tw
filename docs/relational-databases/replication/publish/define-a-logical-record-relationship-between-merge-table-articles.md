---
title: "定義合併資料表發行項之間的邏輯記錄關聯性 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication logical records [SQL Server replication]
- articles [SQL Server replication], logical records
- logical records [SQL Server replication]
ms.assetid: ff847b3a-c6b0-4eaf-b225-2ffc899c5558
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3630c769c33d4888f384d00ec341503fc47c89cd
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="define-a-logical-record-relationship-between-merge-table-articles"></a>定義合併資料表發行項之間的邏輯記錄關聯性
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中定義合併資料表發行項之間的邏輯記錄關聯性。  
  
 合併式複寫可讓您在不同資料表內定義相關資料列之間的關聯性。 然後這些資料列在同步處理期間，可以當做交易式單位來處理。 可以在兩個發行項之間定義邏輯記錄，不論這些發行項是否有聯結篩選關聯性。 如需詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
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
  
-   如果您在初始化發行集的訂閱後，新增、修改或刪除邏輯記錄，則必須在進行變更後產生新的快照集並重新初始化所有訂閱。 如需屬性變更需求的詳細資訊，請參閱[變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 您可以在位於 [新增發行集精靈] 和 [發行集屬性 - \<發行集>] 對話方塊的 [加入聯結] 對話方塊中，定義邏輯記錄。 如需使用精靈及存取對話方塊的詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)和[檢視及修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
 只有將邏輯記錄套用至合併式發行集中的聯結篩選，並且該發行集符合使用預先計算的資料分割要求時，方可在 **[加入聯結]** 對話方塊中定義這些邏輯記錄。 若要定義未套用至聯結篩選的邏輯記錄，並在邏輯記錄層級設定衝突偵測和解決方案，您必須使用預存程序。  
  
#### <a name="to-define-a-logical-record-relationship"></a>若要定義邏輯記錄關聯性  
  
1.  在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<發行集>] 對話方塊的 [篩選資料列] 頁面上，從 [已篩選的資料表] 窗格中選取一個資料列篩選。  
  
     邏輯記錄關聯性與聯結篩選相關聯，這會擴充資料列篩選。 因此，您必須在使用聯結擴充篩選並套用邏輯記錄關聯性之前，先定義資料列篩選。 定義好一個聯結篩選後，您可以以另一個聯結篩選擴充這個聯結篩選。 如需定義聯結篩選的詳細資訊，請參閱＜ [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)＞。  
  
2.  按一下 **[加入]**，然後按一下 **[加入聯結以擴充選取的篩選]**。  
  
3.  在 **[加入聯結]** 對話方塊中定義聯結篩選，然後選取 **[邏輯記錄]**核取方塊。  
  
4.  如果您在 [發行集屬性 - \<發行集>] 對話方塊中，請按一下 [確定] 儲存並關閉對話方塊。  
  
#### <a name="to-delete-a-logical-record-relationship"></a>若要刪除邏輯記錄關聯性  
  
-   僅刪除邏輯記錄關聯性，或刪除邏輯記錄關聯性及與其相關聯的聯結篩選。  
  
     若要僅刪除邏輯記錄關聯性：  
  
    1.  在 [新增發行集精靈] 的 [篩選資料列] 頁面上，或是在 [發行集屬性 - \<發行集>] 對話方塊的 [篩選資料列] 頁面上，從 [已篩選的資料表] 窗格中選取與邏輯記錄關聯性相關聯的聯結篩選，然後按一下 [編輯]。  
  
    2.  在 **[編輯聯結]** 對話方塊中，清除 **[邏輯記錄]**核取方塊。  
  
    3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     若要刪除邏輯記錄關聯性及與其關聯的聯結篩選：  
  
    -   在 [新增發行集精靈] 或 [發行集屬性 - \<發行集>] 對話方塊的 [篩選資料列] 頁面上，從 [已篩選的資料表] 窗格中選取一個篩選，然後按一下 [刪除]。 如果您刪除的聯結篩選本身已由其他聯結擴充，也會一併刪除這些聯結。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序，以程式設計方式指定發行項之間的邏輯記錄關聯性。  
  
#### <a name="to-define-a-logical-record-relationship-without-an-associated-join-filter"></a>定義沒有相關聯結篩選的邏輯記錄關聯性  
  
1.  如果發行集包含任何篩選的發行項，請執行 [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)，並記下結果集中的 **use_partition_groups** 值。  
  
    -   如果這個值是 **1**，則表示已經使用預先計算的資料分割。  
  
    -   如果這個值是 **0**，請在發行集資料庫的發行者上執行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 。 請為 **use_partition_groups** 指定 **@property** 的值，並為 **@value** 指定 **@value**。  
  
        > [!NOTE]  
        >  如果發行集不支援預先計算的資料分割，將無法使用邏輯記錄。 如需詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)主題中的＜使用預先計算的資料分割之需求＞。  
  
    -   如果此值為 NULL，則必須執行快照集代理程式，才能為發行集產生初始快照集。  
  
2.  如果組成此邏輯記錄的發行項不存在，請在發行集資料庫的發行者上執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 。 針對此邏輯記錄指定下列其中一個衝突偵測和解決選項：  
  
    -   若要偵測及解決邏輯記錄中相關資料列內所發生的衝突，請為 **@value** 指定 **@logical_record_level_conflict_detection** ＞和＜ **@logical_record_level_conflict_resolution**。  
  
    -   若要使用標準資料列層級或資料行層級的衝突偵測與解決方法，請為 **@logical_record_level_conflict_detection** 指定 **@logical_record_level_conflict_detection** ＞和＜ **@logical_record_level_conflict_resolution**的值 (這是預設值)。  
  
3.  針對組成此邏輯記錄的每一個發行項重複步驟 2。 您必須針對此邏輯記錄中的每一個發行項使用相同的衝突偵測和解決選項。 如需詳細資訊，請參閱 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)。  
  
4.  在發行集資料庫的發行者上，執行 [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)。 指定 **@publication**、關聯性中 **@article**的一個發行項名稱、 **@join_articlename**的第二個發行項名稱、 **@filtername**的關聯性名稱、為 **@join_filterclause**定義兩個發行項之間之關聯性的子句、 **@join_unique_key** 的聯結類型，以及 **@filter_type**的下列其中一個值：  
  
    -   **2** - 定義邏輯關聯性。  
  
    -   **3** - 定義具有聯結篩選的邏輯關聯性。  
  
    > [!NOTE]  
    >  如果未使用聯結篩選，則兩個發行項之間的關聯性方向就不是那麼重要。  
  
5.  針對發行集中每一個剩餘的邏輯記錄關聯性重複步驟 2。  
  
#### <a name="to-change-conflict-detection-and-resolution-for-logical-records"></a>變更邏輯記錄的衝突偵測和解決方式  
  
1.  若要偵測及解決邏輯記錄中相關資料列內所發生的衝突：  
  
    -   在發行集資料庫的發行者上，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 請為 **@property** 指定 **@property** 的值，並為 **@value** 指定 **@value**。 請為 **1** 指定 **@force_invalidate_snapshot** ＞和＜ **@force_reinit_subscription**。  
  
    -   在發行集資料庫的發行者上，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 請為 **@property** 指定 **@property** 的值，並為 **@value** 指定 **@value**。 請為 **1** 指定 **@force_invalidate_snapshot** ＞和＜ **@force_reinit_subscription**。  
  
2.  若要使用標準資料列層級或資料行層級的衝突偵測與解決方式：  
  
    -   在發行集資料庫的發行者上，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 請為 **@property** 指定 **@property** 的值，並為 **@logical_record_level_conflict_detection** 指定 **@value**。 請為 **1** 指定 **@force_invalidate_snapshot** ＞和＜ **@force_reinit_subscription**。  
  
    -   在發行集資料庫的發行者上，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 請為 **@property** 指定 **@property** 的值，並為 **@logical_record_level_conflict_detection** 指定 **@value**。 請為 **1** 指定 **@force_invalidate_snapshot** ＞和＜ **@force_reinit_subscription**。  
  
#### <a name="to-remove-a-logical-record-relationship"></a>移除邏輯記錄關聯性  
  
1.  在發行集資料庫的發行者上，執行下列查詢來傳回有關針對指定之發行集定義之所有邏輯記錄關聯性的資訊：  
  
     [!code-sql[HowTo#sp_ReturnMergeLogicalRecords](../../../relational-databases/replication/codesnippet/tsql/define-a-logical-record-_1.sql)]  
  
     請注意從結果集中 **filtername** 資料行所移除的邏輯記錄關聯性名稱。  
  
    > [!NOTE]  
    >  此查詢會傳回與 [sp_helpmergefilter](../../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)相同的資訊，但是此系統預存程序只會傳回也屬於聯結篩選之邏輯記錄關聯性的相關資訊。  
  
2.  在發行集資料庫的發行者上，執行 [sp_dropmergefilter](../../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)。 指定 **@publication**、關聯性中 **@article**的其中一個發行項名稱，以及步驟 1 中 **@filtername**。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 這個範例會在現有的發行集上啟用預先計算的資料分割，並針對 `SalesOrderHeader` 和 `SalesOrderDetail` 資料表建立組成兩個新發行項的邏輯記錄。  
  
 [!code-sql[HowTo#sp_AddMergeLogicalRecord](../../../relational-databases/replication/codesnippet/tsql/define-a-logical-record-_2.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
  
> [!NOTE]  
>  合併式複寫可允許您指定在邏輯記錄層級追蹤及解決衝突，但這些選項無法使用 RMO 來設定。  
  
#### <a name="to-define-a-logical-record-relationship-without-an-associated-join-filter"></a>定義沒有相關聯結篩選的邏輯記錄關聯性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體、為發行集設定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性，以及將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為步驟 1 中所建立的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  如果 <xref:Microsoft.SqlServer.Replication.MergePublication.PartitionGroupsOption%2A> 屬性設定為 <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.False>，請將它設定為 <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.True>。  
  
5.  如果組成此邏輯記錄的發行項不存在，請建立 <xref:Microsoft.SqlServer.Replication.MergeArticle> 類別的執行個體，並設定以下屬性：  
  
    -   為 <xref:Microsoft.SqlServer.Replication.Article.Name%2A> 設定發行項的名稱。  
  
    -   為 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A> 設定發行集名稱。  
  
    -   (選擇性) 如果以水平方式篩選此發行項，請為 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 屬性指定資料列篩選子句。 使用此屬性可指定靜態或參數化資料列篩選器。 如需詳細資訊，請參閱 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。  
  
     如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Article.Create%2A> 方法。  
  
7.  針對組成此邏輯記錄的每一個發行項重複執行步驟 5 和 6。  
  
8.  建立 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 類別的執行個體，以定義發行項之間的邏輯記錄關聯性。 然後，設定下列屬性：  
  
    -   為 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.ArticleName%2A> 屬性設定邏輯記錄關聯性中的子發行項名稱。  
  
    -   為 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinArticleName%2A> 屬性設定邏輯記錄關聯性中的現有父發行項名稱。  
  
    -   為 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterName%2A> 屬性設定邏輯記錄關聯性的名稱。  
  
    -   為 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinFilterClause%2A> 屬性設定定義此關聯性的運算式。  
  
    -   為 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterTypes%2A> 屬性設定 <xref:Microsoft.SqlServer.Replication.FilterTypes.LogicalRecordLink> 的值。 如果邏輯記錄關聯性也是聯結篩選，請針對這個屬性指定 <xref:Microsoft.SqlServer.Replication.FilterTypes.JoinFilterAndLogicalRecordLink> 的值。 如需詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
9. 在表示關聯性子發行項的物件上呼叫 <xref:Microsoft.SqlServer.Replication.MergeArticle.AddMergeJoinFilter%2A> 方法。 傳遞步驟 8 中的 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 物件來定義關聯性。  
  
10. 針對發行集中每一個剩餘的邏輯記錄關聯性重複步驟 8 和 9。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 這個範例會針對 `SalesOrderHeader` 和 `SalesOrderDetail` 資料表建立組成兩個新發行項的邏輯記錄。  
  
 [!code-cs[HowTo#rmo_CreateLogicalRecord](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createlogicalrecord)]  
  
 [!code-vb[HowTo#rmo_vb_CreateLogicalRecord](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createlogicalrecord)]  
  
## <a name="see-also"></a>另請參閱  
 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [針對合併發行項定義及修改參數化資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [定義及修改靜態資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [使用邏輯記錄分組相關資料列的變更](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)   
 [使用預先計算的資料分割最佳化參數化篩選效能](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)   
 [使用邏輯記錄分組相關資料列的變更](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)  
  
  
