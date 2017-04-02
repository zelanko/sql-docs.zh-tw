---
title: "發行項 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.articles.f1"
ms.assetid: 7c743dc6-6c6d-4c92-b711-842e1b0b273e
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# 發行項
  在 **文章** 頁面上，指定要為發行集中發行項包含資料庫物件。 如果您發行的資料庫物件相依於一或多個其他資料庫物件，就必須發行所有參考物件。 例如，如果您發行相依於資料表的檢視表，同時也必須發行該資料表。  
  
 無法發行的物件旁邊會有一個紅色的圖示，且精靈頁面底部的資訊面板中會顯示說明。 下列物件無法發行：  
  
-   加密的物件。  
  
-   沒有主索引鍵的資料表，無法在交易式發行集內發行。  
  
-   資料表無法同時發行到合併式發行集以及啟用佇列更新訂閱的交易式發行集。 如需在多個發行集中發行發行項的詳細資訊，請參閱 」 中超過一個發行集中發行資料表 」 一節 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
## Oracle 發行者  
 Oracle 發行者有其他的注意事項：  
  
-   可以從 Oracle 發行之物件的清單，請參閱 [設計考量和限制的 Oracle 發行者](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)。 無法發行的物件不會顯示。  
  
-   如需可以發行的資料類型的清單，請參閱 [Oracle 發行者的資料類型對應](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)。 具有無法發行之資料類型的資料行不會顯示。  
  
## 資料行篩選  
 展開的資料表中篩選這個頁面上的資料行 **發行的物件** 窗格，然後選取 [需要的資料行 (資料列可以篩選在 **篩選資料表資料列** 此精靈的頁面)。 資料行的篩選功能有很多優點，包括安全性 (可防止機密資料被複寫) 和效能 (例如可避免複寫大型二進位大型物件 (BLOB) 資料行)。 如需有關資料行篩選，包括無法篩選的資料行類型的清單，請參閱 [篩選已發佈資料](../../relational-databases/replication/publish/filter-published-data.md)。  
  
## 選項  
  **發行的物件** 窗格可讓您︰  
  
-   檢視所有可以複寫的物件。  
  
-   選取某個物件旁的核取方塊，將該物件加入發行集。  
  
-   在物件類型的發行集選取旁邊的核取方塊中包含特定的型別 （例如資料表） 的所有物件 (例如 **資料表**)。  
  
-   展開資料表節點，以查看資料表中的資料行。  
  
-   清除某資料行旁的核取方塊，篩選出資料表資料行，將其排除在發行集之外。  
  
-   以滑鼠右鍵按一下窗格中的物件，以查看該物件的命令功能表。  
  
 **發行項屬性**  
 按一下 [ **發行項屬性**, ，然後按一下下列其中之一︰  
  
-   按一下 [ **設定的反白顯示屬性 \< ObjectType> 文章** 啟動 **發行項屬性-\< ObjectName>** ] 對話方塊中，屬性在此對話方塊中所做的變更只會套用到的物件，會在 [物件] 窗格上反白顯示 **文章** 頁面。  
  
-   按一下 [ **設定屬性的所有 \< ObjectType> 文章**, ，以啟動 **所有屬性 \< ObjectType> 文章** ] 對話方塊中，屬性在此對話方塊中所做的變更套用至該類型的物件] 窗格的所有物件上 **文章** ] 頁面上，包括尚未選取 [發行集。  
  
    > [!NOTE]  
    >  屬性中所做的變更 **所有屬性 \< ObjectType> 文章** 對話方塊覆寫任何先前所做的 **發行項屬性-\< o b j>** 對話方塊。 例如，若要設定所有屬於某物件類型之發行項的一些預設值，但同時要設定個別物件的某些屬性，則請先設定所有發行項的預設值， 然後再設定個別物件的屬性。  
  
 **反白的資料表僅限下載**  
 僅限合併式複寫。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 選取以指定如果使用客訂閱，則訂閱者端不允許變更。 因為僅限下載的發行項不能在訂閱者端進行更新，追蹤中繼資料不會傳送給訂閱者。 如此可減少訂閱者上的儲存體並提高效能，特別是網路連接緩慢時。 此選項對應到值為 **-僅限下載至訂閱者，禁止訂閱者變更** 選項 **同步處理方向** 中 **發行項屬性** 對話方塊。 如需詳細資訊，請參閱 [最佳化合併式複寫效能的 「 文章](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
 **僅顯示清單中已核取的物件**  
 選取這個核取方塊，就只會顯示在物件窗格中選取的發行項。  
  
## 另請參閱  
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
  