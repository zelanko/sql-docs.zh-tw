---
title: "使用 AUTO 模式自動格式化 JSON 輸出 (SQL Server) | Microsoft Docs"
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
helpviewer_keywords: 
  - "FOR JSON AUTO"
ms.assetid: 178a2a4e-e0f6-49b9-9895-396956d3c7d9
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 15
---
# 使用 AUTO 模式自動格式化 JSON 輸出 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  若要根據 **SELECT** 陳述式的結構自動格式化 JSON 輸出，請指定 **AUTO** 選項搭配 **FOR JSON** 子句。  
  
 使用 **AUTO** 選項，會根據 SELECT 清單中的資料行順序和其來源資料表自動決定 JSON 輸出格式。 您無法變更此格式。  
  
 使用 **FOR JSON AUTO** 選項的查詢必須具有 **FROM** 子句。  
  
 以下是 **FOR JSON** 子句搭配 **AUTO** 選項的一些範例。  
  
## 範例  
 **查詢 1**  
  
 如果只有一個資料表用於查詢，FOR JSON AUTO 子句的結果會類似於 FOR JSON PATH。 在此情況下，FOR JSON AUTO 不會建立巢狀物件。 唯一的差別在於會使用點產生以點分隔的別名作為索引鍵 (亦即 FOR JSON AUTO 不會使用資料行別名作為格式)。  
  
```tsql  
SELECT TOP 5   
      BusinessEntityID As Id,  
      FirstName, LastName,  
      Title As 'Info.Title',  
      MiddleName As 'Info.MiddleName'  
  FROM Person.Person  
  FOR JSON AUTO  
```  
  
 **結果 1**  
  
```json  
[  
      {"Id":1,"FirstName":"Ken","LastName":"Sánchez","Info.MiddleName":"J"},  
      {"Id":2,"FirstName":"Terri","LastName":"Duffy","Info.MiddleName":"Lee"},  
      {"Id":3,"FirstName":"Roberto","LastName":"Tamburello"},  
      {"Id":4,"FirstName":"Rob","LastName":"Walters"},  
      {"Id":5,"FirstName":"Gail","LastName":"Erickson","Info.Title":"Ms.","Info.MiddleName":"A"}  
]  
```  
  
 **查詢 2**  
  
 聯結資料表時，第一個資料表中的資料行會產生為根物件的屬性。 第二個資料表中的資料行則會產生為巢狀物件的屬性。 第二個資料表的資料表名稱或別名可作為巢狀陣列的名稱。  
  
```tsql  
SELECT TOP 2 SalesOrderNumber,  
       OrderDate,  
       UnitPrice,  
       OrderQty  
FROM Sales.SalesOrderHeader H  
  INNER JOIN Sales.SalesOrderDetail D  
    ON H.SalesOrderID = D.SalesOrderID  
FOR JSON AUTO  
```  
  
 **結果 2**  
  
```json  
[  
  {  
       "SalesOrderNumber":"SO43659",  
        "OrderDate":"2011-05-31T00:00:00",  
        "D":[  
            {"UnitPrice":24.99, "OrderQty":1  }  
         ]  
  },  
  {  
       "SalesOrderNumber":"SO43659" ,  
       "D":[  
          { "UnitPrice":34.40  },  
          { "UnitPrice":134.24, "OrderQty":5 }  
        ]  
  }  
]  
  
```  
  
## 範例 - 產生巢狀 JSON 輸出  
 除了 FOR JSON AUTO 之外，您也可以撰寫巢狀 FOR JSON 查詢，並放在使用 FOR JSON PATH 子句之主要查詢的 SELECT 部分，如下列範例所示。  
  
 **查詢 1**  
  
```tsql  
SELECT TOP 2  
   SalesOrderNumber,  
   OrderDate,  
   (SELECT UnitPrice, OrderQty  
     FROM Sales.SalesOrderDetail AS D  
     WHERE H.SalesOrderID = D.SalesOrderID  
    FOR JSON PATH) AS D  
FROM Sales.SalesOrderHeader AS H  
FOR JSON PATH  
```  
  
 **結果 1**  
  
```json  
[  
  {  
       "SalesOrderNumber":"SO43659",  
        "OrderDate":"2011-05-31T00:00:00",  
        "D":[  
            { "UnitPrice":24.99,  "OrderQty":1 }  
         ]  
  },  
  {  
       "SalesOrderNumber":"SO4390" ,  
       "D":[  
            { "UnitPrice":24.99 }  
        ]  
  }  
]  
  
```  
  
## 另請參閱  
 [FOR 子句 &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  