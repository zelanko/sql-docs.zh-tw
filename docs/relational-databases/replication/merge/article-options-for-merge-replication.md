---
title: "合併式複寫的發行項選項 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "合併式複寫 [SQL Server 複寫], 發行項選項"
  - "發行項 [SQL Server 複寫]、合併複寫選項"
ms.assetid: 670abd41-d204-4cd7-a371-7664e603a0ce
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 合併式複寫的發行項選項
  合併資料表發行項有許多選項，可讓您自訂複寫行為以適應應用程式的需要。 使用合併式複寫，您可以執行下列項目：  
  
-   使用資料列篩選、聯結篩選和資料行篩選。 篩選資料表發行項可讓您建立即將發行的資料分割。 如需詳細資訊，請參閱 [篩選已發佈資料](../../../relational-databases/replication/publish/filter-published-data.md)。  
  
-   指定「訂閱者」端的變更是否上傳到「發行者」。 對於部份或所有資料在「訂閱者」端應為唯讀的應用程式，僅限下載的發行項可提供效能優勢。 如需詳細資訊，請參閱 [最佳化合併式複寫效能的 「 文章](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
-   指定複寫觸發程序和系統資料表不應追蹤對於一個或多個發行項所作的刪除。 這個選項在許多應用程式案例中可能很有用處。 這些包括使用不需要複寫之批次刪除的案例。 如需詳細資訊，請參閱 [最佳化合併式複寫效能 with Conditional Delete Tracking](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)。  
  
-   指定發行項的處理順序，以確定發行項是以應用程式需要的順序進行處理。 如需詳細資訊，請參閱 [指定處理順序合併發行項的](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)。  
  
-   指定一組相關記錄應視為一個單位處理 (依預設，合併式複寫會以逐個資料列的方式處理資料表的變更)。 如需詳細資訊，請參閱 [使用邏輯記錄的相關資料列群組變更](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
-   對可以在拓撲的多個節點上變更相同資料之案例，使用衝突偵測和解決方案。 如需相關資訊，請參閱 [Detect and Resolve Merge Replication Conflicts](../../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md)。  
  
-   指定結構描述選項，如條件約束和觸發程序是否複製到訂閱者。 如需詳細資訊，請參閱 [指定結構描述選項](../../../relational-databases/replication/publish/specify-schema-options.md)。  
  
-   使用商務邏輯處理常式，以便在同步處理期間回應許多狀況。 這些包括資料變更、衝突和錯誤。 如需詳細資訊，請參閱 [執行商務邏輯合併同步處理期間](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)。  
  
## 另請參閱  
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  