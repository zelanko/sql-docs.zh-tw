---
title: 第 1 課：將資料表轉換為階層式結構 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 66e77d0badf14a804cb82249d03ed552e1f8dcfb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52788700"
---
# <a name="lesson-1-converting-a-table-to-a-hierarchical-structure"></a>第 1 課：將資料表轉換為階層式結構
  具有使用自我聯結表達階層式關聯性之資料表的客戶可以使用本課程當做指導方針，將其資料表轉換為階層式結構。 從這種表示法移轉到另一種使用 `hierarchyid` 之表示法的步驟非常簡單。 移轉之後，使用者將會有一個精簡而且容易了解的階層式表示法，可以使用數種方式建立索引以便進行有效率的查詢。  
  
 本課程會檢查現有的資料表、建立包含 `hierarchyid` 資料行的新資料列、使用來源資料表中的資料擴展資料表，然後示範三個索引策略。 這個課程包含下列主題：  
  
-   [檢查 Employee 資料表的目前結構](lesson-1-1-examining-the-current-structure-of-the-employee-table.md)  
  
-   [使用現有的階層式資料填入資料表](lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
-   [最佳化 NewOrg 資料表](lesson-1-3-optimizing-the-neworg-table.md)  
  
-   [摘要：將資料表轉換為階層式結構](lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
## <a name="prerequisites"></a>先決條件  
 本課程需要使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [檢查 Employee 資料表的目前結構](lesson-1-1-examining-the-current-structure-of-the-employee-table.md)  
  
## <a name="next-lesson"></a>下一課  
 [第 2 課：建立及管理階層式資料表中的資料](lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
  
  
