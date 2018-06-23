---
title: 定義和修改合併發行項之間的聯結篩選| Microsoft 文件
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- filters [SQL Server replication], join
- merge replication join filters [SQL Server replication]
- modifying filters, join
- join filters
ms.assetid: f7f23415-43ff-40f5-b3e0-0be1d148ee5b
caps.latest.revision: 45
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: dad83104b83a3d26e204b0ebf8d873dcf2bec975
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146721"
---
# <a name="define-and-modify-a-join-filter-between-merge-articles"></a>定義和修改合併發行項之間的聯結篩選
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中定義及修改合併發行項之間的聯結篩選。 合併式複寫支援聯結篩選，聯結篩選通常會配合參數化篩選一起使用，以將資料表資料分割擴充到其他相關的資料表發行項。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
-   **若要定義和修改合併發行項之間的聯結篩選，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   若要建立聯結篩選，發行集至少必須包含兩個相關的資料表。 聯結篩選會擴充資料列篩選；因此您必須先定義一個資料表上的資料列篩選，然後才可利用聯結在另一個資料表上擴充篩選。 定義好一個聯結篩選後，如果發行集包含其他相關資料表，您可以用另一個聯結篩選擴充這個聯結篩選。  
  
-   如果您在初始化發行集的訂閱後，新增、修改或刪除聯結篩選，則必須在進行變更後產生新的快照集並重新初始化所有訂閱。 如需屬性變更需求的詳細資訊，請參閱[變更發行集與發行項屬性](change-publication-and-article-properties.md)。  
  
###  <a name="Recommendations"></a> 建議  
  
-   可以為一組資料表手動建立聯結篩選，或者根據資料表中定義的外部索引鍵與主索引鍵之間的關聯性自動產生篩選。 如需自動產生一組聯結篩選的詳細資訊，請參閱[在合併發行項之間自動產生一組聯結篩選 &#40;SQL Server Management Studio&#41;](automatically-generate-join-filters-between-merge-articles.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 您可以在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<發行集>] 對話方塊的 [篩選資料列] 頁面上，定義、修改及刪除聯結篩選。 如需使用精靈及存取對話方塊的詳細資訊，請參閱[建立發行集](create-a-publication.md)和[檢視及修改發行集屬性](view-and-modify-publication-properties.md)。  
  
#### <a name="to-define-a-join-filter"></a>若要定義聯結篩選  
  
1.  在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<發行集>] 對話方塊的 [篩選資料列] 頁面上，從 [已篩選的資料表] 窗格中選取一個現有的資料列篩選或聯結篩選。  
  
2.  按一下 **[加入]**，然後按一下 **[加入聯結以擴充選取的篩選]**。  
  
3.  建立聯結陳述式：選取 [使用產生器建立陳述式]  或 [手動寫入 join 陳述式] 。  
  
    -   如果選取使用產生器，請使用方格中的資料行 ([結合]、[已篩選的資料表資料行] 、[運算子] 和 [聯結的資料表資料行] ) 來建立聯結陳述式。  
  
         方格中的每個資料行都包含下拉式方塊，可讓您選取兩個資料行和一個運算子 (**=**、[已篩選的資料表資料行] **<>**、[已篩選的資料表資料行] **<=**、[已篩選的資料表資料行] **\<**、[已篩選的資料表資料行] **>=**、[已篩選的資料表資料行] **>** 和 [聯結的資料表資料行] **like**)。 結果會在 **[預覽]** 文字區域中顯示。 如果聯結涉及多對資料行，請從 **[結合]** 資料行中選取一個結合 (AND 或 OR)，然後輸入兩個或更多的資料行及一個運算子。  
  
    -   如果選取手動寫入陳述式，請在 **[聯結陳述式]** 文字區域寫入聯結陳述式。 使用 **[已篩選的資料表資料行]** 清單方塊與 **[聯結的資料表資料行]** 清單方塊將資料行拖放到 **[Join 陳述式]** 文字區域。  
  
    -   完整的聯結陳述式應類似於：  
  
        ```  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] INNER JOIN [Sales].[SalesOrderDetail] ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID]  
        ```  
  
         JOIN 子句應該使用兩段式命名；不支援三段式和四段式命名。  
  
4.  指定聯結選項：  
  
    -   如果在篩選的資料表 (父系資料表) 中聯結的資料行是唯一的，請選擇 **[唯一索引鍵]**。  
  
        > [!CAUTION]  
        >  選取此選項表示聯結篩選中的子資料表與父資料表之間的關聯性是一對一或一對多。 如果在子系資料表中的聯結資料行有保證唯一性的條件約束，請僅選取此選項。 如果選項設定不正確，則資料可能發生非聚合的情況。  
  
    -   依預設，合併式複寫在同步處理過程中會按逐個資料列的方式處理變更。 若要將篩選資料表及聯結資料表之資料列中的相關變更做為一個單位進行處理，請選取 **[邏輯記錄]** ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 及更新版本)。 只有當發行項與發行集之使用邏輯記錄的需求均符合時，才可以使用此選項。 如需詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../merge/group-changes-to-related-rows-with-logical-records.md)中的＜使用邏輯記錄的考量＞一節。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  如果您在 [發行集屬性 - \<發行集>] 對話方塊中，請按一下 [確定] 以儲存並關閉對話方塊。  
  
#### <a name="to-modify-a-join-filter"></a>若要修改聯結篩選  
  
1.  在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<發行集>]的 [篩選資料列] 頁面上，從 [已篩選的資料表] 窗格中選取一個篩選，然後按一下 [編輯]。  
  
2.  在 **[編輯聯結]** 對話方塊中，修改篩選。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-join-filter"></a>若要刪除聯結篩選  
  
1.  在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<發行集>]的 [篩選資料列] 頁面上，從 [已篩選的資料表] 窗格中選取一個篩選，然後按一下 [刪除]。 如果您刪除的聯結篩選本身已由其他聯結擴充，也會一併刪除這些聯結。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 這些程序顯示父發行項上的參數化篩選，其中包含此發行項與相關子發行項之間的聯結篩選。 您可以使用複寫預存程序來以程式設計的方式定義及修改聯結篩選。  
  
#### <a name="to-define-a-join-filter-to-extend-an-article-filter-to-related-articles-in-a-merge-publication"></a>定義聯結篩選，將發行項擴充到合併式發行集中的相關發行項  
  
1.  針對聯結的發行項定義篩選，此發行項也稱為父發行項。  
  
    -   如需使用參數化資料列篩選器篩選的發行項，請參閱＜ [針對合併發行項定義及修改參數化資料列篩選](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)＞。  
  
    -   如需使用靜態資料列篩選進行篩選的發行項，請參閱＜ [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md)＞。  
  
2.  在發行集資料庫的發行者端，執行 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 來針對發行集定義一個或多個相關發行項，這些發行項也稱為子發行項。 如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
3.  在發行集資料庫的發行者端，執行 [sp_addmergefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql)。 指定 **@publication**、針對 **@filtername**指定此篩選的唯一名稱、針對 **@article**指定步驟 2 中建立的子發行項名稱、針對 **@join_articlename**指定聯結的父發行項名稱，以及針對 **@join_unique_key**指定下列其中一個值：  
  
    -   **0** - 指示父發行項與子發行項之間的多對一或多對多的聯結。  
  
    -   **1** - 指示父發行項與子發行項之間的一對一或一對多的聯結。  
  
     這樣會定義兩個發行項之間的聯結篩選。  
  
    > [!CAUTION]  
    >  只有當保證唯一性的父發行項之基礎資料表中的聯結資料行上有條件約束時，才能將 **@join_unique_key** 設為 **1** 。 如果將 **@join_unique_key** 錯誤地設定為 **1** ，可能會發生資料無法聚合。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 這個範例會針對合併式發行集定義發行項，其中會針對 `SalesOrderDetail` 資料表篩選 `SalesOrderHeader` 資料表發行項 (前者資料表本身會使用靜態資料列篩選來進行篩選)。 如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md)。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepub.sql#sp_addmergearticle)]  
  
 此範例會在合併式發行集中定義一組發行項，其中的發行項會使用一系列的聯結篩選來針對 `Employee` 資料表進行篩選 (此資料表本身是使用 [LoginID](/sql/t-sql/functions/host-name-transact-sql) 資料行中 **HOST_NAME** 值上的參數化資料列篩選來進行篩選)。 如需詳細資訊，請參閱 [針對合併發行項定義及修改參數化資料列篩選](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubdynamic1.sql#sp_mergedynamicpub1)]  
  
## <a name="see-also"></a>另請參閱  
 [聯結篩選](../merge/join-filters.md)   
 [參數化資料列篩選器](../merge/parameterized-filters-parameterized-row-filters.md)   
 [變更發行集與發行項屬性](change-publication-and-article-properties.md)   
 [針對合併式複寫篩選發行的資料](../merge/filter-published-data-for-merge-replication.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [定義合併資料表發行項之間的邏輯記錄關聯性](define-a-logical-record-relationship-between-merge-table-articles.md)   
 [針對合併發行項定義及修改參數化資料列篩選](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
  
