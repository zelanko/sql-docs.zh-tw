---
title: "建立 UNION 查詢 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6c1ec545f2175067a3e4d6f9f625356607cb0eb4
ms.lasthandoff: 04/11/2017

---
# <a name="create-union-queries-visual-database-tools"></a>建立 UNION 查詢 (Visual Database Tools)
UNION 關鍵字讓您可以在所產生的單一資料表中，包含 2 個 SELECT 陳述式的結果。 由任一 SELECT 陳述式所傳回的所有資料列，會被結合為 UNION 運算式的結果。 如需範例，請參閱 [SELECT 範例 (Transact-SQL)](http://msdn.microsoft.com/en-us/9b9caa3d-e7d0-42e1-b60b-a5572142186c)。  
  
> [!NOTE]  
> 圖表窗格只能顯示單一 SELECT 子句。 因此，當您使用 UNION 查詢時，查詢設計工具會隱藏資料表運算窗格。  
  
### <a name="to-create-a-merged-select-query"></a>建立合併的 SELECT 查詢  
  
1.  開啟查詢或建立新查詢。  
  
2.  在 SQL 窗格中，輸入有效的 UNION 運算式。  
  
    下列範例是有效的 UNION 運算式。  
  
    ```  
    SELECT ProductModelID, Name  
    FROM Production.ProductModel  
    UNION  
    SELECT ProductModelID, Name   
    FROM dbo.Gloves;  
    ```  
  
3.  在 [查詢設計工具]**** 功能表中，按一下 [執行 SQL]**** 來執行查詢。  
  
    查詢設計工具目前已格式化您的 UNION 查詢。  
  
## <a name="see-also"></a>另請參閱  
[支援的查詢類型 (Visual Database Tools)](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[設計查詢和檢視使用說明主題 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[執行查詢的基本作業 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[UNION (Transact-SQL)](http://msdn.microsoft.com/en-us/607c296f-8a6a-49bc-975a-b8d0c0914df7)  
  

