---
title: 將查詢結果中的資料列分組 (Visual Database Tools) | Microsoft Docs
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
- summarizing table subsets
- grouping rows
- grouping query results
ms.assetid: b07082d5-4d55-4903-9af9-4c470554c6d3
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 72ef5527dd8cc1c6feae1eeb41e09b479425810c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33048475"
---
# <a name="group-rows-in-query-results-visual-database-tools"></a>群組查詢結果中的資料列 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
如果您要建立小計，或顯示資料表子集的其他摘要資訊，請使用彙總查詢 (Aggregate Query) 建立群組。 每個群組都會針對資料表中具有相同值的所有資料列摘要資料。  
  
例如，您可能想查看 `titles` 資料表中某本書的平均價格，但是想依照簽發者顯示結果。 若要這麼做，請依照簽發者將查詢分組 (例如， `pub_id`)。 結果查詢輸出可能如下所示：  
  
![查詢結果：依發行者分組的平均價格](../../ssms/visual-db-tools/media/dv3w9e1.gif "查詢結果：依發行者分組的平均價格")  
  
將資料分組時，您只能顯示摘要或分組的資料，例如：  
  
-   分組資料行 (出現在 GROUP BY 子句中的資料行) 的值。 在上述範例中， `pub_id` 就是分組資料行。  
  
-   SUM( ) 及 AVG( ) 之類彙總函式所產生的值。 在上列的範例中，第二個資料行是使用 AVG( ) 函數及 `price` 資料行所產生的。  
  
您不能顯示個別資料列的值。 例如，如果您只依照簽發者分組，就不能在查詢中顯示個別標題。 因此，如果您將資料行新增至查詢輸出， [查詢和檢視表設計工具](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 就會自動將這些資料行新增至 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)中的陳述式 GROUP BY 子句。 如果您要改為彙總資料行，您可以針對該資料行指定彙總函式。  
  
如果您依照一個以上的資料行分組，查詢中的每個群組便會顯示所有群組資料行的彙總值。  
  
例如，下列針對 `titles` 執行的查詢同時依照簽發者 (`pub_id`) 以及書籍類型 (`type`) 進行分組。 查詢結果將依照簽發者的順序排列，並顯示簽發者出版的每一種不同書籍類型的摘要資訊：  
  
```  
SELECT pub_id, type, SUM(price) Total_price  
FROM titles  
GROUP BY pub_id, type  
```  
  
產生的輸出將如下所示：  
  
![查詢結果：依發行者和類型分組的價格](../../ssms/visual-db-tools/media/dv3w9e2.gif "查詢結果：依發行者和類型分組的價格")  
  
### <a name="to-group-rows"></a>若要將資料列分組  
  
1.  將您要摘要的資料表加入至 [圖表] 窗格，以便開始進行查詢。  
  
2.  在 [圖表] 窗格的背景上按一下滑鼠右鍵，然後從快速鍵功能表中選擇 [新增群組依據]。 查詢和檢視表設計工具會將 [群組依據] 資料行新增至 [準則] 窗格的方格中。  
  
3.  將您想分組的一或多個資料行加入至 [準則] 窗格。 如果您想讓資料行出現在查詢輸出中，務必選取 [輸出] 資料行進行輸出。  
  
    查詢和檢視設計師會將 GROUP BY 子句加入至 [SQL] 窗格的陳述式中。 例如，SQL 陳述式將如下所示：  
  
    ```  
    SELECT pub_id  
    FROM titles  
    GROUP BY pub_id  
    ```  
  
4.  將您想彙總的一或多個資料行加入至 [準則] 窗格。 務必標記資料行以進行輸出。  
  
5.  在要彙總資料行的 [群組依據] 方格資料格中，選取適當的彙總函式。  
  
    [查詢和檢視表設計工具] 會自動將資料行別名指派給您要加總的資料行。 您可以使用較有意義的別名取代這個自動產生的別名。 如需詳細資訊，請參閱 [建立資料行別名 (Visual Database Tools)](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md)。  
  
    ![將資料行別名新增到查詢結果集](../../ssms/visual-db-tools/media/dv3w9e3.gif "將資料行別名新增到查詢結果集")  
  
    [SQL] 窗格中的對應陳述式將如下所示：  
  
    ```  
    SELECT   pub_id, SUM(price) AS Totalprice  
    FROM     titles  
    GROUP BY pub_id  
    ```  
  
## <a name="see-also"></a>另請參閱  
[排序及群組查詢結果 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
