---
title: MSSQLSERVER_207 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 207 (Database Engine error)
ms.assetid: d1ab00c7-0331-437a-84fe-bae53b82feec
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ba320288a06dd8498d9699712a6e53e34ae93c09
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver207"></a>MSSQLSERVER_207
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|207|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQ_BADCOL|  
|訊息文字|無效的資料行名稱 '%.*ls'。|  
  
## <a name="explanation"></a>說明  
這項查詢錯誤可能是由於下列其中一個問題所造成。  
  
-   資料行名稱拼字錯誤，或者資料行不存在任何指定的資料表中。  
  
-   資料庫的定序會區分大小寫，而且查詢中指定之資料行名稱的大小寫不符合資料表中定義之資料行的大小寫。 例如，如果資料庫中含有區分大小寫的定序，當資料表中的資料行定義為 **LastName**時，以 **Lastname** 或 **lastname** 的形式查詢此資料行會導致系統傳回錯誤 207，因為資料行名稱不符。  
  
-   在 SELECT 子句中定義的資料行別名由其他子句 (例如 WHERE 或 GROUP BY 子句) 所參考。 例如，下列查詢會在 SELECT 子句中定義資料行別名 `Year`，並且在 GROUP BY 子句中參考它。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year, SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY Year;  
    ```  
  
    這則範例會因查詢子句的邏輯處理順序而傳回錯誤 207。 處理順序如下：  
  
    1.  FROM  
  
    2.  ON  
  
    3.  JOIN  
  
    4.  WHERE  
  
    5.  GROUP BY  
  
    6.  WITH CUBE 或 WITH ROLLUP  
  
    7.  HAVING  
  
    8.  SELECT  
  
    9. DISTINCT  
  
    10. ORDER BY  
  
    11. 頂端  
  
    由於處理 SELECT 子句之前尚未定義資料行別名，因此在處理 GROUP BY 子句時別名名稱是未知的。  
  
-   當 *<merge_matched>* 子句參考了來源資料表中的資料行，但是 WHEN NOT MATCHED BY SOURCE 子句中的來源資料表沒有傳回任何資料列時，MERGE 陳述式就會引發這項錯誤。 發生此錯誤的原因是，沒有任何資料列傳回給查詢時，系統無法存取來源資料表中的資料行。 例如，如果無法存取來源資料表的 `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1`，子句 `Col1` 可能會導致陳述式失敗。  
  
## <a name="user-action"></a>使用者動作  
請確認下列資訊並依適當情況更正陳述式。  
  
-   資料行名稱存在資料表中，而且拼字正確。 下列範例會查詢 **sys.columns** 目錄檢視，以便傳回給定資料表的所有資料行名稱。  
  
    ```  
    SELECT name FROM sys.columns WHERE object_id = OBJECT_ID('schema_name.table_name');  
    ```  
  
-   資料庫定序是否區分大小寫。 下列陳述式會傳回指定之資料庫的定序。  
  
    ```  
    SELECT collation_name FROM sys.databases WHERE name = 'database_name';  
    ```  
  
    定序名稱中的縮寫 CS 表示定序會區分大小寫。 例如，Latin1_General_CS_AS 是區分大小寫而且區分腔調字的定序。 請將資料行名稱修改成符合資料表中定義之資料行名稱的大小寫。  
  
-   資料行別名的參考方式不正確。 請在正確的子句中重複定義別名的運算式或使用衍生資料表，藉此修改陳述式。 下列範例會在 GROUP BY 子句中重複定義 `Year` 別名的運算式。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year ,SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY DATEPART(yyyy,OrderDate);  
    ```  
  
    下列範例會使用衍生資料表，讓別名名稱可供查詢中的其他子句使用。 請注意，別名 `Year` 定義於 FROM 子句中 (優先處理)，因此會讓別名可用於查詢中的其他子句。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT d.Year, SUM(TotalDue) AS Total  
    FROM (SELECT DATEPART(yyyy,OrderDate) AS Year, TotalDue  
          FROM Sales.SalesOrderHeader)AS d  
    GROUP BY Year;  
    ```  
  
-   MERGE 陳述式中的 WHEN NOT MATCHED BY SOURCE 子句參考了可存取的值。 請修改 MERGE 陳述式，讓 WHEN NOT MATCHED BY SOURCE 子句中的來源資料表至少會傳回一個資料列。 例如，您可能必須加入或修訂針對該子句所指定的搜尋條件。 或者，您也可以修改子句，以便指定沒有參考來源資料表的值。 例如， `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = <expression, or other available value>`。  
  
## <a name="see-also"></a>另請參閱  
[MERGE &#40;Transact-SQL&#41;](~/t-sql/statements/merge-transact-sql.md)  
[FROM &#40;Transact-SQL&#41;](~/t-sql/queries/from-transact-sql.md)  
[SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](~/t-sql/queries/update-transact-sql.md)  
  

