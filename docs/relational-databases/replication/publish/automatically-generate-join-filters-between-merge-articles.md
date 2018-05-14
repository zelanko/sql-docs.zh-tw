---
title: 在合併發行項之間自動產生聯結篩選 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- automatic join filter generation
- join filters
ms.assetid: 7ef419f4-c17f-42a5-9068-174a3ec08941
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70fc107aab8433822e5d674b39b8b4986ec32f4e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="automatically-generate-join-filters-between-merge-articles"></a>在合併發行項之間自動產生聯結篩選
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<發行集>] 對話方塊的 [篩選資料列] 頁面上，自動產生一組聯結篩選。 如需使用精靈及存取對話方塊的詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)和[檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
> [!NOTE]  
>  如果在初始化發行集的訂閱之後，在 [發行集屬性 - \<發行集>] 對話方塊中自動產生了一組聯結篩選，則您必須在經過變更之後，產生一個新的快照集並重新初始化所有的訂閱。 如需屬性變更需求的詳細資訊，請參閱[變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
 可以為一組資料表手動建立聯結篩選，或根據資料表中定義之主索引鍵關聯性的外部索引鍵，複寫可以自動產生篩選。 如需手動建立聯結篩選的詳細資訊，請參閱[定義和修改合併發行項之間的聯結篩選](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
### <a name="to-automatically-generate-a-set-of-join-filters-between-merge-articles"></a>若要在合併發行項之間自動產生一組聯結篩選  
  
1.  在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<發行集>] 的 [篩選資料列] 頁面上，按一下 [新增]，然後按一下 [自動產生篩選]。  
  
    > [!NOTE]  
    >  自動產生篩選會刪除發行集中任何現有的資料列篩選或聯結篩選。 您可以在自動產生一組篩選之後加入篩選。  
  
2.  遵循 **[產生篩選]** 對話方塊中的處理建立資料列篩選。 資料列篩選隨後會透過主索引鍵和外部索引鍵的關聯性擴充到與已篩選資料表相關的資料表。  
  
    1.  從下拉式清單方塊中選取要篩選的資料表。  
  
    2.  在 **[篩選陳述式]** 文字方塊中建立篩選陳述式。 您可直接在文字區域輸入，也可以從 **[資料行]** 清單方塊中拖曳資料行。  
  
         **[篩選陳述式]** 文字區域包括預設文字，其格式為：  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
         預設文字無法變更；使用標準 SQL 語法在 WHERE 關鍵字之後，為靜態資料列篩選或參數化資料列篩選器輸入篩選子句。 參數化資料列篩選器的完整篩選子句類似於：  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         WHERE 子句應使用兩部份命名；不支援三部份及四部份命名。  
  
    3.  指定篩選選項。  
  
         選取符合在「訂閱者」之間共用資料方式的選項： **[這個資料表中的一個資料列會提供給多個訂閱]** 或 **[這個資料表中的一個資料列只會提供給一個訂閱]**。 若您選取 **[這個資料表中的一個資料列只會提供給一個訂閱]**，合併式複寫可藉由儲存和處理較少中繼資料來將效能最佳化。 不過您必須確定資料分割方式不會將資料列複寫至多個訂閱者。 如需進一步資訊，請參閱主題＜ [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞中的「設定資料分割選項」。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     您指定的篩選會被剖析，並會針對 SELECT 子句中的資料表執行。 如果篩選陳述式包含語法錯誤或其他問題，則系統會通知您，然後您可以編輯該篩選陳述式。  
  
     剖析陳述式之後，複寫會建立必要的聯結篩選，並在 **[篩選資料表的資料列]** 或 **[篩選資料列]** 頁面上的 **[已篩選的資料表]** 窗格中顯示它們。 如果您從「新增發行集精靈」產生篩選，且尚未針對此精靈執行的「發行者」設定「散發者」，您會被提示要進行設定。  
  
4.  如果您在 [發行集屬性 - \<發行集>] 對話方塊中，請按一下 [確定] 以儲存並關閉對話方塊。  
  
### <a name="to-modify-a-filter-that-was-automatically-generated"></a>若要修改自動產生的篩選  
  
1.  在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<發行集>] 的 [篩選資料列] 頁面上，從 [已篩選的資料表] 窗格中選取一個篩選，然後按一下 [編輯]。  
  
2.  在 **[編輯篩選]** 或 **[編輯聯結]** 對話方塊中修改篩選。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-filter-that-was-automatically-generated"></a>若要刪除自動產生的篩選  
  
1.  在 [新增發行集精靈] 的 [篩選資料表的資料列] 頁面上，或是在 [發行集屬性 - \<發行集>] 的 [篩選資料列] 頁面上，從 [已篩選的資料表] 窗格中選取一個篩選，然後按一下 [刪除]。  
  
## <a name="see-also"></a>另請參閱  
 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
