---
title: 建立檢視和預存程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- creating views and stored procedures
ms.assetid: 53a0426d-07d8-4b7c-aa21-22632753bad8
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: f4ff7d53cc51d8995cdf348742299daedf574d26
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37301288"
---
# <a name="creating-views-and-stored-procedures"></a>建立檢視和預存程序
  既然 Mary 現在能存取 **TestData** 資料庫，您或許想要建立一些資料庫物件，如檢視和預存程序，然後授與 Mary 存取這些物件。 檢視是預存的 SELECT 陳述式，而預存程序是一個或多個批次執行的 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式。  
  
 檢視的查詢方式就跟資料表一樣，而且不接受參數。 預存程序就比檢視還要複雜。 預存程序能有輸出和輸入參數，而且還能包含控制程式碼流程的陳述式，如 IF 和 WHILE 陳述式。 對於所有在資料庫中的重複動作，使用預存程序是一個不錯的程式設計方法。  
  
 例如，您將使用 CREATE VIEW 建立檢視，其中只選取 **Products** 資料表中的兩個資料行。 接著，您將使用 CREATE PROCEDURE 建立預存程序，其中接受 price 參數並只傳回成本小於指定參數值的產品。  
  
### <a name="to-create-a-view"></a>建立檢視  
  
1.  執行下列陳述式建立簡單的檢視，其中會執行 SELECT 陳述式並將產品名稱及價格傳回給使用者。  
  
    ```  
    CREATE VIEW vw_Names  
       AS  
       SELECT ProductName, Price FROM Products;  
    GO  
  
    ```  
  
### <a name="test-the-view"></a>測試檢視  
  
1.  檢視的處理方式和資料表一樣。 使用 `SELECT` 陳述式存取檢視。  
  
    ```  
    SELECT * FROM vw_Names;  
    GO  
  
    ```  
  
### <a name="to-create-a-stored-procedure"></a>若要建立預存程序  
  
1.  下列陳述式會建立預存程序名稱 `pr_Names`，接受資料類型為 `@VarPrice` 的輸入參數 (名稱是 `money`)。 預存程序會列印與輸出參數串連的 `Products less than` 陳述式，而這個輸出參數會從 `money` 資料類型變更為 `varchar(10)` 字元資料類型。 然後，預存程序會執行檢視上的 `SELECT` 陳述式，將輸出參數當做 `WHERE` 子句的一部分進行傳遞。 這樣會傳回成本小於輸出參數值的所有產品。  
  
    ```  
    CREATE PROCEDURE pr_Names @VarPrice money  
       AS  
       BEGIN  
          -- The print statement returns text to the user  
          PRINT 'Products less than ' + CAST(@VarPrice AS varchar(10));  
          -- A second statement starts here  
          SELECT ProductName, Price FROM vw_Names  
                WHERE Price < @varPrice;  
       END  
    GO  
  
    ```  
  
### <a name="test-the-stored-procedure"></a>測試預存程序  
  
1.  若要測試預存程序，請輸入並執行下列陳述式。 這個程序應該傳回兩個成本小於 `Products` 的產品名稱，這兩個產品是在第 1 課輸入 `10.00`資料表而來的。  
  
    ```  
    EXECUTE pr_Names 10.00;  
    GO  
  
    ```  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [授與資料庫物件的存取權](lesson-2-4-granting-access-to-a-database-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
