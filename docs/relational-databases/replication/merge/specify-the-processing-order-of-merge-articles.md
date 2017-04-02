---
title: "指定合併發行項的處理順序 | Microsoft Docs"
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
  - "發行項 [SQL Server 複寫], 處理順序"
  - "合併式複寫 [SQL Server 複寫], 發行項處理順序"
ms.assetid: d151e2c5-cf50-4cb3-a829-8f32455dbd66
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 指定合併發行項的處理順序
  開頭為 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], ，就可以覆寫處理合併式發行集的發行項的預設順序。 這非常有用，例如，如果您透過觸發程序定義參考完整性，並且那些觸發程序必須以特定順序引發。  
  
 **若要指定發行項處理順序**  
  
-   複寫 TRANSACT-SQL 程式設計︰ [指定在處理順序的合併資料表發行項 & #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/publish/specify the processing order of merge table articles.md)  
  
## 如何確定處理順序  
 在合併同步處理期間，依預設，發行項將按物件間相依性所需的順序處理，包括在基底資料表上定義的宣告式參考完整性 (DRI) 條件約束。 處理包括列舉對資料表所作的變更，然後套用這些變更。 如果沒有 DRI，但資料表發行項之間存在聯結篩選或邏輯記錄，發行項將以篩選和邏輯記錄所需的順序處理。 文件無關透過 DRI、 任何其他發行項聯結篩選、 邏輯記錄或其他相依性的處理方式中發行項暱稱 [sysmergearticles & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-tables/sysmergearticles-transact-sql.md) 系統資料表。  
  
 包含資料表的發行集，請考慮 **SalesOrderHeader** 和 **SalesOrderDetail** 主索引鍵資料行 **SalesOrderID** 中 **SalesOrderHeader** 資料表和對應外部索引鍵資料行 **SalesOrderID** 中 **SalesOrderDetail** 資料表。 合併式複寫同步處理期間，藉由插入任何新的資料列，以防止外部索引鍵違規 **SalesOrderHeader** 之前插入相關聯的資料列中 **SalesOrderDetail**。 同樣地，刪除資料列從 **SalesOrderDetail** 相關聯的資料列會從刪除之前 **SalesOrderHeader**。  
  
 但是，在某些應用程式中，參照完整性透過資料庫觸發程序強化，或使用應用程式層級而不是透過 DRI 來強化。 指定發行集而不是 DRI，上述步驟 **SalesOrderDetail** 資料表可能會有 insert 觸發程序，以確保在相關聯的資料列 **SalesOrderHeader** 允許插入前存在的資料表。 **SalesOrderHeader** 有 delete 觸發程序，以確保沒有相關聯的資料列中 **SalesOrderDetail** 允許刪除前。 合併式複寫在確定發行項處理順序時，不會考慮觸發程序，因為它無法在引發觸發程序前確定其結果。 同樣地，複寫不會考慮在應用程式層級上定義的條件約束。  
  
 當透過觸發程序或在應用程式層級上維護參考完整性時，您應該指定處理發行項的順序。 在觸發程序的範例中，您應該指定 **SalesOrderHeader** 資料表之前處理 **SalesOrderDetail**, ，因為發行項排序根據插入順序。 合併式複寫將自動反轉刪除順序。 沒有發行項排序，合併式複寫也不會失敗，因為如果條件約束出現違規，「合併代理程式」會繼續處理發行項；然後重試在處理其他發行項後失敗的任何作業。 只需指定發行項順序即可避免重試以及與其相關的其他處理。 如果您指定了錯誤順序 (例如，導致在標頭記錄前處理詳細記錄的順序)，合併式複寫將會重試處理，直到它成功。  
  
## 另請參閱  
 [合併式複寫的發行項選項](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [使用邏輯記錄分組相關資料列的變更](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)   
 [聯結篩選](../../../relational-databases/replication/merge/join-filters.md)  
  
  