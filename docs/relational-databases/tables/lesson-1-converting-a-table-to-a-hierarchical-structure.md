---
title: "第 1 課：將資料表轉換為階層式結構 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "HierarchyID"
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# 第 1 課：將資料表轉換為階層式結構
具有使用自我聯結表達階層式關聯性之資料表的客戶可以使用本課程當做指導方針，將其資料表轉換為階層式結構。 從這種表示法移轉到另一種使用 **hierarchyid**之表示法的步驟非常簡單。 移轉之後，使用者將會有一個精簡而且容易了解的階層式表示法，可以使用數種方式建立索引以便進行有效率的查詢。  
  
本課程會檢查現有的資料表、建立包含 **hierarchyid** 資料行的新資料列、使用來源資料表中的資料擴展資料表，然後示範三個索引策略。 這個課程包含下列主題：  
  
-   [檢查 Employee 資料表的目前結構](../../relational-databases/tables/examining-the-current-structure-of-the-employee-table.md)  
  
-   [使用現有的階層式資料填入資料表](../../relational-databases/tables/populating-a-table-with-existing-hierarchical-data.md)  
  
-   [最佳化 NewOrg 資料表](../../relational-databases/tables/optimizing-the-neworg-table.md)  
  
-   [摘要：將資料表轉換為階層式結構](../../relational-databases/tables/summary-converting-a-table-to-a-hierarchical-structure.md)  
  
## 必要條件  
本課程需要使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫。  
  
## 本課程的下一項工作  
[檢查 Employee 資料表的目前結構](../../relational-databases/tables/examining-the-current-structure-of-the-employee-table.md)  
  
## 下一課  
[第 2 課：在階層式資料表中建立與管理資料](../../relational-databases/tables/lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
  
  
  
