---
title: "支援的查詢類型 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Delete query
- queries [SQL Server], types
- Update query
- Query Designer [SQL Server], query types
- Criteria pane
- Insert Values query
- Select query
- Make Table query
- Insert Results query
- Diagram pane [Visual Database Tools]
- View Designer, query types
ms.assetid: 72b9116c-c128-4078-a78d-257a2955a3f6
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 448de9dd9238d62e1b71d76f15807c73ce2fcc03
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="supported-query-types-visual-database-tools"></a>支援的查詢類型 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 在[查詢和檢視表設計工具](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)的 [圖表] 和 [準則] 窗格 (圖形窗格) 中，您可以建立下列查詢類型：  
  
-   **選取查詢** ：從一或多個資料表或檢視擷取資料。 此類查詢將建立 SQL SELECT 陳述式。  
  
-   **插入結果** ：將一個資料表的現有資料列複製到另一個資料表，或複製到同一個資料表中做為新的資料列，以建立新的資料列。 此類查詢將建立 SQL INSERT INTO...SELECT 陳述式。  
  
-   **插入值** ：建立新資料列，並將新值插入至指定的資料行。 此類查詢將建立 SQL INSERT INTO...VALUES 陳述式。  
  
-   **更新查詢** ：變更資料表中一或多個現有資料列中的個別資料行值。 此類查詢將建立 SQL UPDATE…SET 陳述式。  
  
-   **刪除查詢** ：從資料表移除一或多個資料列。 這類查詢將建立 SQL DELETE 陳述式。  
  
    > [!NOTE]  
    > [刪除查詢] 會刪除資料表中的整個資料列。 如果您要刪除個別的資料欄值，請使用 UPDATE 查詢。  
  
-   **製成資料表查詢** ：建立新資料表，並且將查詢結果複製到該新資料表中來建立資料列。 此類查詢將建立 SQL SELECT...INTO 陳述式。  
  
除了使用圖形窗格來建立查詢外，您可以將任何 SQL 陳述式輸入 SQL 窗格，如聯合查詢 (Union Query)。  
  
當您使用 SQL 陳述式建立的查詢無法在圖形窗格顯示時，查詢和檢視設計師將使這些窗格變成暗灰色，表示他們無法反映您所建立的查詢。 但這些暗灰色的窗格仍處於作用中狀態，而且在許多情況下，您可以在這些窗格中變更查詢。 如果您的變更使得圖形窗格可以顯示查詢，這些窗格就不再是暗灰色了。  
  
## <a name="see-also"></a>另請參閱  
[設計查詢和檢視使用說明主題 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[查詢類型 (Visual Database Tools)](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
  
