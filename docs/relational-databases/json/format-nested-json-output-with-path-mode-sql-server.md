---
description: 以 PATH 模式格式化巢狀的 JSON 輸出 (SQL Server)
title: 以 PATH 模式格式化巢狀的 JSON 輸出
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c091618be5e414faa15e200fc8b30230f793eaf
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96130248"
---
# <a name="format-nested-json-output-with-path-mode-sql-server"></a>以 PATH 模式格式化巢狀的 JSON 輸出 (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

若要保有 **FOR JSON** 子句輸出的完整控制權，請指定 **PATH** 選項。  
  
**PATH** 模式讓您建立包裝函式物件和巢狀複雜屬性。 結果會格式化為 JSON 物件陣列。  
  
替代方法是使用 **AUTO** 選項，以根據 **SELECT** 陳述式的結構自動格式化輸出。
 -   如需 **AUTO** 選項的詳細資訊，請參閱 [使用 AUTO 模式自動格式化 JSON 輸出](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)。
 -   如需這兩個選項的概觀，請參閱[使用 FOR JSON 將查詢結果格式化為 JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)。
 
以下是 **FOR JSON** 子句搭配 **PATH** 選項的一些範例。 使用點分隔資料行名稱，或使用巢狀查詢格式化巢狀結果，如下例所示。 根據預設，null 值不會包含在 **FOR JSON** 輸出中。  [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) 是 JSON 查詢的建議使用查詢編輯器，因為此編輯器會自動格式化 JSON 結果 (如本文所示)，而非顯示一般字串。

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
SELECT TOP 2 H.SalesOrderNumber AS 'Order.Number',  
        H.OrderDate AS 'Order.Date',  
        D.UnitPrice AS 'Product.Price',  
        D.OrderQty AS 'Product.Quantity'  
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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>深入了解 SQL Server 和 Azure SQL Database 中的 JSON  
  
### <a name="microsoft-videos"></a>Microsoft 影片

如需 SQL Server 和 Azure SQL Database 中內建 JSON 支援的觀看式簡介，請參閱下列影片：

-   [SQL Server 2016 和 JSON 支援](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [使用 SQL Server 2016 和 Azure SQL Database 中的 JSON](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL 與關聯式領域之間的橋樑 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)

## <a name="see-also"></a>另請參閱  
 [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
