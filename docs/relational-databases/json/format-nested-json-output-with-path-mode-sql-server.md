---
title: "以 PATH 模式格式化巢狀的 JSON 輸出 (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# 以 PATH 模式格式化巢狀的 JSON 輸出 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  若要保有對 JSON 輸出格式的完整控制權，請指定 **PATH** 選項搭配 **FOR JSON** 子句。  
  
 **PATH** 模式讓您建立包裝函式物件和巢狀複雜屬性。 結果會格式化為 JSON 物件陣列。  
  
 以下是 **FOR JSON** 子句搭配 **PATH** 選項的一些範例。 使用點分隔資料行名稱，或使用巢狀查詢格式化巢狀結果，如下例所示。 輸出預設不包含 Null 值。  
  
## 範例 - 點分隔資料行名稱  
 下列查詢會將 AdventureWorks Person 資料表中的前五個資料列格式化為 JSON。  
  
 **查詢**  
  
```tsql  
SELECT TOP 5   
      BusinessEntityID As Id,  
      FirstName, LastName,  
      Title As 'Info.Title',  
      MiddleName As 'Info.MiddleName'  
  FROM Person.Person  
  FOR JSON PATH  
```  
  
 **結果**  
  
```json  
[  
    {"Id":1,"FirstName":"Ken","LastName":"Sánchez","Info":{"MiddleName":"J"}},  
    {"Id":2,"FirstName":"Terri","LastName":"Duffy","Info":{"MiddleName":"Lee"}},  
    {"Id":3,"FirstName":"Roberto","LastName":"Tamburello"},  
    {"Id":4,"FirstName":"Rob","LastName":"Walters"},  
    {"Id":5,"FirstName":"Gail","LastName":"Erickson","Info":{"Title":"Ms.","MiddleName":"A"}}  
]  
```  
  
 FOR JSON PATH 子句會使用資料行別名或資料行名稱判斷 JSON 輸出的索引鍵名稱。 如果某些別名包含句點，FOR JSON PATH 子句就會建立巢狀物件。 請注意，輸出不會產生有 NULL 值的資料格。  
  
## 範例 - 多份資料表  
 如果在查詢中參考多份資料表，結果會顯示為一般清單，然後 FOR JSON PATH 使用其別名巢狀處理每個資料行。 下列查詢會為在查詢中聯結的每組 (OrderHeader,OrderDetails) 建立一個 JSON 物件：  
  
 **查詢**  
  
```tsql  
SELECT TOP 2 SalesOrderNumber AS 'Order.Number',  
       OrderDate AS 'Order.Date',  
       UnitPrice AS 'Product.Price',  
       OrderQty AS 'Product.Quantity'  
FROM Sales.SalesOrderHeader H  
  INNER JOIN Sales.SalesOrderDetail D  
    ON H.SalesOrderID = D.SalesOrderID  
FOR JSON PATH  
```  
  
 **結果**  
  
```json  
[  
  {  
    "Order":{  
        "Number":"SO43659",  
        "Date":"2011-05-31T00:00:00"  
      },  
    "Product":{  
         "Price":2024.9940,  
         "Quantity":1  
     }  
  },  
  {  
    "Order":{ "Number":"SO43659“ },  
    "Product":{"Price":2024.9940}  
  }  
]  
```  
  
## 另請參閱  
 [FOR 子句 &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  