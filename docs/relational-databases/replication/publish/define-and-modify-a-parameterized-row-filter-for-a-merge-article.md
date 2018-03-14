---
title: "針對合併發行項定義及修改參數化資料列篩選 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameterized filters [SQL Server replication], defining
- parameterized filters [SQL Server replication], modifying
- merge replication [SQL Server replication], dynamic filters
- merge replication parameterized filters [SQL Server replication]
- filters [SQL Server replication], parameterized
- modifying filters, parameterized row
- dynamic filters [SQL Server replication]
ms.assetid: de0482a2-3cc8-4030-8a4a-14364549ac9f
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 25e02f17df0a17ac500eb4549f564b1b1f5f6200
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="define-and-modify-a-parameterized-row-filter-for-a-merge-article"></a>針對合併發行項定義及修改參數化資料列篩選
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中定義及修改參數化資料列篩選。  
  
 在建立資料表發行項時，您可以使用參數化資料列篩選器。 這些篩選器會使用 [WHERE](../../../t-sql/queries/where-transact-sql.md) 子句來選取要發行的適當資料。 您可以指定下列系統函數的其中之一或兩者，而不要在子句中指定常值 (如同處理靜態資料列篩選)： [SUSER_SNAME](../../../t-sql/functions/suser-sname-transact-sql.md) 和 [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md)。 如需詳細資訊，請參閱＜ [參數化資料列篩選器](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要定義及修改參數化資料列篩選，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果您在初始化發行集的訂閱後，新增、修改或刪除參數化資料列篩選，則必須在進行變更後產生新的快照集並重新初始化所有訂閱。 如需屬性變更需求的詳細資訊，請參閱[變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
###  <a name="Recommendations"></a> 建議  
  
-   基於效能的考量，我們建議您不要在參數化資料列篩選器子句中，將函數套用至資料行名稱上，如 `LEFT([MyColumn]) = SUSER_SNAME()`。 如果在篩選子句中使用 HOST_NAME，並且覆寫 HOST_NAME 值，則可能需要使用 CONVERT 來轉換資料類型。 如需有關此案例之最佳做法的詳細資訊，請參閱主題＜ [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞中的「覆寫 HOST_NAME() 值」一節。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 您可以在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<發行集>] 對話方塊的 [篩選資料列] 頁面上，定義、修改及刪除參數化資料列篩選。 如需使用精靈及存取對話方塊的詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)和[檢視及修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### <a name="to-define-a-parameterized-row-filter"></a>若要定義參數化資料列篩選器  
  
1.  在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<發行集>] 的 [篩選資料列] 頁面上，按一下 [加入]，然後按一下 [加入篩選]。  
  
2.  在 **[加入篩選]** 對話方塊中，從下拉式清單方塊中選取要篩選的資料表。  
  
3.  在 **[篩選陳述式]** 文字方塊中建立篩選陳述式。 您可直接在文字區域輸入，也可以從 **[資料行]** 清單方塊中拖曳資料行。  
  
    -   **[篩選陳述式]** 文字區域包括預設文字，其格式為：  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
    -   預設的文字無法變更；使用標準 SQL 語法，在 WHERE 關鍵字後面輸入篩選子句。 參數化篩選包括對系統函數 **HOST_NAME()** 與/或 **SUSER_SNAME()**的呼叫，或參考上述一或兩個函數的使用者定義函數。 下列為參數化資料列篩選器的完整篩選子句範例：  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         WHERE 子句應使用兩部份命名；不支援三部份及四部份命名。  
  
4.  選取符合資料在訂閱者之間共用資料方式的選項：  
  
    -   **這個資料表中的一個資料列會提供給多個訂閱**  
  
    -   **這個資料表中的一個資料列只會提供給一個訂閱**  
  
     若您選取 **[這個資料表中的一個資料列只會提供給一個訂閱]**，合併式複寫可藉由儲存和處理較少中繼資料來將效能最佳化。 不過您必須確定資料分割方式不會將資料列複寫至多個訂閱者。 如需進一步資訊，請參閱主題＜ [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞中的「設定資料分割選項」。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  如果您在 [發行集屬性 - \<發行集>] 對話方塊中，請按一下 [確定] 以儲存並關閉對話方塊。  
  
#### <a name="to-modify-a-parameterized-row-filter"></a>若要修改參數化資料列篩選器  
  
1.  在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<發行集>]的 [篩選資料列] 頁面上，從 [已篩選的資料表] 窗格中選取一個篩選，然後按一下 [編輯]。  
  
2.  在 **[編輯篩選]** 對話方塊中，修改篩選。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-parameterized-row-filter"></a>若要刪除參數化資料列篩選器  
  
1.  在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<發行集>]的 [篩選資料列] 頁面上，從 [已篩選的資料表] 窗格中選取一個篩選，然後按一下 [刪除]。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式建立及修改參數化資料列篩選器。  
  
#### <a name="to-define-a-parameterized-row-filter-for-an-article-in-a-merge-publication"></a>針對合併式發行集中的發行項定義參數化資料列篩選器  
  
1.  在發行集資料庫的發行者端，執行 [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定 **@publication**、針對 **@article**指定發行項的名稱、針對 **@source_object**指定發行的資料表、針對 **@subset_filterclause** (不包括 `WHERE`) 指定定義參數化篩選器的 WHERE 子句，以及針對 **@partition_options**(用來描述從參數化資料列篩選器產生的資料分割類型) 指定下列其中一個值：  
  
    -   **0** - 發行項的篩選是靜態的，或是不產生每個資料分割的唯一資料子集 (也就是「重疊」的資料分割)。  
  
    -   **1** - 產生的資料分割是重疊的，而且在訂閱者上進行的更新並不會變更資料列所屬的資料分割。  
  
    -   **2** - 發行項的篩選會產生非重疊的資料分割，但多個訂閱者可以接收相同的資料分割。  
  
    -   **3** - 發行項的篩選會產生對每項訂閱而言都是唯一的非重疊資料分割。  
  
#### <a name="to-change-a-parameterized-row-filter-for-an-article-in-a-merge-publication"></a>針對合併式發行集中的發行項變更參數化資料列篩選器  
  
1.  在發行集資料庫的發行者上，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定 **@publication**、指定 **@article**、針對 **@property** @property **@property**值、針對 **@value** (不包括 `WHERE`) 指定定義參數化篩選器的運算式、針對 **1** 和 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**中定義及修改參數化資料列篩選。  
  
2.  如果此變更會產生不同的資料分割行為，則再次執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 。 指定 **@publication**、指定 **@article**、針對 **@property** @property **@property**的值，以及針對 **@value**指定最適當的資料分割選項，可以是下列其中一項：  
  
    -   **0** - 發行項的篩選是靜態的，或是不產生每個資料分割的唯一資料子集 (也就是「重疊」的資料分割)。  
  
    -   **1** - 產生的資料分割是重疊的，而且在訂閱者上進行的更新並不會變更資料列所屬的資料分割。  
  
    -   **2** - 發行項的篩選會產生非重疊的資料分割，但多個訂閱者可以接收相同的資料分割。  
  
    -   **3** - 發行項的篩選會產生對每項訂閱而言都是唯一的非重疊資料分割。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會在合併式發行集中定義一組發行項，其中的發行項會使用一系列的聯結篩選來針對 `Employee` 資料表進行篩選 (此資料表本身是使用 **LoginID** 資料行上的參數化資料列篩選來進行篩選)。 在同步處理期間，會覆寫 [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) 函數傳回的值。 如需詳細資訊，請參閱＜ [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞主題中的「覆寫 HOST_NAME() 值」。  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-para_1.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
