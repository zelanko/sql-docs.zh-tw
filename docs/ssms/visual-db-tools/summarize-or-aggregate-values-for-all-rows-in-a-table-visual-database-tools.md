---
title: 摘要或彙總資料表中所有資料列的值 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- summarizing query results
- aggregate functions [SQL Server], summarizing query results
ms.assetid: f5af876e-f937-4110-ba09-07999c35a699
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4921dc12b4eb6532d89b9231fb707b411af8aec4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33052445"
---
# <a name="summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools"></a>摘要或彙總資料表中所有資料列的值 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
## <a name="aggregate-function"></a>彙總函式
使用彙總函式 (Aggregate Function) 可以在資料表中建立所有值的摘要。 例如，您可以建立如下所示的查詢，以顯示在 `titles` 資料表中所有書籍的總價格：  
  
```  
SELECT SUM(price)  
FROM titles  
```  
  
對多個資料行使用彙總函式，在相同查詢中建立多個彙總。 例如，您可以建立計算 `price` 資料行總計和 `discount` 資料行平均的查詢。  
  
在相同查詢中，您可以使用不同的方法彙總相同的資料行 (例如加總、計數和平均)。 例如，下列查詢會平均並加總 `price` 資料表的 `titles` 資料行：  
  
```  
SELECT AVG(price), SUM(price)  
FROM titles  
```  
  
如果加入搜尋條件，您可以彙總符合條件的資料列子集。  

**注意！** 您可以計算資料表中的所有資料列，或計算符合指定條件的資料列。 如需詳細資訊，請參閱[計算資料表中的資料列 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/count-rows-in-a-table-visual-database-tools.md)。  
  
  
在建立資料表中所有資料列的單一彙總值時，只顯示彙總值本身。 例如，如果加總 `price` 資料表的 `titles` 資料行值，將不會顯示個別的書名、出版者名稱等等。  
 
 **!** 如果進行小計，也就是建立群組，可以顯示每個群組的資料行值。 如需詳細資訊，請參閱[群組查詢結果中的資料列 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md)。  

## <a name="aggregate-values-for-all-rows"></a>彙總所有資料列的值  
  
1.  請確定您要彙總的資料表已經出現在 [圖表] 窗格中。  
  
2.  在 [圖表] 窗格的背景上按一下滑鼠右鍵，然後從快速鍵功能表中選擇 [群組依據]。 [查詢和檢視表設計工具](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)會將 [群組依據] 資料行新增至 [準則] 窗格的方格中。  
  
3.  將您想彙總的資料行加入至 [準則] 窗格。 務必標記資料行以進行輸出。  
  
    [查詢和檢視表設計工具] 會自動將資料行別名指派給您要加總的資料行。 您可以使用較有意義的別名取代這個別名。 如需詳細資訊，請參閱[建立資料行別名 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md)。  
  
4.  在 [群組依據] 方格資料行中，選取適當的彙總函式，例如：[Sum]、[Avg]、[Min]、[Max]、[Count]。 如果只要彙總結果集中的唯一資料列，請選擇含有 DISTINCT 選項的彙總函式，例如 [Min Distinct]。 不要選擇 [Group By]、[Expression] 或 [Where]，因為這些選項不適用於彙總所有資料列。  
  
    查詢和檢視表設計工具會使用指定的彙總函式，取代 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)中陳述式的資料行名稱。 例如，SQL 陳述式將如下所示：  
  
    ```  
    SELECT SUM(price)  
    FROM titles  
    ```  
  
5.  若要在查詢中建立一個以上的彙總，請重複步驟 3 和 4。  
  
    當其他資料行新增至查詢輸出清單或排序依據清單時，查詢和檢視表設計工具會自動將 [群組依據] 一詞填入至方格的 [群組依據] 資料行。 選取適當的彙總函式。  
  
6.  加入搜尋條件 (如果有)，以指定要加總的資料列子集。  
  
在執行查詢時，[結果] 窗格會顯示指定的彙總。  
  
> [!NOTE]  
> [查詢和檢視表設計工具] 會在 [SQL] 窗格中將彙總函式保持為 SQL 陳述式的一部分，直到明確關閉 [群組依據] 模式為止。 因此，如果您變更查詢類型，或變更在 [圖表] 窗格中顯示的資料表或資料表值物件，以便修改查詢，則結果查詢可能會包含無效的彙總函式。  
  
## <a name="see-also"></a>另請參閱  
[排序及分組查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[摘要查詢結果 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  
