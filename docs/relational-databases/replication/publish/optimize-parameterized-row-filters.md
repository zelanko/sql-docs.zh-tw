---
title: "最佳化參數化資料列篩選 | Microsoft Docs"
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
  - "預先計算的資料分割 [SQL Server 複寫]"
  - "篩選 [SQL Server 複寫], 參數化"
  - "合併式複寫預先計算的資料分割 [SQL Server 複寫], SQL Server Management Studio"
  - "參數化篩選 [SQL Server 複寫], 最佳化"
ms.assetid: 49349605-ebd0-4757-95be-c0447f30ba13
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 最佳化參數化資料列篩選
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中最佳化參數化資料列篩選。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
-   **若要最佳化參數化資料列篩選，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   在使用參數化篩選器時，您可以在建立發行集時，藉由指定 [使用資料分割群組]  選項或 [保留資料分割變更]  選項來控制合併式複寫要如何處理篩選。 這兩個選項都可以透過在發行集資料庫中儲存其他中繼資料，以提升具有篩選發行項之發行集的同步處理效能。 您可以在建立發行項時，藉由設定 [資料分割選項]  來控制要如何在訂閱者之間共用資料。 如需有關這些需求的詳細資訊，請參閱＜ [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)＞。  
  
     對於 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]SQL Server Compact 訂閱者，必須將 keep_partition_changes 設為 true，才能確保正確傳播刪除。 設為 false 時，訂閱者所擁有的資料列可能比預期多。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 下列設定可用於最佳化參數化資料列篩選器：  
  
 **資料分割選項**  
 此選項設為 on **屬性** 頁面 **發行項屬性-\< 發行項>** 對話方塊中，或是在 **加入篩選條件** 對話方塊。 這兩個對話方塊會在新增發行集精靈和 **發行集屬性-\< 發行集>** 對話方塊。  **發行項屬性-\< 發行項>** 對話方塊可讓您指定這個選項不適用於的其他值 **加入篩選條件** 對話方塊。  
  
 **預先計算資料分割**  
 此選項設定為 **True** 依預設，如果您的發行集中發行項符合一組需求。 如需這些需求的詳細資訊，請參閱 [最佳化 Parameterized Filter Performance with Precomputed Partitions](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)。 修改此選項在 **訂閱選項** 頁面 **發行集屬性-\< 發行集>** 對話方塊。  
  
 **最佳化同步處理**  
 這個選項應該設為 **True** 才 **預先計算資料分割** 設為 **False**。 此選項設為 on **訂閱選項** 頁面 **發行集屬性-\< 發行集>** 對話方塊。  
  
 如需有關使用 「 新增發行集精靈 」 及存取 **發行集屬性-\< 發行集>** 對話方塊中，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md) 和 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 若要在加入篩選或編輯篩選對話方塊中設定資料分割選項  
  
1.  在 **篩選資料表資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，按一下 **新增**, ，然後按一下 [ **加入篩選條件**。  
  
2.  建立參數化篩選。 如需詳細資訊，請參閱 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
3.  選取符合資料在訂閱者之間共用資料方式的選項：  
  
    -   **這個資料表中的一個資料列會提供給多個訂閱**  
  
    -   **這個資料表中的一個資料列只會提供給一個訂閱**  
  
     若您選取 **[這個資料表中的一個資料列只會提供給一個訂閱]**，合併式複寫可藉由儲存和處理較少中繼資料來將效能最佳化。 不過您必須確定資料分割方式不會將資料列複寫至多個訂閱者。 如需進一步資訊，請參閱主題＜ [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)＞中的「設定資料分割選項」。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您是在 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **確定** 儲存並關閉對話方塊。  
  
#### 若要設定資料分割選項中的發行項屬性-\< 發行項> 對話方塊  
  
1.  在 **文章** 新的發行集精靈] 頁面或 **發行集屬性-\< 發行集>** 對話方塊中，選取資料表，然後按一下 **發行項屬性**。  
  
2.  按一下 **[設定反白顯示資料表發行項的屬性]** 或 **[設定所有資料表發行項的屬性]**。  
  
3.  在 **目的地物件** 區段 **屬性** ] 索引標籤的 **發行項屬性-\< 發行項>** 對話方塊方塊中，指定下列值的其中一個 **資料分割選項**:  
  
    -   **重疊**  
  
    -   **重疊，不允許變更資料分割外的資料**  
  
    -   **不重疊，單一訂閱**  
  
    -   **不重疊，共用於訂閱之間**  
  
     如需這些選項及其如何與 **[加入篩選]** 和 **[編輯篩選]** 對話方塊中可用之選項相關聯的詳細資訊，請參閱＜ [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)＞的「設定資料分割選項」一節。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您是在 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **確定** 儲存並關閉對話方塊。  
  
#### 若要設定預先計算資料分割  
  
1.  在 **訂閱選項** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，選取一個值 **預先計算資料分割** 選項。 在下列情況下，該屬性是唯讀的：  
  
    -   發行集不符合預先計算資料分割的需求。  
  
    -   尚未產生此發行集的快照集。 在此情況下，選項會顯示 **[建立快照時會自動設定]**的值。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 若要設定最佳化同步處理  
  
1.  上 **訂閱選項** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，選取值 **True** 針對 **最佳化同步處理** 選項。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 如需篩選選項的定義 **@keep_partition_changes** 和 **@use_partition_groups**, ，請參閱 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。  
  
#### 在建立新的發行集時指定合併篩選最佳化  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 指定 **@publication** ，並針對下列其中一個參數指定 **true** 的值：  
  
    -   **@use_partition_groups**:-最高的效能最佳化，前提是發行項符合預先計算資料分割的需求。 如需詳細資訊，請參閱 [最佳化 Parameterized Filter Performance with Precomputed Partitions](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)。  
  
    -   **@keep_partition_changes** -如果預先計算的資料分割不能使用此最佳化。  
  
2.  加入此發行集的快照集作業。 如需詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
3.  在發行集資料庫的發行者，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), ，指定下列參數︰  
  
    -   **@publication** -步驟 1 中發行集的名稱。  
  
    -   **@article** -發行項的名稱  
  
    -   **@source_object** -發行的資料庫物件。  
  
    -   **@subset_filterclause** -用來水平篩選發行項的選擇性參數化的篩選子句。  
  
    -   **@partition_options** -篩選之發行項的資料分割選項。  
  
4.  針對發行集中的每一個發行項重複步驟 3。  
  
5.  （選擇性）在發行集資料庫的發行者，執行 [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 來定義兩個發行項之間的聯結篩選。 如需詳細資訊，請參閱 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
#### 檢視及修改現有發行集的合併篩選行為  
  
1.  （選擇性）在發行集資料庫的發行者，執行 [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), ，並指定 **@publication**。 記下的值 **keep_partition_changes** 和 **use_partition_groups** 結果集中。  
  
2.  （選擇性）在發行集資料庫的發行者，執行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 指定的值為 **use_partition_groups** 的 **@property** 和 **true** 或 **false** 的 **@value**。  
  
3.  （選擇性）在發行集資料庫的發行者，執行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 指定的值為 **keep_partition_changes** 的 **@property** 和 **true** 或 **false** 的 **@value**。  
  
    > [!NOTE]  
    >  啟用時 **keep_partition_changes**, ，您必須先停用 **use_partition_groups** 和指定的值為 **1** 的 **@force_reinit_subscription**。  
  
4.  （選擇性）在發行集資料庫的發行者，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定的值為 **partition_options** 的 **@property** 和適當的值給 **@value**。 請參閱 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 定義這些篩選選項。  
  
5.  (選擇性) 在必要時，啟動快照集代理程式來重新產生快照集。 如需哪些變更需要產生新的快照集的資訊，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
## 另請參閱  
 [自動產生一組的合併發行項和 #40; 之間的聯結篩選SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md)   
 [針對合併發行項定義及修改參數化資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [參數化資料列篩選器](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  