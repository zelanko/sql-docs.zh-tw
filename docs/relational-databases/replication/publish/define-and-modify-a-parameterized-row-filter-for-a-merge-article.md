---
title: "針對合併發行項定義及修改參數化資料列篩選 | Microsoft Docs"
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
  - "參數化篩選 [SQL Server 複寫], 定義"
  - "參數化篩選 [SQL Server 複寫], 修改"
  - "合併式複寫 [SQL Server 複寫]，動態篩選"
  - "合併式複寫參數化篩選 [SQL Server 複寫]"
  - "篩選 [SQL Server 複寫], 參數化"
  - "修改篩選, 參數化資料列"
  - "動態篩選 [SQL Server 複寫]"
ms.assetid: de0482a2-3cc8-4030-8a4a-14364549ac9f
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 針對合併發行項定義及修改參數化資料列篩選
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中定義及修改參數化資料列篩選。  
  
 在建立資料表發行項時，您可以使用參數化資料列篩選器。 這些篩選器使用 [其中](../../../t-sql/queries/where-transact-sql.md) 子句來選取要發行的適當資料。 您不需要指定子句中的常值 （如同對靜態資料列篩選），您可以指定一個或多個下列系統函數︰ [SUSER_SNAME](../../../t-sql/functions/suser-sname-transact-sql.md) 和 [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md)。 如需詳細資訊，請參閱 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要定義及修改參數化資料列篩選，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果您在初始化發行集的訂閱後，新增、修改或刪除參數化資料列篩選，則必須在進行變更後產生新的快照集並重新初始化所有訂閱。 如需屬性變更需求的詳細資訊，請參閱 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
###  <a name="Recommendations"></a> 建議  
  
-   基於效能的考量，我們建議您不要在參數化資料列篩選器子句中，將函數套用至資料行名稱上，如 `LEFT([MyColumn]) = SUSER_SNAME()`。 如果在篩選子句中使用 HOST_NAME，並且覆寫 HOST_NAME 值，則可能需要使用 CONVERT 來轉換資料類型。 如需此案例的最佳作法的詳細資訊，請參閱主題中的 「 覆寫 host_name （） 值 」 一節 [參數化資料列篩選](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 定義、 修改和刪除參數化資料列篩選器上 **篩選資料表資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>** 對話方塊。 如需使用精靈，並存取此對話方塊的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md) 和 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 若要定義參數化資料列篩選器  
  
1.  在 **篩選資料表資料列** 新增發行集精靈 」 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>**, ，按一下 **新增**, ，然後按一下 [ **加入篩選條件**。  
  
2.  在 **加入篩選條件** 對話方塊中，選取要從下拉式清單方塊篩選的資料表。  
  
3.  建立篩選陳述式中的 **篩選陳述式** 文字方塊。 您可直接在文字區域輸入，也可以從 **[資料行]** 清單方塊中拖曳資料行。  
  
    -   **[篩選陳述式]** 文字區域包括預設文字，其格式為：  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
    -   預設的文字無法變更；使用標準 SQL 語法，在 WHERE 關鍵字後面輸入篩選子句。 參數化的篩選中包含的系統函式呼叫 **host_name （)** 及/或 **suser_sname （)**, ，或參考上述一或兩種函式的使用者定義函式。 下列為參數化資料列篩選器的完整篩選子句範例：  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         WHERE 子句應使用兩部份命名；不支援三部份及四部份命名。  
  
4.  選取符合資料在訂閱者之間共用資料方式的選項：  
  
    -   **這個資料表中的一個資料列會提供給多個訂閱**  
  
    -   **這個資料表中的一個資料列只會提供給一個訂閱**  
  
     若您選取 **[這個資料表中的一個資料列只會提供給一個訂閱]**，合併式複寫可藉由儲存和處理較少中繼資料來將效能最佳化。 不過您必須確定資料分割方式不會將資料列複寫至多個訂閱者。 如需進一步資訊，請參閱主題＜ [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)＞中的「設定資料分割選項」。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  如果您是在 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **確定** 儲存並關閉對話方塊。  
  
#### 若要修改參數化資料列篩選器  
  
1.  在 **篩選資料表資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>**, ，選取篩選器，在 **已篩選的資料表** ] 窗格中，然後再按一下 **編輯**。  
  
2.  在 **[編輯篩選]** 對話方塊中，修改篩選。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 若要刪除參數化資料列篩選器  
  
1.  在 **篩選資料表資料列** 新的發行集精靈] 頁面或 **篩選的資料列** 頁面 **發行集屬性-\< 發行集>**, ，選取篩選器，在 **已篩選的資料表** ] 窗格中，然後再按一下 **刪除**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式建立及修改參數化資料列篩選器。  
  
#### 針對合併式發行集中的發行項定義參數化資料列篩選器  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定 **@publication**, ，發行項的名稱 **@article**, 、 發行的資料表 **@source_object**, ，定義參數化的篩選的 WHERE 子句 **@subset_filterclause** (不包括 `WHERE`)，以及下列其中一個值 **@partition_options**, ，用來描述資料分割的類型會因參數化資料列篩選器︰  
  
    -   **0** -發行項是靜態或不會產生唯一的每個資料分割 （「 重疊 」 的磁碟分割） 的資料子集的篩選。  
  
    -   **1** -產生的資料分割重疊，並更新 「 訂閱者 」 無法變更資料列所屬的資料分割。  
  
    -   **2** -發行項的篩選會產生非重疊資料分割，但多個訂閱者可以接收相同的資料分割。  
  
    -   **3** -篩選發行項會產生非重疊資料分割都是唯一的每個訂閱。  
  
#### 針對合併式發行集中的發行項變更參數化資料列篩選器  
  
1.  在發行集資料庫的發行者，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定 **@publication**, ，**@article**, ，值為 **subset_filterclause** 的 **@property**, ，定義參數化的篩選的運算式 **@value** (不包括 `WHERE`)，而值為 **1** 兩者 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**。  
  
2.  如果這項變更會導致不同的資料分割行為，然後執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 一次。 指定 **@publication**, ，**@article**, ，值為 **partition_options** 的 **@property**, ，和最適當的資料分割選項，如 **@value**, ，它可以是下列其中之一︰  
  
    -   **0** -發行項是靜態或不會產生唯一的每個資料分割 （「 重疊 」 的磁碟分割） 的資料子集的篩選。  
  
    -   **1** -產生的資料分割重疊，並更新 「 訂閱者 」 無法變更資料列所屬的資料分割。  
  
    -   **2** -發行項的篩選會產生非重疊資料分割，但多個訂閱者可以接收相同的資料分割。  
  
    -   **3** -篩選發行項會產生非重疊資料分割都是唯一的每個訂閱。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 這個範例會使用一系列的聯結篩選來針對已篩選發行項的合併式發行集中定義一組發行 `Employee` 也就是資料表本身上使用參數化資料列篩選進行篩選 **LoginID** 資料行。 同步處理期間，傳回的值 [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) 函式會覆寫。 如需詳細資訊，請參閱覆寫 host_name （） 值 > 主題中 [參數化資料列篩選](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-para_1.sql)]  
  
## 另請參閱  
 [定義和修改合併發行項之間的聯結篩選](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [聯結篩選](../../../relational-databases/replication/merge/join-filters.md)   
 [參數化資料列篩選器](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  