---
title: "發行集屬性，篩選資料列 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.pubproperties.filterrows.f1
ms.assetid: 2c5fdbed-9b10-4818-98cc-cc6b01351318
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 30b632ee39ae16233a66ef4985ce018e0ef8b9d7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="publication-properties-filter-rows"></a>發行集屬性，篩選資料列
  **[發行集屬性]** 對話方塊的 **[篩選資料列]** 頁面，可以讓您進行加入、編輯或刪除：  
  
-   將靜態資料列篩選套用至快照集式、交易式和合併式發行集的資料表發行項。  
  
-   將參數化資料列篩選器套用至合併式發行集的資料表發行項。  
  
-   使用聯結篩選，將合併資料表發行項的篩選擴充到相關的資料表發行項。  
  
 如需篩選選項的詳細資訊，請參閱[篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)。  
  
> [!NOTE]  
>  需要有發行集的新快照集，而且要重新初始化所有訂閱，才能加入、編輯或刪除篩選。  
  
 若要使應用程式效能最佳化，並減少需要的遠端儲存體數量，或限制特定訂閱者對特定資料的存取，您就應該只發行需要的資料。 發行集可同時包括未篩選和已篩選的資料表。 例如，您可以包括公司產品的完整 (未篩選) 資料表，並使用資料列篩選來提供已篩選過、僅包含特定區域之客戶的資料表。 利用篩選發行的資料，您可以：  
  
-   將透過網路傳送的資料總量縮減到最少。  
  
-   降低訂閱者端所需的儲存空間量。  
  
-   依照個別的訂閱者需求，自訂發行集和應用程式。  
  
-   可以避免或減少訂閱者更新資料時的衝突，因為不同資料分割可以傳送給不同的訂閱者 (不會有兩個訂閱者同時更新相同的資料值)。  
  
-   避免傳送機密資料。 資料列篩選與資料行篩選可用於限制訂閱者對資料的存取。 對於合併式複寫，如果使用含有 HOST_NAME() 的參數化篩選，則有安全性考量。 如需詳細資訊，請參閱＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞中的「使用 HOST_NAME() 進行篩選」一節。  
  
## <a name="options"></a>選項  
 **已篩選的資料表**  
 當您在發行集的資料表發行項中加入篩選時，這些篩選就會擴展到窗格中。 含有資料列篩選的資料表，會顯示為窗格中的最上層節點。 若為合併式發行集，則透過聯結篩選而擴充篩選的資料表，就會顯示為子節點。  
  
 **加入**  
 按一下 **[加入]** 即可啟動一個可讓您篩選資料表發行項的對話方塊。 在快照集或交易式發行集按一下 **[加入]** 會立即啟動對話方塊。 針對合併式發行集按一下 **[加入]** ，就會顯示三個選項： **[加入篩選]**、 **[加入聯結以擴充選取的篩選]**和 **[自動產生篩選]**。  
  
-   選取 **[加入篩選]** 即可啟動 **[加入篩選]** 對話方塊。 這個對話方塊可以讓您套用資料列篩選至資料表發行項。 例如，在 **[加入篩選]** 對話方塊中，您可以指定含有客戶資料的資料表在複寫到訂閱者時，只能包含法國客戶的資料。  
  
-   選取 **[加入聯結以擴充選取的篩選]** 即可啟動 **[加入聯結]** 對話方塊。 **[加入聯結]** 對話方塊可以讓您擴充資料列篩選，使它篩選與具有資料列篩選的資料表相關之資料表中的資料。 例如，如果客戶資料表經過篩選後只包含法國客戶的資料，而它有一個包含客戶訂單的相關資料表，那麼您就可以在兩個資料表之間定義聯結，使訂單資料表只包括法國客戶的訂單。  
  
    > [!NOTE]  
    >  唯有當您先在篩選窗格中選取聯結的基底資料表，才能使用此選項。  
  
-   選取 **[自動產生篩選]** 來啟動 **[產生篩選]** 對話方塊。 這個對話方塊可讓您在合併式發行集的一個資料表上定義資料列篩選，複寫時會自動將此篩選擴充到因外部索引鍵關聯性而相關的其他資料表。 例如，發行集可包括 3 個資料表：客戶資料表、訂單資料表 (含有客戶資料表的外部索引鍵) 和訂單明細資料表 (含有訂單資料表的外部索引鍵)。 在客戶資料表上定義資料列篩選，複寫時會將它擴充到其他資料表。  
  
    > [!NOTE]  
    >  當複寫自動產生篩選時，發行集上任何現有的篩選都會被刪除。 若要同時包括自動產生的篩選和手動指定的篩選，請先產生篩選。 您只能對每個發行集指定一個自動產生的篩選集。  
  
 **編輯**  
 在篩選窗格中選取資料列篩選或聯結篩選，再按一下 **[編輯]** ，即可啟動 **[編輯篩選]** 或 **[編輯聯結]** 對話方塊。  
  
 **Delete**  
 在篩選窗格中選取資料列篩選或聯結篩選，再按一下 **[刪除]** 即可刪除篩選。  
  
 **尋找資料表**  
 僅合併式發行集。 按一下 **[尋找資料表]** ，即可在複雜篩選樹中尋找資料表。 在含有複雜關聯性的資料庫中，因為資料表可以聯結到多個資料表，所以資料表可能重複出現在篩選樹的多個位置。  
  
 實際資料表只出現在篩選樹的一個位置，而在其他位置，資料表是以捷徑方式顯示。 資料表的捷徑只是資料表的參考，它不會顯示資料表的子節點。 捷徑節點會以捷徑箭頭標示，展開該節點會顯示這段文字：按一下 [尋找資料表]，以檢視 \<資料表名稱> 的資料表。  
  
 在窗格中選取捷徑節點，然後按一下 **[尋找資料表]** ，窗格就會展開並反白該資料表。 如果您按一下 **[尋找資料表]** 但未選取捷徑節點，則會啟動 **[尋找資料表]** 對話方塊。  
  
 **篩選**  
 包含在篩選窗格中選取之篩選的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 定義。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [檢視和修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)   
 [聯結篩選](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
