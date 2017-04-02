---
title: "定義和修改合併發行項之間的聯結篩選 | Microsoft Docs"
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
  - "篩選 [SQL Server 複寫], 聯結"
  - "合併式複寫聯結篩選 [SQL Server 複寫]"
  - "修改篩選, 聯結"
  - "聯結篩選"
ms.assetid: f7f23415-43ff-40f5-b3e0-0be1d148ee5b
caps.latest.revision: 46
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# 定義和修改合併發行項之間的聯結篩選
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中定義及修改合併發行項之間的聯結篩選。 合併式複寫支援聯結篩選，聯結篩選通常會配合參數化篩選一起使用，以將資料表資料分割擴充到其他相關的資料表發行項。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
-   **若要定義和修改合併發行項之間的聯結篩選，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   若要建立聯結篩選，發行集至少必須包含兩個相關的資料表。 聯結篩選會擴充資料列篩選；因此您必須先定義一個資料表上的資料列篩選，然後才可利用聯結在另一個資料表上擴充篩選。 定義好一個聯結篩選後，如果發行集包含其他相關資料表，您可以用另一個聯結篩選擴充這個聯結篩選。  
  
-   如果您在初始化發行集的訂閱後，新增、修改或刪除聯結篩選，則必須在進行變更後產生新的快照集並重新初始化所有訂閱。 如需屬性變更需求的詳細資訊，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
###  <a name="Recommendations"></a> 建議  
  
-   可以為一組資料表手動建立聯結篩選，或者根據資料表中定義的外部索引鍵與主索引鍵之間的關聯性自動產生篩選。 如需自動產生一組聯結篩選的詳細資訊，請參閱 [自動產生設定聯結篩選之間合併發行項的 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 定義、 修改和刪除聯結篩選 **篩選資料表資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>** 對話方塊。 如需使用精靈，並存取此對話方塊的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md) 和 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 若要定義聯結篩選  
  
1.  在 **篩選資料表資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>**, 中，選取現有的資料列篩選或聯結篩選 **已篩選的資料表** 窗格。  
  
2.  按一下 **[加入]**，然後按一下 **[加入聯結以擴充選取的篩選]**。  
  
3.  建立聯結陳述式：選取 [使用產生器建立陳述式]  或 [手動寫入 join 陳述式] 。  
  
    -   如果您選取使用產生器，使用的資料行在方格中 (**搭配**, ，**篩選資料表資料行**, ，**運算子**, ，和 **聯結資料表資料行**) 來建立聯結陳述式。  
  
         在方格中的每個資料行包含一個下拉式清單方塊，可讓您選取兩個資料行和一個運算子 (**=**, ，**<>**, ，**<=**, ，**\<**, ，**>=**, ，**>**, ，和 **像**)。 結果會在 **[預覽]** 文字區域中顯示。 如果聯結涉及一對以上的資料行，選取一個結合 (或 OR) 從 **搭配** 資料行，然後輸入兩個多個資料行和一個運算子。  
  
    -   如果選取手動寫入陳述式，請在 **[聯結陳述式]** 文字區域寫入聯結陳述式。 使用 **[已篩選的資料表資料行]** 清單方塊與 **[聯結的資料表資料行]** 清單方塊將資料行拖放到 **[Join 陳述式]** 文字區域。  
  
    -   完整的聯結陳述式應類似於：  
  
        ```  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] INNER JOIN [Sales].[SalesOrderDetail] ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID]  
        ```  
  
         JOIN 子句應該使用兩段式命名；不支援三段式和四段式命名。  
  
4.  指定聯結選項：  
  
    -   如果您加入的篩選資料表 （父資料表） 中的資料行是唯一的選取 **唯一索引鍵**。  
  
        > [!CAUTION]  
        >  選取此選項表示聯結篩選中的子資料表與父資料表之間的關聯性是一對一或一對多。 如果在子系資料表中的聯結資料行有保證唯一性的條件約束，請僅選取此選項。 如果選項設定不正確，則資料可能發生非聚合的情況。  
  
    -   依預設，合併式複寫在同步處理過程中會按逐個資料列的方式處理變更。 若要將相關的篩選的資料表及聯結的資料表當做一個單位處理之資料列中的變更，請選取 **邏輯記錄** ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本)。 只有當發行項與發行集之使用邏輯記錄的需求均符合時，才可以使用此選項。 如需詳細資訊請參閱 「 使用邏輯記錄的考量 」 一節中 [使用邏輯記錄的相關資料列群組變更](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  如果您是在 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **確定** 儲存並關閉對話方塊。  
  
#### 若要修改聯結篩選  
  
1.  在 **篩選資料表資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>**, ，選取篩選器，在 **已篩選的資料表** ] 窗格中，然後再按一下 **編輯**。  
  
2.  在 **[編輯聯結]** 對話方塊中，修改篩選。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 若要刪除聯結篩選  
  
1.  在 **篩選資料表資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>**, ，選取篩選器，在 **已篩選的資料表** ] 窗格中，然後再按一下 **刪除**。 如果您刪除的聯結篩選本身已由其他聯結擴充，也會一併刪除這些聯結。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 這些程序顯示父發行項上的參數化篩選，其中包含此發行項與相關子發行項之間的聯結篩選。 您可以使用複寫預存程序來以程式設計的方式定義及修改聯結篩選。  
  
#### 定義聯結篩選，將發行項擴充到合併式發行集中的相關發行項  
  
1.  針對聯結的發行項定義篩選，此發行項也稱為父發行項。  
  
    -   如需使用參數化資料列篩選器篩選的發行項，請參閱＜ [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)＞。  
  
    -   如需使用靜態資料列篩選進行篩選的發行項，請參閱＜ [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)＞。  
  
2.  在發行集資料庫的發行者，執行 [sp_addmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 若要定義一個或多個相關文件，也就是也稱為子發行項，發行集。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
3.  在發行集資料庫的發行者，執行 [sp_addmergefilter & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)。 指定 **@publication**, ，此篩選條件的唯一名稱 **@filtername**, ，如步驟 2 中建立的子發行項名稱 **@article**, ，如聯結至父發行項名稱 **@join_articlename**, ，和下列其中一個值 **@join_unique_key**:  
  
    -   **0** -指示父和子發行項之間的多對一或多對多聯結。  
  
    -   **1** -指示父和子發行項之間的一對一或一對多的聯結。  
  
     這樣會定義兩個發行項之間的聯結篩選。  
  
    > [!CAUTION]  
    >  只有設定 **@join_unique_key** 至 **1** 如果您有保證唯一性的父發行項之基礎資料表中的聯結資料行的條件約束。 如果 **@join_unique_key** 設為 **1** 不正確，可能會發生非聚合的資料。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 這個範例會針對合併式發行集定義發行項，其中會針對 `SalesOrderDetail` 資料表篩選 `SalesOrderHeader` 資料表發行項 (前者資料表本身會使用靜態資料列篩選來進行篩選)。 如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_1.sql)]  
  
 這個範例會使用一系列的聯結篩選來針對已篩選發行項的合併式發行集中定義一組發行 `Employee` 也就是資料表本身的值上使用參數化資料列篩選進行篩選 [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) 中 **LoginID** 資料行。 如需詳細資訊，請參閱 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_2.sql)]  
  
## 另請參閱  
 [聯結篩選](../../../relational-databases/replication/merge/join-filters.md)   
 [參數化資料列篩選器](../../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [篩選合併式複寫之發行的資料](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)   
 [如何：定義和修改合併發行項之間的聯結篩選 (SQL Server Management Studio)](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [定義合併資料表發行項之間的邏輯記錄關聯性](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [針對合併發行項定義及修改參數化資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
  