---
title: "使用內建函數，驗證、查詢以及變更 JSON 資料 (SQL Server) | Microsoft Docs"
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
  - "JSON, 內建函數"
  - "函數 (JSON)"
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
caps.latest.revision: 21
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# 使用內建函數，驗證、查詢以及變更 JSON 資料 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  內建 JSON 支援包含本主題說明的下列內建函數。  
  
-   [ISJSON](#ISJSON) 可測試字串是否包含有效的 JSON。  
  
-   [JSON_VALUE](#VALUE) 可從 JSON 字串擷取純量值。  
  
-   [JSON_QUERY](#QUERY) 可從 JSON 字串擷取物件或陣列。  
  
-   [JSON_MODIFY](#MODIFY) 可更新 JSON 字串中的屬性值，並傳回更新後的 JSON 字串。  
  
##  <a name="ISJSON"></a> 使用 ISJSON 函數來驗證 JSON 文字  
 **ISJSON** 函數可測試字串是否包含有效的 JSON。  
  
 下列範例會在資料行包含有效的 JSON 時，傳回 JSON 文字。  
  
```tsql  
SELECT id, json_col  
FROM tab1  
WHERE ISJSON(json_col) > 0  
```  
  
 如需詳細資訊，請參閱 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)。  
  
##  <a name="VALUE"></a> 使用 JSON_VALUE 函數，從 JSON 文字中擷取值  
 **JSON_VALUE** 函數可從 JSON 字串擷取純量值。  
  
 下列範例會將 JSON 屬性的值擷取到區域變數中。  
  
```tsql  
SET @town = JSON_VALUE(@jsonInfo, '$.info.address.town')  
```  
  
 如需詳細資訊，請參閱 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)。  
  
##  <a name="QUERY"></a> 使用 JSON_QUERY 函數，從 JSON 文字擷取物件或陣列  
 **JSON_QUERY** 函數可從 JSON 字串擷取物件或陣列。  
  
 請參考下列包含複雜元素的 JSON 文字範例。  
  
```json  
DECLARE @jsonInfo VARCHAR(MAX)  
SET @jsonInfo = N'{  
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
  
 下列範例示範如何在查詢結果中傳回 JSON 片段。  
  
```tsql  
SELECT FirstName, LastName,   
       JSON_QUERY(jsonInfo, '$.info.address') AS Address  
FROM Person.Person  
ORDER BY LastName  
```  
  
 如需詳細資訊，請參閱 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)。  
  
##  <a name="JSONCompare"></a> JSON_VALUE 與 JSON_QUERY 的比較  
 **JSON_VALUE** 和 **JSON_QUERY** 的主要差別是 **JSON_VALUE** 傳回純量值，而 **JSON_QUERY** 傳回物件或陣列。  
  
 請參考下列 JSON 文字範例：  
  
```json  
{ "a": "[1,2]", "b": [1,2], "c": "hi" }  
```  
  
 在這個 JSON 文字範例中，資料成員 "a" 和 "c" 為字串值，而資料成員 "b" 是陣列。 **JSON_VALUE** 和 **JSON_QUERY** 傳回下列結果︰  
  
|查詢|**JSON_VALUE** 傳回|**JSON_QUERY** 傳回|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL 或錯誤|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL 或錯誤|  
|**$.b**|NULL 或錯誤|[1,2]|  
|**$.b[0]**|1|NULL 或錯誤|  
|**$.c**|hi|NULL 或錯誤|  
  
## 使用 AdventureWorks 範例資料庫，測試 JSON_VALUE 與 JSON_QUERY  
 依據本主題中所述，使用 AdventureWorks 範例資料庫，執行下列範例 (其中包含 JSON 資料)，以測試內建函數。 若要取得 AdventureWorks 範例資料庫，請 [按一下此處](http://www.microsoft.com/en-us/download/details.aspx?id=49502)。  
  
 在下列範例中，SalesOrder_json 資料表中的「資訊」資料行包含 JSON 文字。  
  
### 範例 1 - 傳回標準的資料行和 JSON 資料  
 下列查詢會傳回標準的關聯式資料行和來自 JSON 資料行的值。  
  
```tsql  
SELECT SalesOrderNumber, OrderDate, Status, ShipDate, Status, AccountNumber, TotalDue,  
             JSON_QUERY(Info, '$.ShippingInfo') ShippingInfo,  
             JSON_QUERY(Info, '$.BillingInfo') BillingInfo,  
             JSON_VALUE(Info, '$.SalesPerson.Name') SalesPerson,  
             JSON_VALUE(Info, '$.ShippingInfo.City') City,  
             JSON_VALUE(Info, '$.Customer.Name') Customer,  
             JSON_QUERY(OrderItems, '$') OrderItems  
FROM Sales.SalesOrder_json  
WHERE ISJSON(Info) > 0  
  
```  
  
### 範例 2 - 彙總並篩選 JSON 值  
 下列查詢會依據客戶名稱和狀態來彙總小計 (客戶名稱是儲存在 JSON 中，而狀態是儲存在一般資料行中)。 然後它會依據縣/市和 OrderDate 來篩選結果 (縣/市是儲存在 JSON 中，而 OrderDate 是儲存在一般資料行中)。  
  
```tsql  
SELECT JSON_VALUE(Info, '$.Customer.Name') AS Customer, Status, SUM(SubTotal) AS Total  
FROM Sales.SalesOrder_json  
WHERE TerritoryID = @territoryid  
AND JSON_VALUE(Info, '$.ShippingInfo.City') = @city  
AND OrderDate > '1/1/2015'  
GROUP BY JSON_VALUE(Info, '$.Customer.Name'), Status  
HAVING SUM(SubTotal) > 1000  
  
```  
  
##  <a name="MODIFY"></a> 使用 JSON_MODIFY 函數來更新 JSON 文字中的屬性值  
 **JSON_MODIFY** 函數可更新 JSON 字串中的屬性值，並傳回更新後的 JSON 字串。  
  
 下列範例會在包含 JSON 的變數中更新屬性的值。  
  
```tsql  
SET @info = JSON_MODIFY(@jsonInfo, "$.info.address[0].town", 'London')  
```  
  
 如需詳細資訊，請參閱 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)。  
  
## 深入了解 SQL Server 內建的 JSON 支援  
 [Microsoft 專案經理 Jovan Popovic 的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## 另請參閱  
 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)   
 [JSON 路徑運算式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  