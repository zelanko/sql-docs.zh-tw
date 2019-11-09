---
title: 定義及修改靜態資料列篩選 | Microsoft 文件
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying filters, static row
- static row filters
- filters [SQL Server replication], static row
ms.assetid: a6ebb026-026f-4c39-b6a9-b9998c3babab
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7bb7aebed25c571108e4b0d7e7366fc52c45e3c1
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882302"
---
# <a name="define-and-modify-a-static-row-filter"></a>定義及修改靜態資料列篩選
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
  
-   如果您在初始化發行集的訂閱後，新增、修改或刪除靜態資料列篩選，則必須在進行變更後產生新的快照集並重新初始化所有訂閱。 如需屬性變更需求的詳細資訊，請參閱[變更發行集與發行項屬性](change-publication-and-article-properties.md)。  
  
-   如果為點對點異動複寫啟用發行集，則無法篩選資料表。  
  
###  <a name="Recommendations"></a> 建議  
  
-   由於這些篩選都是靜態的，所以所有訂閱者都將收到相同子集的資料。 如果您需要動態篩選屬於合併式發行集之資料表發行項內的資料，好讓每一個訂閱者都會收到不同的資料分割，請參閱＜ [Define and Modify a Parameterized Row Filter for a Merge Article](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)＞。 合併式複寫也可讓您根據現有的資料列篩選來篩選相關的資料列。 如需詳細資訊，請參閱 [Define and Modify a Join Filter Between Merge Articles](define-and-modify-a-join-filter-between-merge-articles.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 您可以在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - **發行集>]** **對話方塊的 [篩選資料列]\<** 頁面上，定義、修改及刪除靜態資料列篩選。 如需使用精靈和存取對話方塊的詳細資訊，請參閱[建立發行集](create-a-publication.md)和[檢視及修改發行集屬性](view-and-modify-publication-properties.md)。  
  
#### <a name="to-define-a-static-row-filter"></a>若要定義靜態資料列篩選  
  
1.  在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - **發行集>]** **對話方塊的 [篩選資料列]\<** 頁面上，您所採取的動作會視發行集類型而定：  
  
    -   對於快照式或交易式發行集，請按一下 **[加入]** 。  
  
    -   對於合併式發行集，請按一下 **[加入]** ，然後按一下 **[加入篩選]** 。  
  
2.  在 **[加入篩選]** 對話方塊中，從下拉式清單方塊中選取要篩選的資料表。  
  
3.  在 **[篩選陳述式]** 文字區域中建立篩選陳述式。 您可直接在文字區域輸入，也可以從 **[資料行]** 清單方塊中拖曳資料行。  
  
    > [!NOTE]  
    >  WHERE 子句應使用兩部份命名；不支援三部份及四部份命名。 如果發行集來自「Oracle 發行者」，則 WHERE 子句必須與 Oracle 語法相容。  
  
    -   **[篩選陳述式]** 文字區域包括預設文字，其格式為：  
  
        ```sql  
        SELECT <published_columns> FROM [schema].[tablename] WHERE  
        ```  
  
    -   預設的文字無法變更；使用標準 SQL 語法，在 WHERE 關鍵字後面輸入篩選子句。 完整的篩選子句應類似於：  
  
        ```sql  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE [LoginID] = 'adventure-works\ranjit0'  
        ```  
  
    -   靜態資料列篩選可以包含使用者定義函數。 含有使用者定義函數的靜態資料列篩選之完整的篩選子句應類似於：  
  
        ```sql  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] WHERE MyFunction([Freight]) > 100  
        ```  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您在 [發行集屬性 - **發行集>]\<** 對話方塊中，請按一下 [確定] 儲存並關閉對話方塊。  
  
#### <a name="to-modify-a-static-row-filter"></a>若要修改靜態資料列篩選  
  
1.  在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - **發行集>]** **對話方塊的 [篩選資料列]\<** 頁面上，從 [已篩選的資料表] 窗格中選取一個篩選，然後按一下 [編輯]。  
  
2.  在 **[編輯篩選]** 對話方塊中，修改篩選。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-static-row-filter"></a>若要刪除靜態資料列篩選  
  
1.  在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - **發行集>]** **對話方塊的 [篩選資料列]\<** 頁面上，從 [已篩選的資料表] 窗格中選取一個篩選，然後按一下 [刪除]。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 當您建立資料表發行項時，可以定義 WHERE 子句從發行項篩選資料列。 您也可以在定義資料列篩選之後，加以變更。 您可以使用複寫預存程序來以程式設計的方式建立及修改靜態資料列篩選。  
  
#### <a name="to-define-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>為快照式或交易式發行集定義靜態資料列篩選  
  
1.  定義要篩選的發行項。 如需詳細資訊，請參閱 [Define an Article](define-an-article.md)。  
  
2.  在發行集資料庫的發行者端，執行 [sp_articlefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql)。 為 **\@article** 指定發行項的名稱、為 **\@publication** 指定發行集的名稱、為 **\@filter_name** 指定篩選的名稱，並為 **\@filter_clause** (不包括 `WHERE`) 指定篩選子句。  
  
3.  如果仍然必須定義資料行篩選，請參閱＜ [定義及修改資料行篩選](define-and-modify-a-column-filter.md)＞。 否則，執行 [sp_articleview &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql)。 為 **\@publication** 指定發行集的名稱、為 **\@article** 指定篩選的發行項名稱，並為 **\@filter_clause** 指定步驟 2 中所指定的篩選子句。 這樣會針對篩選的發行項建立同步處理物件。  
  
#### <a name="to-modify-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>為快照式或交易式發行集修改靜態資料列篩選  
  
1.  在發行集資料庫的發行者端，執行 [sp_articlefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql)。 為 **\@article** 指定發行項的名稱、為 **\@publication** 指定發行集的名稱、為 **\@filter_name** 指定新的篩選名稱，並為 **\@filter_clause** (不包括 `WHERE`) 指定新的篩選子句。 由於這項變更將會讓現有訂閱中的資料失效，所以請為force_reinit_subscription **指定 \@1** 值。  
  
2.  在發行集資料庫的發行者端，執行 [sp_articleview &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql)。 為 **\@publication** 指定發行集的名稱、為 **\@article** 指定篩選的發行項名稱，並為 **\@filter_clause** 指定步驟 1 中所指定的篩選子句。 這樣會重新建立可定義篩選之發行項的檢視。  
  
3.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)。  
  
4.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../reinitialize-subscriptions.md)。  
  
#### <a name="to-delete-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>為快照式或交易式發行集刪除靜態資料列篩選  
  
1.  在發行集資料庫的發行者端，執行 [sp_articlefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql)。 為 **\@article** 指定發行項的名稱、為 **\@publication** 指定發行集的名稱、為 **\@filter_name** 指定 NULL 的值，並為 **\@filter_clause** 指定 NULL 的值。 由於這項變更將會讓現有訂閱中的資料失效，所以請為force_reinit_subscription **指定 \@1** 值。  
  
2.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)。  
  
3.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../reinitialize-subscriptions.md)。  
  
#### <a name="to-define-a-static-row-filter-for-a-merge-publication"></a>為合併式發行集定義靜態資料列篩選  
  
1.  在發行集資料庫的發行者端，執行 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 為 **\@subset_filterclause** (不包括 `WHERE`) 指定篩選子句。 如需詳細資訊，請參閱 [Define an Article](define-an-article.md)。  
  
2.  如果仍然必須定義資料行篩選，請參閱＜ [定義及修改資料行篩選](define-and-modify-a-column-filter.md)＞。  
  
#### <a name="to-modify-a-static-row-filter-for-a-merge-publication"></a>為合併式發行集修改靜態資料列篩選  
  
1.  在發行集資料庫的發行者端，執行 [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)。 為 **\@publication** 指定發行集的名稱、為 **\@article** 指定篩選的發行項名稱、為property **指定 \@subset_filterclause** 值，並為 **\@value** (不包括 `WHERE`) 指定新的篩選子句。 由於這項變更將會讓現有訂閱中的資料失效，所以請為 **\@force_reinit_subscription** 指定 1 值。  
  
2.  針對此發行集重新執行快照集代理程式作業，以產生更新的快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)。  
  
3.  重新初始化訂閱。 如需詳細資訊，請參閱 [重新初始化訂閱](../reinitialize-subscriptions.md)。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 在此異動複寫範例中，會以水平方式篩選此發行項，以移除所有不再生產的產品。  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createtranpub.sql#sp_addtranarticle)]  
  
 在此合併式複寫範例中，會以水平方式篩選發行項，以便只傳回屬於指定之銷售人員的資料列。 也會使用聯結篩選。 如需詳細資訊，請參閱 [Define and Modify a Join Filter Between Merge Articles](define-and-modify-a-join-filter-between-merge-articles.md)。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepub.sql#sp_addmergearticle)]  
  
## <a name="see-also"></a>另請參閱  
 [針對合併發行項定義及修改參數化資料列篩選](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [變更發行集與發行項屬性](change-publication-and-article-properties.md)   
 [篩選發行的資料](filter-published-data.md)   
 [合併式複寫之篩選發行資料](../merge/filter-published-data-for-merge-replication.md)  
  
  
