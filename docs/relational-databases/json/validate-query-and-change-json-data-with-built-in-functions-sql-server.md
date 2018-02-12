---
title: "使用內建函式，驗證、查詢以及變更 JSON 資料 (SQL Server) | Microsoft 文件"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c6803992992cf2a62afe741df536c0fa87a5fe2d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>使用內建函數，驗證、查詢以及變更 JSON 資料 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

內建的 JSON 支援包含下列在此主題中簡述的內建功能。  
  
-   [ISJSON](#ISJSON) 可測試字串是否包含有效的 JSON。  
  
-   [JSON_VALUE](#VALUE) 可從 JSON 字串擷取純量值。  
  
-   [JSON_QUERY](#QUERY) 可從 JSON 字串擷取物件或陣列。  
  
-   [JSON_MODIFY](#MODIFY) 可更新 JSON 字串中的屬性值，並傳回更新後的 JSON 字串。  
 
## <a name="json-text-for-the-examples-on-this-page"></a>此頁面上之範例的 JSON 文字
此頁面上的範例使用下列 JSON 文字，其中包含複雜的項目。

```sql 
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }' 
``` 

##  <a name="ISJSON"></a> 使用 ISJSON 函數來驗證 JSON 文字  
 **ISJSON** 函數可測試字串是否包含有效的 JSON。  
  
下列範例會傳回資料行 `json_col` 中包含有效 JSON 的資料列。  
  
```sql  
SELECT id, json_col
FROM tab1
WHERE ISJSON(json_col) > 0 
```  

如需詳細資訊，請參閱 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)。  
  
##  <a name="VALUE"></a> 使用 JSON_VALUE 函數，從 JSON 文字中擷取值  
**JSON_VALUE** 函數可從 JSON 字串擷取純量值。  
  
下列範例會將巢狀 JSON 屬性 `town` 的值擷取為區域變數。  
  
```sql  
SET @town = JSON_VALUE(@jsonInfo, '$.info.address.town')  
```  
  
如需詳細資訊，請參閱 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)。  
  
##  <a name="QUERY"></a> 使用 JSON_QUERY 函數，從 JSON 文字擷取物件或陣列  
**JSON_QUERY** 函數可從 JSON 字串擷取物件或陣列。  
 
下列範例示範如何在查詢結果中傳回 JSON 片段。  
  
```sql  
SELECT FirstName, LastName, JSON_QUERY(jsonInfo,'$.info.address') AS Address
FROM Person.Person
ORDER BY LastName
```  
  
如需詳細資訊，請參閱 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)。  
  
##  <a name="JSONCompare"></a> JSON_VALUE 與 JSON_QUERY 的比較  
**JSON_VALUE** 和 **JSON_QUERY** 的主要差別是 **JSON_VALUE** 傳回純量值，而 **JSON_QUERY** 傳回物件或陣列。  
  
請參考下列 JSON 文字範例：  
  
```json  
{
    "a": "[1,2]",
    "b": [1, 2],
    "c": "hi"
}  
```  
  
在這個 JSON 文字範例中，資料成員 "a" 和 "c" 為字串值，而資料成員 "b" 是陣列。 **JSON_VALUE** 和 **JSON_QUERY** 傳回下列結果︰  
  
|路徑|**JSON_VALUE** 傳回|**JSON_QUERY** 傳回|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL 或錯誤|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL 或錯誤|  
|**$.b**|NULL 或錯誤|[1,2]|  
|**$.b[0]**|@shouldalert|NULL 或錯誤|  
|**$.c**|hi|NULL 或錯誤|  
  
## <a name="test-jsonvalue-and-jsonquery-with-the-adventureworks-sample-database"></a>使用 AdventureWorks 範例資料庫，測試 JSON_VALUE 與 JSON_QUERY  
依據本主題中所述，使用 AdventureWorks 範例資料庫，執行下列範例，以測試內建函式。 如需何處取得 AdventureWorks 及如何新增 JSON 資料以供測試的資訊，請參閱[測試磁碟機內建的 JSON 支援](json-data-sql-server.md#test-drive-built-in-json-support-with-the-adventureworks-sample-database)。
  
在下列範例中，`SalesOrder_json`資料表中的 `Info` 資料行包含 JSON 文字。  
  
### <a name="example-1---return-both-standard-columns-and-json-data"></a>範例 1 - 傳回標準的資料行和 JSON 資料  
下列查詢會傳回來自標準關聯式資料行及 JSON 資料行的值。  
  
```sql  
SELECT SalesOrderNumber, OrderDate, Status, ShipDate, Status, AccountNumber, TotalDue,
 JSON_QUERY(Info,'$.ShippingInfo') ShippingInfo,
 JSON_QUERY(Info,'$.BillingInfo') BillingInfo,
 JSON_VALUE(Info,'$.SalesPerson.Name') SalesPerson,
 JSON_VALUE(Info,'$.ShippingInfo.City') City,
 JSON_VALUE(Info,'$.Customer.Name') Customer,
 JSON_QUERY(OrderItems,'$') OrderItems
FROM Sales.SalesOrder_json
WHERE ISJSON(Info) > 0
```  
  
### <a name="example-2--aggregate-and-filter-json-values"></a>範例 2 - 彙總並篩選 JSON 值  
下列查詢會依據客戶名稱和狀態來彙總小計 (客戶名稱是儲存在 JSON 中，而狀態是儲存在一般資料行中)。 然後依縣市 (儲存在 JSON 中) 及 OrderDate (儲存在一般資料行中) 篩選結果。  
  
```sql  
DECLARE @territoryid INT;
DECLARE @city NVARCHAR(32);

SET @territoryid=3;

SET @city=N'Seattle';

SELECT JSON_VALUE(Info, '$.Customer.Name') AS Customer, Status, SUM(SubTotal) AS Total
FROM Sales.SalesOrder_json
WHERE TerritoryID=@territoryid
 AND JSON_VALUE(Info, '$.ShippingInfo.City') = @city
 AND OrderDate > '1/1/2015'
GROUP BY JSON_VALUE(Info, '$.Customer.Name'), Status
HAVING SUM(SubTotal)>1000
```  
  
##  <a name="MODIFY"></a> 使用 JSON_MODIFY 函數來更新 JSON 文字中的屬性值  
**JSON_MODIFY** 函式會更新 JSON 字串中屬性的值，並傳回更新的 JSON 字串。  
  
下列範例會更新包含 JSON 的變數中，JSON 屬性的值。  
  
```sql  
SET @info = JSON_MODIFY(@jsonInfo, "$.info.address[0].town", 'London')    
```  
  
 如需詳細資訊，請參閱 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)。  
  
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>深入了解 SQL Server 和 Azure SQL Database 中的 JSON  
  
### <a name="microsoft-blog-posts"></a>Microsoft 部落格文章  
  
如需特定的解決方案、使用案例和建議，請參閱這些[部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)，了解 SQL Server 和 Azure SQL Database 中的內建 JSON 支援。  

### <a name="microsoft-videos"></a>Microsoft 影片

如需 SQL Server 和 Azure SQL Database 中內建 JSON 支援的觀看式簡介，請參閱下列影片：

-   [SQL Server 2016 與 JSON 支援](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [使用 SQL Server 2016 和 Azure SQL Database 中的 JSON](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL 與關聯式領域之間的橋樑 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>另請參閱  
 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)   
 [JSON 路徑運算式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  
