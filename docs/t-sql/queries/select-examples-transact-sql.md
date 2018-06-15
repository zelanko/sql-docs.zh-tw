---
title: SELECT 範例 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- parentheses [SQL Server]
- GROUP BY clause, SELECT statement
- query hints [SQL Server]
- ALL keyword
- ROLLUP operator
- SELECT statement [SQL Server], examples
- correlated subqueries, SELECT statement
- SELECT INTO statement
- ORDER BY clause [Transact-SQL]
- GROUPING function
- index hints [SQL Server]
- HAVING clause, SELECT statement
- DISTINCT keyword
- CUBE operator
- UNION operator [SQL Server]
- computed sums
- WHERE clause, SELECT statement
ms.assetid: 9b9caa3d-e7d0-42e1-b60b-a5572142186c
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ebd04f177103c8fa105ec6fc1ab2289e1e643f9e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33064645"
---
# <a name="select-examples-transact-sql"></a>SELECT 範例 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  本主題提供使用 [SELECT](../../t-sql/queries/select-transact-sql.md) 陳述式的範例。  
  
## <a name="a-using-select-to-retrieve-rows-and-columns"></a>A. 使用 SELECT 擷取資料列和資料行  
 下列範例會顯示三個程式碼範例。 第一個程式碼範例會從 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的 `*` 資料表中，傳回所有資料列 (未指定 WHERE 子句) 和所有資料行 (使用 `Product`)。  
  
 [!code-sql[Select#SelectExamples1](../../t-sql/queries/codesnippet/tsql/select-examples-transact_1.sql)]  
  
 這個範例會從 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的 `Name` 資料表中，傳回所有資料列 (未指定 WHERE 子句)，但只傳回資料行子集 (`ProductNumber`、`ListPrice`、`Product`)。 另外，也會加入一個資料行標題。  
  
 [!code-sql[Select#SelectExamples2](../../t-sql/queries/codesnippet/tsql/select-examples-transact_2.sql)]  
  
 這個範例只傳回產品行是 `Product` 且製造天數小於 `R` 天的 `4` 資料列。  
  
 [!code-sql[Select#SelectExamples3](../../t-sql/queries/codesnippet/tsql/select-examples-transact_3.sql)]  
  
## <a name="b-using-select-with-column-headings-and-calculations"></a>B. 使用 SELECT 與資料行標題及計算  
 下列範例會傳回 `Product` 資料表的所有資料列。 第一個範例傳回銷售總額及各項產品的折扣。 第二個範例則針對各項產品來計算總收入。  
  
 [!code-sql[Select#SelectExamples4](../../t-sql/queries/codesnippet/tsql/select-examples-transact_4.sql)]  
  
 這是計算每份銷售訂單中各項產品之收入的查詢。  
  
 [!code-sql[Select#SelectExamples5](../../t-sql/queries/codesnippet/tsql/select-examples-transact_5.sql)]  
  
## <a name="c-using-distinct-with-select"></a>C. 使用 DISTINCT 與 SELECT  
 下列範例會利用 `DISTINCT` 來防止擷取重複的標題。  
  
 [!code-sql[Select#SelectExamples6](../../t-sql/queries/codesnippet/tsql/select-examples-transact_6.sql)]  
  
## <a name="d-creating-tables-with-select-into"></a>D. 使用 SELECT INTO 建立資料表  
 下列第一個範例會在 `#Bicycles` 中，建立一份名稱為 `tempdb` 的暫存資料表。  
  
 [!code-sql[Select#SelectExamples7](../../t-sql/queries/codesnippet/tsql/select-examples-transact_7.sql)]  
  
 第二個範例會建立永久資料表 `NewProducts`。  
  
 [!code-sql[Select#SelectExamples8](../../t-sql/queries/codesnippet/tsql/select-examples-transact_8.sql)]  
  
## <a name="e-using-correlated-subqueries"></a>E. 使用相互關聯的子查詢  
 下列範例會顯示語意相等的查詢，且說明使用 `EXISTS` 關鍵字和 `IN` 關鍵字之間的差異。 兩者都是有效子查詢，擷取產品模型是長袖標誌緊身內衣之各項產品名稱的單一執行個體的，`ProductModelID` 和 `Product` 資料表的 `ProductModel` 號碼相符。  
  
 [!code-sql[Select#SelectExamples9](../../t-sql/queries/codesnippet/tsql/select-examples-transact_9.sql)]  
  
 下列範例在相關或重複的子查詢中使用 `IN`。 這是一項相依於外部查詢來取得其值的查詢。 這項查詢會重複執行，外部查詢可能選取的每個資料列各執行一次。 這個查詢會擷取 `SalesPerson` 資料表中的獎金是 `5000.00`，且 `Employee` 和 `SalesPerson` 資料表中的員工識別碼相符的每一位員工的姓名執行個體。  
  
 [!code-sql[Select#SelectExamples10](../../t-sql/queries/codesnippet/tsql/select-examples-transact_10.sql)]  
  
 這個陳述式中先前的子查詢無法在外部查詢之外獨立評估。 它需要 `Employee.EmployeeID` 值，但在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 檢查 `Employee` 中的不同資料列時，這個值會跟著改變。  
  
 您也可以在外部查詢的 `HAVING` 子句中，使用相關的子查詢。 這個範例會尋找最大標價大於模型平均值兩倍的產品模型。  
  
 [!code-sql[Select#SelectExamples11](../../t-sql/queries/codesnippet/tsql/select-examples-transact_11.sql)]  
  
 這個範例利用相關的子查詢來尋找銷售了特定產品的員工名稱。  
  
 [!code-sql[Select#SelectExamples12](../../t-sql/queries/codesnippet/tsql/select-examples-transact_12.sql)]  
  
## <a name="f-using-group-by"></a>F. 使用 GROUP BY  
 下列範例會尋找資料庫中每份銷售訂單的總計。  
  
 [!code-sql[Select#SelectExamples13](../../t-sql/queries/codesnippet/tsql/select-examples-transact_13.sql)]  
  
 由於 `GROUP BY` 子句，只會針對每份銷焦訂單，傳回一個包含所有銷售總和的資料行。  
  
## <a name="g-using-group-by-with-multiple-groups"></a>G. 使用 GROUP BY 與多個群組  
 下列範例會依照產品識別碼和特殊優惠識別碼，來尋找平均價格和年初至今的銷售總和。  
  
 [!code-sql[Select#SelectExamples14](../../t-sql/queries/codesnippet/tsql/select-examples-transact_14.sql)]  
  
## <a name="h-using-group-by-and-where"></a>H. 使用 GROUP BY 與 WHERE  
 下列範例會在只擷取標價大於 `$1000` 的資料列之後，將結果放入群組中。  
  
 [!code-sql[Select#SelectExamples15](../../t-sql/queries/codesnippet/tsql/select-examples-transact_15.sql)]  
  
## <a name="i-using-group-by-with-an-expression"></a>I. 使用 GROUP BY 與運算式  
 下列範例會依運算式來分組。 如果運算式不包括彙總函式，您可以依運算式來進行分組。  
  
 [!code-sql[Select#SelectExamples16](../../t-sql/queries/codesnippet/tsql/select-examples-transact_16.sql)]  
  
## <a name="j-using-group-by-with-order-by"></a>J. 使用 GROUP BY 與 ORDER BY  
 下列範例會尋找各項產品類型的平均價格，且會依照平均價格來排序結果。  
  
 [!code-sql[Select#SelectExamples18](../../t-sql/queries/codesnippet/tsql/select-examples-transact_17.sql)]  
  
## <a name="k-using-the-having-clause"></a>K. 使用 HAVING 子句  
 下列第一個範例會顯示含彙總函式的 `HAVING` 子句。 它會依照產品識別碼來分組 `SalesOrderDetail` 資料表中的資料列，且會刪除平均訂單數量是五或更少的產品。 第二個範例顯示不含彙總函式的 `HAVING` 子句。  
  
 [!code-sql[Select#SelectExamples19](../../t-sql/queries/codesnippet/tsql/select-examples-transact_18.sql)]  
  
 這個查詢在 `LIKE` 子句中使用 `HAVING` 子句。  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT SalesOrderID, CarrierTrackingNumber   
FROM Sales.SalesOrderDetail  
GROUP BY SalesOrderID, CarrierTrackingNumber  
HAVING CarrierTrackingNumber LIKE '4BD%'  
ORDER BY SalesOrderID ;  
GO  
```  
  
## <a name="l-using-having-and-group-by"></a>L. 使用 HAVING 與 GROUP BY  
 下列範例會顯示如何在單一 `GROUP BY` 陳述式中使用 `HAVING`、`WHERE`、`ORDER BY` 和 `SELECT` 子句。 它會產生群組和摘要值，但會先刪除價格超出 $25，且平均訂單數量在 5 之下的產品，再執行這個動作。 此外，它也會依照 `ProductID` 組織結果。  
  
 [!code-sql[Select#SelectExamples21](../../t-sql/queries/codesnippet/tsql/select-examples-transact_19.sql)]  
  
## <a name="m-using-having-with-sum-and-avg"></a>M. 使用 HAVING 與 SUM 及 AVG  
 下列範例會依產品識別碼來分組 `SalesOrderDetail` 資料表，且只會包括訂單總計超出 `$1000000.00`，平均訂單數量小於 `3` 的產品群組。  
  
 [!code-sql[Select#SelectExamples22](../../t-sql/queries/codesnippet/tsql/select-examples-transact_20.sql)]  
  
 若要查看總銷售額大於 `$2000000.00` 的產品，請使用這項查詢：  
  
 [!code-sql[Select#SelectExamples23](../../t-sql/queries/codesnippet/tsql/select-examples-transact_21.sql)]  
  
 如果您要確定每項產品的計算都至少包含了一千五百個項目，請利用 `HAVING COUNT(*) > 1500` 來刪除傳回銷售總計小於 `1500` 項的產品。 查詢內容如下所示：  
  
 [!code-sql[Select#SelectExamples24](../../t-sql/queries/codesnippet/tsql/select-examples-transact_22.sql)]  
  
## <a name="n-using-the-index-optimizer-hint"></a>N. 使用 INDEX 最佳化工具提示  
 下列範例會顯示兩種使用 `INDEX` 最佳化工具提示的方法。 第一個範例顯示如何強制最佳化工具利用非叢集索引來擷取資料表中的資料列，第二個範例則強制利用索引 0 來掃描資料表。  
  
 [!code-sql[Select#SelectExamples45](../../t-sql/queries/codesnippet/tsql/select-examples-transact_23.sql)]  
  
## <a name="m-using-option-and-the-group-hints"></a>M. 使用 OPTION 與 GROUP 提示  
 下列範例會顯示如何搭配 `OPTION (GROUP)` 子句來使用 `GROUP BY` 子句。  
  
 [!code-sql[Select#SelectExamples46](../../t-sql/queries/codesnippet/tsql/select-examples-transact_24.sql)]  
  
## <a name="o-using-the-union-query-hint"></a>O. 使用 UNION 查詢提示  
 下列範例使用 `MERGE UNION` 查詢提示。  
  
 [!code-sql[Select#SelectExamples47](../../t-sql/queries/codesnippet/tsql/select-examples-transact_25.sql)]  
  
## <a name="p-using-a-simple-union"></a>P. 使用簡單 UNION  
 在下列範例中，結果集包括 `ProductModelID` 和 `Name` 資料表之 `ProductModel` 和 `Gloves` 資料行的內容。  
  
 [!code-sql[Select#SelectExamples48](../../t-sql/queries/codesnippet/tsql/select-examples-transact_26.sql)]  
  
## <a name="q-using-select-into-with-union"></a>Q. 搭配 UNION 使用 SELECT INTO  
 在下列範例中，第二個 `INTO` 陳述式中的 `SELECT` 子句指定利用名稱為 `ProductResults` 的資料表，保留 `ProductModel` 和 `Gloves` 資料表的指定資料行之聯集的最終結果集。 請注意，`Gloves` 資料表建立在第一個 `SELECT` 陳述式中。  
  
 [!code-sql[Select#SelectExamples49](../../t-sql/queries/codesnippet/tsql/select-examples-transact_27.sql)]  
  
## <a name="r-using-union-of-two-select-statements-with-order-by"></a>R. 搭配 ORDER BY 使用兩個 SELECT 陳述式的 UNION  
 搭配 UNION 子句使用之特定參數的順序非常重要。 下列範例會顯示在兩個 `UNION` 陳述式中的輸出重新命名一個資料行時，`SELECT` 的正確和不正確用法。  
  
 [!code-sql[Select#SelectExamples50](../../t-sql/queries/codesnippet/tsql/select-examples-transact_28.sql)]  
  
## <a name="s-using-union-of-three-select-statements-to-show-the-effects-of-all-and-parentheses"></a>S. 利用三個 SELECT 陳述式的 UNION 來顯示 ALL 和括號的作用  
 下列範例會利用 `UNION` 來結合有 5 個相同資料列的三份資料表的結果。 第一個範例利用 `UNION ALL` 來顯示重複的記錄，以及傳回所有的 15 個資料列。 第二個範例利用不含 `UNION` 的 `ALL` 來刪除三個 `SELECT` 陳述式之組合結果中重複的資料列，並傳回 5 個資料列。  
  
 第三個範例搭配第一個 `ALL` 來使用 `UNION`，用括號括住未使用 `UNION` 的第二個 `ALL`。 第二個 `UNION` 會先處理，因為它在括號中，且會傳回 5 個資料列，因為並未使用 `ALL` 選項，複本會移除。 這 5 個資料列利用 `SELECT` 關鍵字，與第一個 `UNION ALL` 的結果結合起來。 這並不會在兩組 5 個資料列之間移除複本。 最終結果有 10 個資料列。  
  
 [!code-sql[Select#SelectExamples51](../../t-sql/queries/codesnippet/tsql/select-examples-transact_29.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [UNION &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-union-transact-sql.md)   
 [EXCEPT 和 INTERSECT &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [PathName &#40;Transact-SQL&#41;](../../relational-databases/system-functions/pathname-transact-sql.md)   
 [INTO 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-into-clause-transact-sql.md)  
  
  
