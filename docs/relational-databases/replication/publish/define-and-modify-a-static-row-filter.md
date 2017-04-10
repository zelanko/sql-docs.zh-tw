---
title: "定義及修改靜態資料列篩選 | Microsoft Docs"
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
  - "modifying filters, static row"
  - "static row filters"
  - "篩選 [SQL Server 複寫], 靜態資料列"
ms.assetid: a6ebb026-026f-4c39-b6a9-b9998c3babab
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 定義及修改靜態資料列篩選
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中定義及修改靜態資料列篩選。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
-   **若要定義及修改靜態資料列篩選，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果您在初始化發行集的訂閱後，新增、修改或刪除靜態資料列篩選，則必須在進行變更後產生新的快照集並重新初始化所有訂閱。 如需屬性變更需求的詳細資訊，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
-   如果為點對點異動複寫啟用發行集，則無法篩選資料表。  
  
###  <a name="Recommendations"></a> 建議  
  
-   由於這些篩選都是靜態的，所以所有訂閱者都將收到相同子集的資料。 如果您需要動態篩選屬於合併式發行集之資料表發行項內的資料，好讓每一個訂閱者都會收到不同的資料分割，請參閱＜ [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)＞。 合併式複寫也可讓您根據現有的資料列篩選來篩選相關的資料列。 如需詳細資訊，請參閱 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 定義、 修改和刪除靜態資料列篩選器上 **篩選資料表資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>** 對話方塊。 如需使用精靈，並存取此對話方塊的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md) 和 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 若要定義靜態資料列篩選  
  
1.  在 **篩選資料表資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，您採取的動作取決於發行集的類型︰  
  
    -   對於快照式或交易式發行集，請按一下 **[加入]**。  
  
    -   對於合併式發行集，請按一下 **[加入]**，然後按一下 **[加入篩選]**。  
  
2.  在 **加入篩選條件** 對話方塊中，選取要從下拉式清單方塊篩選的資料表。  
  
3.  在 **[篩選陳述式]** 文字區域中建立篩選陳述式。 您可直接在文字區域輸入，也可以從 **[資料行]** 清單方塊中拖曳資料行。  
  
    > [!NOTE]  
    >  WHERE 子句應使用兩部份命名；不支援三部份及四部份命名。 如果發行集來自「Oracle 發行者」，則 WHERE 子句必須與 Oracle 語法相容。  
  
    -   **[篩選陳述式]** 文字區域包括預設文字，其格式為：  
  
        ```tsql  
        SELECT <published_columns> FROM [schema].[tablename] WHERE  
        ```  
  
    -   預設的文字無法變更；使用標準 SQL 語法，在 WHERE 關鍵字後面輸入篩選子句。 完整的篩選子句應類似於：  
  
        ```tsql  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE [LoginID] = 'adventure-works\ranjit0'  
        ```  
  
    -   靜態資料列篩選可以包含使用者定義函數。 含有使用者定義函數的靜態資料列篩選之完整的篩選子句應類似於：  
  
        ```tsql  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] WHERE MyFunction([Freight]) > 100  
        ```  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您是在 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **確定** 儲存並關閉對話方塊。  
  
#### 若要修改靜態資料列篩選  
  
1.  在 **篩選資料表資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，選取篩選器中的 **已篩選的資料表** ] 窗格中，然後再按一下 **編輯**。  
  
2.  在 **[編輯篩選]** 對話方塊中，修改篩選。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 若要刪除靜態資料列篩選  
  
1.  在 **篩選資料表資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，選取篩選器中的 **已篩選的資料表** ] 窗格中，然後再按一下 **刪除**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 當您建立資料表發行項時，可以定義 WHERE 子句從發行項篩選資料列。 您也可以在定義資料列篩選之後，加以變更。 您可以使用複寫預存程序來以程式設計的方式建立及修改靜態資料列篩選。  
  
#### 為快照式或交易式發行集定義靜態資料列篩選  
  
1.  定義要篩選的發行項。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在發行集資料庫的發行者，執行 [sp_articlefilter & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)。 指定的發行項的名稱 **@article**, ，發行集名稱 **@publication**, 的篩選條件的名稱 **@filter_name**, ，並篩選子句 **@filter_clause** (不包括 `WHERE`)。  
  
3.  如果仍然必須定義資料行篩選，請參閱＜ [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)＞。 否則，執行 [sp_articleview & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 指定的發行集名稱 **@publication**, ，用於篩選的發行項名稱 **@article**, ，和步驟 2 中指定的篩選子句 **@filter_clause**。 這樣會針對篩選的發行項建立同步處理物件。  
  
#### 為快照式或交易式發行集修改靜態資料列篩選  
  
1.  在發行集資料庫的發行者，執行 [sp_articlefilter & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)。 指定的發行項的名稱 **@article**, ，發行集名稱 **@publication**, ，為新的篩選器的名稱 **@filter_name**, ，並為新的篩選子句 **@filter_clause** (不包括 `WHERE`)。 這項變更將會導致現有的訂閱中的資料無效，因為指定的值為 **1** 的 **@force_reinit_subscription**。  
  
2.  在發行集資料庫的發行者，執行 [sp_articleview & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 指定的發行集名稱 **@publication**, ，篩選的發行項的名稱 **@article**, ，並為步驟 1 中所指定的篩選子句 **@filter_clause**。 這樣會重新建立可定義篩選之發行項的檢視。  
  
3.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
4.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### 為快照式或交易式發行集刪除靜態資料列篩選  
  
1.  在發行集資料庫的發行者，執行 [sp_articlefilter & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)。 指定的發行項的名稱 **@article**, ，發行集名稱 **@publication**, ，其值為 NULL 的 **@filter_name**, ，和其值為 NULL 的 **@filter_clause**。 這項變更將會導致現有的訂閱中的資料無效，因為指定的值為 **1** 的 **@force_reinit_subscription**。  
  
2.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
3.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### 為合併式發行集定義靜態資料列篩選  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定的篩選子句 **@subset_filterclause** (不包括 `WHERE`)。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  如果仍然必須定義資料行篩選，請參閱＜ [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)＞。  
  
#### 為合併式發行集修改靜態資料列篩選  
  
1.  在發行集資料庫的發行者，執行 [sp_changemergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定發行集名稱 **@publication**, ，篩選的發行項的名稱 **@article**, ，值 **subset_filterclause** 的 **@property**, ，並為新的篩選子句 **@value** (不包括 `WHERE`)。 這項變更將會導致現有的訂閱中的資料無效，因為指定的值為 1 **@force_reinit_subscription**。  
  
2.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
3.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 在此異動複寫範例中，會以水平方式篩選此發行項，以移除所有不再生產的產品。  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_1.sql)]  
  
 在此合併式複寫範例中，會以水平方式篩選發行項，以便只傳回屬於指定之銷售人員的資料列。 也會使用聯結篩選。 如需詳細資訊，請參閱 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_2.sql)]  
  
## 另請參閱  
 [針對合併發行項定義及修改參數化資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [篩選發行的資料](../../../relational-databases/replication/publish/filter-published-data.md)   
 [篩選合併式複寫之發行的資料](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  