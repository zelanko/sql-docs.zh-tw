---
title: "讀取資料表中的資料 (教學課程) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- reading data in a table
ms.assetid: 532232c9-3d41-45cd-9150-de67a1cbfcf5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 37d35412e052c6b47ef08ece1f861fcd3c44b88e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="lesson-1-4---reading-the-data-in-a-table"></a>課程 1-4 - 讀取資料表中的資料
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)] 使用 SELECT 陳述式來讀取資料表中的資料。 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式中最重要的其中一個陳述式就是 SELECT 陳述式，而其中有很多的語法變化。 在本教學課程中，您將使用五種簡單的變化樣式。  
  
### <a name="to-read-the-data-in-a-table"></a>讀取資料表的資料  
  
1.  輸入並執行下列陳述式，以讀取 `Products` 資料表的資料。  
  
    ```  
    -- The basic syntax for reading data from a single table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
    GO  
  
    ```  
  
2.  您可以使用星號，選取資料表中的所有資料行。 這個方法常在隨選查詢中使用。 您應該在固定程式碼中提供資料行清單，使陳述式會傳回預期的資料行，即使以後加入新資料行還是一樣。  
  
    ```  
    -- Returns all columns in the table  
    -- Does not use the optional schema, dbo  
    SELECT * FROM Products  
    GO  
  
    ```  
  
3.  您可以省略不要傳回的資料行。 而且會以資料行所列出的順序來傳回資料行。  
  
    ```  
    -- Returns only two of the columns from the table  
    SELECT ProductName, Price  
        FROM dbo.Products  
    GO  
  
    ```  
  
4.  使用 `WHERE` 子句，限制要傳回給使用者的資料列。  
  
    ```  
    -- Returns only two of the records in the table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
        WHERE ProductID < 60  
    GO  
  
    ```  
  
5.  您可以處理資料行中所傳回的值。 下列範例會在 `Price` 資料行上進行數學運算。 除非使用 `AS` 關鍵字提供名稱，否則以這種方式變更的資料行將不會有名稱。  
  
    ```  
    -- Returns ProductName and the Price including a 7% tax  
    -- Provides the name CustomerPays for the calculated column  
    SELECT ProductName, Price * 1.07 AS CustomerPays  
        FROM dbo.Products  
    GO  
    ```  
  
## <a name="functions-that-are-useful-in-a-select-statement"></a>函數對 SELECT 陳述式相當有用  
如需有關某些可在 SELECT 陳述式中用來處理資料之函數的詳細資訊，請參閱下列主題：  
  
|||  
|-|-|  
|[字串函數 &#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md)|[日期和時間資料類型與函數 &#40;Transact-SQL&#41;](../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)|  
|[數學函數 &#40;Transact-SQL&#41;](../t-sql/functions/mathematical-functions-transact-sql.md)|[Text 和 Image 函數 &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[摘要：建立資料庫物件](../t-sql/lesson-1-5-summary-creating-database-objects.md)  
  
## <a name="see-also"></a>另請參閱  
[SELECT &#40;Transact-SQL&#41;](../t-sql/queries/select-transact-sql.md)  
  
  
  
