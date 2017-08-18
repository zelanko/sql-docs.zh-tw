---
title: "建立子查詢 (Visual Database Tools) | Microsoft Docs"
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
- search criteria [SQL Server], subqueries
- nested queries
- subqueries [SQL Server], SQL pane
ms.assetid: 34f6b9b4-ca3a-4a4f-9594-36e513f1c547
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2eb9fd6d0a542c4b9636edb1b65b146b0c043e2d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/18/2017

---
# <a name="create-subqueries-visual-database-tools"></a>建立子查詢 (Visual Database Tools)
可以使用某個查詢的結果做為另一個查詢的輸入。 子查詢的結果可以用來做為使用 IN( ) 函數、EXISTS 運算子或 FROM 子句的陳述式。  
  
您可以在 [SQL] 窗格中直接輸入子查詢，也可以複製查詢，再貼入至另一個子查詢中，以建立子查詢。  
  
### <a name="to-define-a-subquery-in-the-sql-pane"></a>若要在 SQL 窗格中定義子查詢  
  
1.  建立主查詢。  
  
2.  在 [SQL] 窗格中選取 SQL 陳述式，然後使用 [複製] 將查詢移至 [剪貼簿]。  
  
3.  起始新的查詢，然後使用 [貼上] 將第一個查詢移至新查詢的 WHERE 或 FROM 子句。  
  
    例如，假設您有兩個資料表 `products` 和 `suppliers`，並且想建立顯示 Sweden 供應商的所有產品的查詢。 請先在 `suppliers` 資料表建立第一個查詢，以找出所有的 Swedish 供應商：  
  
    ```  
    SELECT supplier_id  
    FROM supplier  
    WHERE (country = 'Sweden')  
    ```  
  
    使用 [複製] 指令將此查詢移至剪貼簿。 建立使用 `products` 資料表的第二個查詢，以列出所需的產品資訊：  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    ```  
  
    在 [SQL] 窗格中，將 WHERE 子句加入至第二個查詢，然後從剪貼簿貼入第一個查詢。 在第一個查詢加上括號，使其最終結果如下所示：  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    WHERE supplier_id IN  
       (SELECT supplier_id  
      FROM supplier  
      WHERE (country = 'Sweden'))  
    ```  
  
## <a name="see-also"></a>另請參閱  
[支援的查詢類型 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[指定搜尋準則 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  

