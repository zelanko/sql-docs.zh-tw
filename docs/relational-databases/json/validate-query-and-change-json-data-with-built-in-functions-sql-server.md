---
title: 使用內建函數，驗證、查詢以及變更 JSON 資料
ms.date: 07/17/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ddc5fb198a62374fc43ebacb5fa7423ac9fadd5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "74096070"
---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>使用內建函數，驗證、查詢以及變更 JSON 資料 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

內建的 JSON 支援包含下列在此主題中簡述的內建功能。  
  
-   [ISJSON](#ISJSON) 可測試字串是否包含有效的 JSON。  
  
-   [JSON_VALUE](#VALUE) 可從 JSON 字串擷取純量值。  
  
-   [JSON_QUERY](#QUERY) 可從 JSON 字串擷取物件或陣列。  
  
-   [JSON_MODIFY](#MODIFY) 可更新 JSON 字串中的屬性值，並傳回更新後的 JSON 字串。  
 
## <a name="json-text-for-the-examples-on-this-page"></a>此頁面上之範例的 JSON 文字

此頁面上範例會使用類似於下列範例中所示內容的 JSON 文字：

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller",
         "givenName": "Lisa",
         "gender": "female",
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

此 JSON 文件 (包含巢狀複雜元素) 儲存在下列範例資料表中：

```sql
CREATE TABLE Families (
   id int identity constraint PK_JSON_ID primary key,
   doc nvarchar(max)
)
``` 

##  <a name="ISJSON"></a> 使用 ISJSON 函數來驗證 JSON 文字  
 **ISJSON** 函數可測試字串是否包含有效的 JSON。  
  
下列範例會傳回 JSON 資料行包含有效 JSON 文字的資料列。 請注意，如果沒有明確的 JSON 限制，您可以在 NVARCHAR 資料行中輸入任何文字：  
  
```sql  
SELECT *
FROM Families
WHERE ISJSON(doc) > 0 
```  

如需詳細資訊，請參閱 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)。  
  
##  <a name="VALUE"></a> 使用 JSON_VALUE 函數，從 JSON 文字中擷取值  
**JSON_VALUE** 函數可從 JSON 字串擷取純量值。 下列查詢會傳回 `id` JSON 欄位符合值 `AndersenFamily` 且依據 `city` 和 `state` JSON 欄位排序的文件：

```sql  
SELECT JSON_VALUE(f.doc, '$.id')  AS Name, 
       JSON_VALUE(f.doc, '$.address.city') AS City,
       JSON_VALUE(f.doc, '$.address.county') AS County
FROM Families f 
WHERE JSON_VALUE(f.doc, '$.id') = N'AndersenFamily'
ORDER BY JSON_VALUE(f.doc, '$.address.city') DESC, JSON_VALUE(f.doc, '$.address.state') ASC
```  

下表顯示此查詢的結果：

| 名稱 | City | 郡/縣 |
| --- | --- | --- |
| AndersenFamily | NY | Manhattan |

如需詳細資訊，請參閱 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)。  
  
##  <a name="QUERY"></a> 使用 JSON_QUERY 函數，從 JSON 文字擷取物件或陣列  

**JSON_QUERY** 函數可從 JSON 字串擷取物件或陣列。 下列範例示範如何在查詢結果中傳回 JSON 片段。  
  
```sql
SELECT JSON_QUERY(f.doc, '$.address') AS Address,
       JSON_QUERY(f.doc, '$.parents') AS Parents,
       JSON_QUERY(f.doc, '$.parents[0]') AS Parent0
FROM Families f 
WHERE JSON_VALUE(f.doc, '$.id') = N'AndersenFamily'
```  
下表顯示此查詢的結果：

| 位址 | Parents | Parent0 |
| --- | --- | --- |
| { "state":"NY", "county":"Manhattan", "city":"NY" } | [{ "familyName":"Wakefield", "givenName":"Robin" }, {"familyName":"Miller", "givenName":"Ben" } ]| { "familyName":"Wakefield", "givenName":"Robin" } |

如需詳細資訊，請參閱 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)。  

## <a name="parse-nested-json-collections"></a>剖析巢狀 JSON 集合

`OPENJSON` 函式可讓您將 JSON 子陣列轉換成資料列集，然後將其與父元素聯結。 例如，您可以傳回所有家族文件，並將其與儲存為內部 JSON 陣列的 `children` 物件「聯結」：

```sql
SELECT JSON_VALUE(f.doc, '$.id')  AS Name, 
       JSON_VALUE(f.doc, '$.address.city') AS City,
       c.givenName, c.grade
FROM Families f
        CROSS APPLY OPENJSON(f.doc, '$.children')
            WITH(grade int, givenName nvarchar(100))  c
```

下表顯示此查詢的結果：

| 名稱 | City | givenName | grade |
| --- | --- | --- | --- |
| AndersenFamily | NY | Jesse | 1 |
| AndersenFamily | NY | Lisa | 8 |

我們會取得兩個資料列，因為一個父資料列已聯結兩個子資料列，而這兩個子資料列是由剖析 children 子陣列的兩個元素所產生。 `OPENJSON` 函式會剖析 `doc` 資料行中的 `children` 片段，並以一組資料列形式傳回每個元素的 `grade` 和 `givenName`。 這個資料列集可以與父文件聯結。
 
## <a name="query-nested-hierarchical-json-sub-arrays"></a>查詢巢狀階層式 JSON 子陣列

您可以套用多個 `CROSS APPLY OPENJSON` 呼叫，以便查詢巢狀 JSON 結構。 此範例中所使用 JSON 文件具有稱為 `children` 的巢狀陣列，其中每個兒童都有 `pets` 的巢狀陣列。 下列查詢會剖析每個文件的 children，將每個陣列物件傳回為資料列，然後剖析 `pets` 陣列：

```sql
SELECT  familyName,
    c.givenName AS childGivenName,
    c.firstName AS childFirstName,
    p.givenName AS petName 
FROM Families f 
    CROSS APPLY OPENJSON(f.doc) 
        WITH (familyName nvarchar(100), children nvarchar(max) AS JSON)
        CROSS APPLY OPENJSON(children) 
        WITH (givenName nvarchar(100), firstName nvarchar(100), pets nvarchar(max) AS JSON) as c
            OUTER APPLY OPENJSON (pets)
            WITH (givenName nvarchar(100))  as p
```

第一個 `OPENJSON` 呼叫會使用 AS JSON 子句傳回 `children` 陣列的片段。 此陣列片段將提供給第二個 `OPENJSON` 函式，該函式會傳回每個兒童的 `givenName`、`firstName`，以及 `pets` 的陣列。 `pets` 的陣列將提供給第三個 `OPENJSON` 函式，此函式會傳回寵物的 `givenName`。
下表顯示此查詢的結果：

| familyName | childGivenName | childFirstName | petName |
| --- | --- | --- | --- |
| AndersenFamily | Jesse | Merriam | Goofy |
| AndersenFamily | Jesse | Merriam | Shadow |
| AndersenFamily | Lisa | Miller| `NULL` |

根文件會與第一個 `OPENJSON(children)` 呼叫所傳回的兩個 `children` 資料列聯結，形成兩個資料列 (或元組)。 然後，每個資料列會與 `OPENJSON(pets)` 使用 `OUTER APPLY` 運算子所產生的新資料列聯結。 Jesse 有兩隻寵物，因此 `(AndersenFamily, Jesse, Merriam)` 會與針對 Goofy 和 Shadow 產生的兩個資料列聯結。 Lisa 沒有寵物，因此這個元組沒有 `OPENJSON(pets)` 傳回的任何資料列。 不過，因為我們使用 `OUTER APPLY`，所以將在資料行中取得 `NULL`。 如果我們使用 `CROSS APPLY` 而不是 `OUTER APPLY`，則結果中不會傳回 Lisa，因為沒有任何可與這個元組聯結的寵物資料列。

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
  
|Path|**JSON_VALUE** 傳回|**JSON_QUERY** 傳回|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL 或錯誤|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL 或錯誤|  
|**$.b**|NULL 或錯誤|[1,2]|  
|**$.b[0]**|1|NULL 或錯誤|  
|**$.c**|hi|NULL 或錯誤|  
  
## <a name="test-json_value-and-json_query-with-the-adventureworks-sample-database"></a>使用 AdventureWorks 範例資料庫，測試 JSON_VALUE 與 JSON_QUERY  
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
  
### <a name="microsoft-videos"></a>Microsoft 影片

如需 SQL Server 和 Azure SQL Database 中內建 JSON 支援的觀看式簡介，請參閱下列影片：

-   [SQL Server 2016 和 JSON 支援](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [使用 SQL Server 2016 和 Azure SQL Database 中的 JSON](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL 與關聯式領域之間的橋樑 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>另請參閱  
 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)   
 [JSON 路徑運算式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  
