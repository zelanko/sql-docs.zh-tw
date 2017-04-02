---
title: "在現有發行集中加入和卸除發行項 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "發行項 [SQL Server 複寫], 卸除"
  - "刪除發行項"
  - "移除發行項"
  - "卸除發行項"
  - "加入發行項"
  - "管理複寫, 發行項"
  - "發行集 [SQL Server 複寫], 加入和卸除發行項"
  - "發行項 [SQL Server 複寫], 加入"
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
caps.latest.revision: 48
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# 在現有發行集中加入和卸除發行項
  建立發行集後，可以新增或卸除發行項。 發行項可以隨時新增，但卸除發行項所需的動作取決於複寫的類型以及卸除發行項的時機。  
  
## 新增發行項  
 新增發行項涉及的動作包括：在發行集中新增發行項、建立發行集的新快照集、同步處理訂閱以套用新發行項的結構描述和資料。  
  
> [!NOTE]  
>  如果您將發行項加入至合併式發行集現有的發行項新的發行項而定，您必須指定兩個發行項使用的處理順序 **@processing_order** 參數 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 和 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 請考慮下列狀況：您發行資料表但未發行該資料表所參考的函數。 如果您未發行該函數，該資料表就無法在「訂閱者」端建立。 當您將函數加入發行集︰ 指定的值為 **1** 的 **@processing_order** 參數 **sp_addmergearticle**; 並指定其值為 **2** 的 **@processing_order** 參數 **sp_changemergearticle**, ，指定參數的資料表名稱 **@article**。 此處理順序可確保您先在「訂閱者」端建立函數之後才建立相依於此函數的資料表。 您可對每個發行項使用不同的編號，只要函數的編號低於資料表的編號即可。  
  
1.  透過下列方法之一新增一或多個發行項：  
  
    -   [從發行集和 #40; 加入和卸除發行項SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)  
  
2.  新增發行項到發行集後，您必須為發行集 (和所有資料分割，如果該發行集為含參數化篩選的合併式發行集) 建立一個新快照集。 隨後，「散發代理程式」或「合併代理程式」會將新發行項的結構描述和資料複製到「訂閱者」 (不會重新初始化整個發行集)。  
  
    -   若要建立新的快照集，請參閱 [建立和套用初始快照集](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
    -   若要使用參數化篩選建立合併式發行集的新快照集，請參閱 [建立合併式發行集使用參數化篩選的快照集](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
3.  建立快照集後，同步處理訂閱，以複製新發行項的結構描述和資料。  
  
    -   若要同步處理發送訂閱，請參閱 [同步處理發送訂閱](../../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
    -   若要同步處理提取訂閱，請參閱 [同步處理提取訂閱](../../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
## 卸除發行項  
 發行項可以隨時從發行集中卸除，但必須考慮下列行為：  
  
-   從發行集中卸除發行項不會從發行集資料庫中移除物件，或從訂閱資料庫中移除對應物件。 請使用 DROP \< 物件> 移除這些物件。 當您卸除發行項之相關其他已發行的文件，透過外部索引鍵條件約束時，建議您在 「 訂閱者 」 捨棄資料表，以手動方式或使用隨指令碼執行︰ 指定包含適當的卸除指令碼 \< 物件> 陳述式。 如需詳細資訊，請參閱 [執行指令碼同步處理期間 & #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)。  
  
-   如果合併式發行集的相容性層級為 90RTM 或更高，可以隨時卸除發行項，但需要一個新快照集。 此外：  
  
    -   如果發行項是聯結篩選或邏輯記錄關聯性中的父發行項，則必須先卸除此關聯性 (需要重新初始化)。  
  
    -   如果發行項含發行集中的最終參數化篩選，則訂閱必須重新初始化。  
  
-   對於相容性層級低於 90RTM 的合併式發行集，可以在訂閱的初始同步處理之前卸除發行項，無需特殊考量。 如果在同步處理一個或多個訂閱後卸除發行項，則必須卸除、重新建立並同步處理訂閱。  
  
-   對於快照式或交易式發行集，可以在建立訂閱之前卸除發行項，無需特殊考量。 如果在建立一或多個訂閱後卸除發行項，則必須卸除、重新建立並同步處理訂閱。 如需卸除訂閱的詳細資訊，請參閱 [訂閱發行集](../../../relational-databases/replication/subscribe-to-publications.md) 和 [sp_dropsubscription & #40;TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)。 **sp_dropsubscription** 可讓您從訂用帳戶，而非整個訂閱中卸除單一發行項。  
  
1.  從發行集中卸除發行項涉及卸除發行項並建立該發行集的新快照集。 卸除發行項會使目前快照集無效，因此必須建立新快照集。  
  
    -   若要卸除發行集發行，請參閱 [新增和卸除發行項的發行集與 #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md) 或 [刪除發行項](../../../relational-databases/replication/publish/delete-an-article.md)。  
  
2.  從發行集中卸除發行項後，您必須為發行集 (和所有資料分割，如果該發行集為含有參數化篩選的合併式發行集) 建立一個新快照集。  
  
    -   若要建立新的快照集，請參閱 [建立和套用初始快照集](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
    -   若要使用參數化篩選建立合併式發行集的新快照集，請參閱 [建立合併式發行集使用參數化篩選的快照集](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
 如上所提到的，在某些情況下，卸除發行項需要卸除、重新建立並同步處理訂閱。 如需詳細資訊，請參閱 [訂閱發行集](../../../relational-databases/replication/subscribe-to-publications.md) 和 [同步處理資料](../../../relational-databases/replication/synchronize-data.md)。  
  
## 另請參閱  
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)   
 [對發行集資料庫進行結構描述變更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  