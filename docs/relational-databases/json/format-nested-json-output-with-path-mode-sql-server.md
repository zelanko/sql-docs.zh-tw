---
title: "以 PATH 模式格式化巢狀的 JSON 輸出 (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 1aa87e3d821e6d111948baa0843edf31d087d739
ms.openlocfilehash: 3fc86f957f4ece3564d8f72558467cdf6c54c935
ms.contentlocale: zh-tw
ms.lasthandoff: 07/18/2017

---
# <a name="format-nested-json-output-with-path-mode-sql-server"></a>以 PATH 模式格式化巢狀的 JSON 輸出 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

若要保有 **FOR JSON** 子句輸出的完整控制權，請指定 **PATH** 選項。  
  
**PATH** 模式讓您建立包裝函式物件和巢狀複雜屬性。 結果會格式化為 JSON 物件陣列。  
  
替代方法是使用 **AUTO** 選項，以根據 **SELECT** 陳述式的結構自動格式化輸出。
 -   如需 **AUTO** 選項的詳細資訊，請參閱[使用 AUTO 模式自動格式化 JSON 輸出](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)。
 -   如需這兩個選項的概觀，請參閱[使用 FOR JSON 將查詢結果格式化為 JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)。
 
以下是 **FOR JSON** 子句搭配 **PATH** 選項的一些範例。 使用點分隔資料行名稱，或使用巢狀查詢格式化巢狀結果，如下例所示。 根據預設，null 值不會包含在 **FOR JSON**輸出中。  

## <a name="example---dot-separated-column-names"></a>範例 - 點分隔資料行名稱  
下列查詢會將 AdventureWorks `Person` 資料表中的前五個資料列格式化為 JSON。  

**FOR JSON PATH** 子句會使用資料行別名或資料行名稱判斷 JSON 輸出中的索引鍵名稱。 如果別名包含點，PATH 選項會建立巢狀物件。  

 **查詢**  
  
```sql  
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
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sanchez",
    "Info": {
        "MiddleName": "J"
    }
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info": {
        "MiddleName": "Lee"
    }
}, {
    "Id": 3,
    "FirstName": "Roberto",
    "LastName": "Tamburello"
}, {
    "Id": 4,
    "FirstName": "Rob",
    "LastName": "Walters"
}, {
    "Id": 5,
    "FirstName": "Gail",
    "LastName": "Erickson",
    "Info": {
        "Title": "Ms.",
        "MiddleName": "A"
    }
}]
```  
   
## <a name="example---multiple-tables"></a>範例 - 多份資料表  
如果在查詢中參考多個資料表，則 **FOR JSON PATH** 會使用別名來巢狀處理每個資料行。 下列查詢會為在查詢中聯結的每組 (OrderHeader, OrderDetails) 建立一個 JSON 物件。 
  
 **查詢**  
  
```sql  
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
[{
    "Order": {
        "Number": "SO43659",
        "Date": "2011-05-31T00:00:00"
    },
    "Product": {
        "Price": 2024.9940,
        "Quantity": 1
    }
}, {
    "Order": {
        "Number": "SO43659"
    },
    "Product": {
        "Price": 2024.9940
    }
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>深入了解內建 JSON 支援 SQL Server 中  
針對特定的解決方案，大量使用案例和建議，請參閱[有關內建 JSON 支援的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)Microsoft 經理專案 jovan popovic 的 Azure SQL Database 和 SQL Server 中。

## <a name="see-also"></a>另請參閱  
 [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  

