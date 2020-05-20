---
title: 發行集屬性，發行項 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.articles.f1
ms.assetid: bdeea318-a153-44b8-9e51-9155f3bad18b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: ee2f59fbb4634cc11bedfa881b1afef071d6dd69
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "76286583"
---
# <a name="publication-properties-articles"></a>發行集屬性，發行項
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[發行集屬性]** 對話方塊的 **[發行項]** 頁面：包含有關發行集內所含發行項的資訊；可讓您將發行項加入至現有的發行集或從現有的發行集卸除發行項；以及可讓您變更發行項屬性和資料行篩選。  
  
> [!NOTE]  
>  建立發行集之後，某些屬性變更需要新的快照集。 如果發行集有訂閱，則某些變更還需要重新初始化所有訂閱。 如需詳細資訊，請參閱[變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)和[在現有發行集中新增和卸除發行項](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
 如果您發行的資料庫物件相依於一或多個其他資料庫物件，就必須發行所有參考物件。 例如，如果您發行相依於資料表的檢視表，同時也必須發行該資料表。  
  
 無法發行的物件旁邊會有一個紅色的圖示，且精靈頁面底部的資訊面板中會顯示說明。 下列物件無法發行：  
  
-   加密的物件。  
  
-   包含允許 NULL 之資料行的索引檢視。  
  
-   沒有主索引鍵的資料表，無法在交易式發行集內發行。  
  
-   資料表無法同時發行到合併式發行集以及啟用佇列更新訂閱的交易式發行集。 如需在多個發行集內發行發行項的詳細資訊，請參閱[發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)的＜在多個發行集內發行資料表＞一節。  
  
## <a name="oracle-publishers"></a>Oracle 發行者  
 Oracle 發行者有其他的注意事項：  
  
-   如需可以從 Oracle 發行之物件的清單，請參閱＜ [Design Considerations and Limitations for Oracle Publishers](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)＞。 無法發行的物件不會顯示。  
  
-   如需可以發行之資料類型的清單，請參閱＜ [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)＞。 具有無法發行之資料類型的資料行不會顯示。  
  
## <a name="column-filters"></a>資料行篩選  
 在 **[發行的物件]** 窗格中展開一個資料表，然後只選取必要的資料行，以篩選這個頁面上的資料行 (資料列可以在這個精靈的 **[篩選資料表的資料列]** 頁面中篩選)。 資料行的篩選功能有很多優點，包括安全性 (可防止機密資料被複寫) 和效能 (例如可避免複寫大型二進位大型物件 (BLOB) 資料行)。 如需資料行篩選的詳細資訊，包括無法篩選的資料行類型清單，請參閱[篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)。  
  
## <a name="options"></a>選項。  
 **[發行的物件]** 窗格可以讓您：  
  
-   檢視所有可以複寫的物件。  
  
-   透過選取該物件旁邊的核取方塊，即可將發行項加入至發行集。  
  
-   透過清除該物件旁邊的核取方塊，即可從發行集卸除發行項。 如需何時可以卸除發行項的資訊，請參閱[在現有發行集中新增和卸除發行項](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
-   選取某物件類型 (例如 **[資料表]** ) 旁的核取方塊，將特定類型 (例如資料表) 的所有物件加入發行集。  
  
-   展開資料表節點，以查看資料表中的資料行。  
  
-   透過清除資料行旁邊的核取方塊來篩選出發行集的資料表資料行，或透過選取核取方塊來包含未發行的資料行。  
  
-   以滑鼠右鍵按一下窗格中的物件，以查看該物件的命令功能表。  
  
 **發行項屬性**  
 按一下 **[發行項屬性]** ，然後按一下下列其中一項：  
  
-   按一下 [設定反白顯示 \<物件類型> 發行項的屬性]  啟動 [發行項屬性 - \<物件名稱>] 對話方塊；在這個對話方塊中所做的屬性變更，只會套用至 [發行項] 頁面的物件窗格中反白顯示的物件。  
  
-   按一下 [設定所有 \<物件類型> 發行項的屬性] 啟動 [所有 \<物件類型> 發行項的屬性] 對話方塊；在這個對話方塊中所做的屬性變更，會套用至 [發行項] 頁面的物件窗格中屬於該類型的所有物件，包括尚未選取發行的物件。  
  
    > [!NOTE]  
    >  在 [所有 \<物件類型> 發行項的屬性] 對話方塊中所做的屬性變更，會覆寫之前在 [發行項屬性 - \<物件名稱>] 對話方塊中所做的任何變更。 例如，若要設定所有屬於某物件類型之發行項的一些預設值，但同時要設定個別物件的某些屬性，則請先設定所有發行項的預設值， 然後再設定個別物件的屬性。  
  
 **反白的資料表僅限下載**  
 僅限合併式複寫。 僅限 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 選取以指定如果使用客訂閱，則訂閱者端不允許變更。 因為僅限下載的發行項不能在訂閱者端進行更新，追蹤中繼資料不會傳送給訂閱者。 如此可減少訂閱者上的儲存體並提高效能，特別是網路連接緩慢時。 此選項對應至 **[發行項屬性]** 對話方塊中， **[同步處理方向]** 選項的 **[僅限下載至訂閱者，禁止訂閱者變更]** 值。 如需詳細資訊，請參閱[使用僅限下載的發行項最佳化合併式複寫效能](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
 **僅顯示清單中已核取的物件**  
 選取這個核取方塊，就只會顯示在物件窗格中選取的發行項。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
