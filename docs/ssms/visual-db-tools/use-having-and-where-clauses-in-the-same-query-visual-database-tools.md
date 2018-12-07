---
title: 在相同查詢中使用 HAVING 和 WHERE 子句 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- search criteria [SQL Server], WHERE clause
- search conditions [SQL Server], HAVING clause
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- HAVING clause, search criteria
- search conditions [SQL Server], WHERE clause
- WHERE clause, search criteria
- excluding rows
ms.assetid: 1e07cf56-b4b7-4c49-8ddd-c276812a7148
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a6e778155ad0a470bd5b9e97484aea94d205055
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52537305"
---
# <a name="use-having-and-where-clauses-in-the-same-query-visual-database-tools"></a>在相同查詢中使用 HAVING 和 WHERE 子句 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
在某些情況下，將條件套用到整個群組 (使用 HAVING 子句) 之前，您可能會想排除群組中的個別資料列 (使用 WHERE 子句)。  
  
HAVING 子句類似 WHERE 子句，但是只適用於整個群組 (也就是在結果集中表示群組的資料列)，而 WHERE 子句則適用於個別資料列。 查詢可以同時包含 WHERE 子句和 HAVING 子句。 在此情況下：  
  
-   WHERE 子句會先套用到 [圖表] 窗格的資料表或資料表值物件的個別資料列。 只有符合 WHERE 子句條件的資料列才會被分組。  
  
-   然後 HAVING 子句會套用到結果集的資料列。 只有符合 HAVING 條件的群組才會出現在查詢輸出中。 您只能將 HAVING 子句套用到也出現在 GROUP BY 子句或彙總函式的資料行。  
  
例如，想像您將 `titles` 和 `publishers` 資料表加以聯結，建立能顯示不同出版商平均書價的查詢。 您只想看到某一群特定出版商的平均價格，也許是加州的出版商。 甚至，您只想看平均價格超過 $10.00 的出版商。  
  
您可以加入 WHERE 子句以建立第一個條件，忽略任何不在加州的出版商，然後才計算平均價格。 第二個條件需要 HAVING 子句，因為條件是以資料的分組和摘要結果為基礎。 產生的 SQL 陳述式將如下所示：  
  
```  
SELECT titles.pub_id, AVG(titles.price)  
FROM titles INNER JOIN publishers  
   ON titles.pub_id = publishers.pub_id  
WHERE publishers.state = 'CA'  
GROUP BY titles.pub_id  
HAVING AVG(price) > 10  
```  
  
您可以在 [準則] 窗格中同時建立 HAVING 和 WHERE 子句。 依照預設，如果您為資料行指定搜尋條件，條件會成為 HAVING 子句的一部分。 然而，您可以將條件變更為 WHERE 子句。  
  
您可以建立需要相同資料行的 WHERE 子句和 HAVING 子句。 若要這樣做，您必須加入兩次資料行到 [準則] 窗格，然後指定一個準則做為 HAVING 子句的一部分，另外一個準則做為 WHERE 子句的一部分。  
  
### <a name="to-specify-a-where-condition-in-an-aggregate-query"></a>若要在彙總查詢指定 WHERE 條件  
  
1.  為您的查詢指定群組。 如需詳細資訊，請參閱 [群組查詢結果中的資料列 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md)。  
  
2.  如果沒有出現在 [準則] 窗格中，加入您想要組成 WHERE 條件的資料行。  
  
3.  除非資料的資料行是 GROUP BY 子句的一部分，或包含在彙總函式中，否則清除 [輸出] 資料行。  
  
4.  在 [篩選條件] 資料行中，指定 WHERE 條件。 [查詢和檢視設計師] 會將條件加入到 SQL 陳述式的 HAVING 子句。  
  
    > [!NOTE]  
    > 在這個程序中所顯示的查詢範例聯結了兩個資料表， `titles` 和 `publishers`。  
  
    這個時候，在查詢中 SQL 陳述式包含一個 HAVING 子句：  
  
    ```  
    SELECT titles.pub_id, AVG(titles.price)  
    FROM titles INNER JOIN publishers   
       ON titles.pub_id = publishers.pub_id  
    GROUP BY titles.pub_id  
    HAVING publishers.state = 'CA'  
    ```  
  
5.  在 [群組依據] 資料行中，從群組和摘要選項清單中選擇 [Where]。 [查詢和檢視設計師] 移除 SQL 陳述式中的 HAVING 子句條件，然後加入到 WHERE 子句。  
  
    SQL 陳述式變更為包含了 WHERE 子句：  
  
    ```  
    SELECT titles.pub_id, AVG(titles.price)  
    FROM titles INNER JOIN publishers   
       ON titles.pub_id = publishers.pub_id  
    WHERE publishers.state = 'CA'  
    GROUP BY titles.pub_id  
    ```  
  
## <a name="see-also"></a>另請參閱  
[排序及群組查詢結果 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[摘要查詢結果 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  
