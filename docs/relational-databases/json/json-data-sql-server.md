---
title: 使用 SQL Server 中的 JSON | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2019
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: quickstart
helpviewer_keywords:
- JSON
- JSON, built-in support
ms.assetid: c9a4e145-33c3-42b2-a510-79813e67806a
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||= azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fc0abe6cb47bff38fd7f8fa63852d6042b9ee9c1
ms.sourcegitcommit: 39630fddc69141531eddca2a3c156ccf8536f49c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72928460"
---
# <a name="json-data-in-sql-server"></a>SQL Server 中的 JSON 資料

[!INCLUDE[appliesto-ss2016-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

JSON 是種熱門的文字資料格式，用於在新式 Web 和行動應用程式中交換資料。 其也可用於將非結構化的資料儲存在記錄檔或是類似 Microsoft Azure Cosmos DB 的 NoSQL 資料庫中。 許多 REST Web 服務會傳回已格式化為 JSON 文字的結果，或接受已格式化為 JSON 的資料。 例如，大部分的 Azure 服務 (例如 Azure 搜尋服務、Azure 儲存體和 Azure Cosmos DB) 都具有傳回或取用 JSON 的 REST 端點。 JSON 也是用於透過 AJAX 呼叫在網頁和 Web 伺服器之間交換資料的主要格式。 

SQL Server 中的 JSON 函數可讓您將 NoSQL 與關聯式概念結合在同一個資料庫中。 現在，您可以將傳統關聯式資料行與包含採用 JSON 文字格式之文件的資料行結合在同一個資料表中、剖析並匯入關聯式結構中的 JSON 文件，或讓關聯式資料採用 JSON 文字格式。 在下列影片中，您將了解在 SQL Server 和 Azure SQL Database 中，JSON 函式如何連接關聯式與 NoSQL 概念：

*NoSQL 與關聯式領域之間的橋樑 JSON*
> [!VIDEO https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds/player]

以下是 JSON 文字範例︰

```json
[
  {
    "name": "John",
    "skills": ["SQL", "C#", "Azure"]
  },
  {
    "name": "Jane",
    "surname": "Doe"
  }
]
```

您可使用 SQL Server 內建函式和運算子，以 JSON 文字執行下列作業：

- 剖析 JSON 文字，並讀取或修改值。  
- 將 JSON 物件的陣列轉換成資料表格式。  
- 在已轉換的 JSON 物件上執行任何 Transact SQL 查詢。  
- 以 JSON 格式格式化 Transact-SQL 查詢的結果。  
  
![內建 JSON 支援概觀](../../relational-databases/json/media/jsonslides1overview.png "內建 JSON 支援概觀")  
  
## <a name="key-json-capabilities-of-sql-server-and-sql-database"></a>SQL Server 和 SQL Database 的主要 JSON 功能

下一節說明 SQL Server 以內建 JSON 支援提供的主要功能。 在下列影片中，您可以了解如何使用 JSON 函數和運算子：

*SQL Server 2016 和 JSON 支援*
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support/player]

### <a name="extract-values-from-json-text-and-use-them-in-queries"></a>從 JSON 文字中擷取值，然後在查詢中使用它們

如有儲存在資料庫資料表中的 JSON 文字，您可以使用下列內建函式來讀取或修改 JSON 文字中的值：  

- [ISJSON (Transact-SQL)](../../t-sql/functions/isjson-transact-sql.md) 可測試字串是否包含有效的 JSON。
- [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md) 可從 JSON 字串擷取純量值。
- [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md) 可從 JSON 字串擷取物件或陣列。
- [JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md) 變更 JSON 字串中的值。

**範例**

在下列範例中，查詢會使用來自資料表的關聯式資料和 JSON 資料 (儲存在名為 `jsonCol` 的資料行中)：  
  
```sql  
SELECT Name, Surname,
  JSON_VALUE(jsonCol, '$.info.address.PostCode') AS PostCode,
  JSON_VALUE(jsonCol, '$.info.address."Address Line 1"') + ' '
  + JSON_VALUE(jsonCol, '$.info.address."Address Line 2"') AS Address,
  JSON_QUERY(jsonCol, '$.info.skills') AS Skills
FROM People
WHERE ISJSON(jsonCol) > 0
  AND JSON_VALUE(jsonCol, '$.info.address.Town') = 'Belgrade'
  AND Status = 'Active'
ORDER BY JSON_VALUE(jsonCol, '$.info.address.PostCode')
```  
  
應用程式和工具分辨不出從純量資料表資料行取得的值和從 JSON 資料行取得的值有何不同。 您可以在 Transact-SQL 查詢的任意部分 (包括 WHERE、ORDER BY 或 GROUP BY 子句、範圍彙總等等)，使用來自 JSON 文字的值。 JSON 函式會使用類似 JavaScript 的語法來參考 JSON 文字內的值。

如需詳細資訊，請參閱[使用內建函式驗證、查詢及變更 JSON 資料 (SQL Server)](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)、[JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md) 和 [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)。  
  
### <a name="change-json-values"></a>變更 JSON 值

如果您必須修改部分 JSON 文字，可以使用 [JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md) 函式來更新 JSON 字串中的屬性值，並傳回更新的 JSON 字串。 下列範例示範在包含 JSON 的變數中更新屬性的值：  
  
```sql
DECLARE @json NVARCHAR(MAX);
SET @json = '{"info": {"address": [{"town": "Belgrade"}, {"town": "Paris"}, {"town":"Madrid"}]}}';
SET @json = JSON_MODIFY(@json, '$.info.address[1].town', 'London');
SELECT modifiedJson = @json;
```

**結果**

|modifiedJson|  
|--------|  
|{"info":{"address":[{"town":"Belgrade"},{"town":"London"},{"town":"Madrid"}]}|  
  
### <a name="convert-json-collections-to-a-rowset"></a>將 JSON 集合轉換為資料列集

您不需要自訂查詢語言也能在 SQL Server 中查詢 JSON。 您可以使用標準的 T-SQL 查詢 JSON 資料。 如果您必須建立 JSON 資料的查詢或報表，可以呼叫 **OPENJSON** 資料列集函式，輕鬆地將 JSON 資料轉換成資料列和資料行。 如需詳細資訊，請參閱[使用 OPENJSON 將 JSON 資料轉換成資料列和資料行 (SQL Server)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)。  
  
下列範例示範呼叫 **OPENJSON**，並將儲存於 `@json` 變數中的物件陣列轉換為可使用標準 SQL **SELECT** 陳述式查詢的資料列集︰  
  
```sql  
DECLARE @json NVARCHAR(MAX);
SET @json = N'[
  {"id": 2, "info": {"name": "John", "surname": "Smith"}, "age": 25},
  {"id": 5, "info": {"name": "Jane", "surname": "Smith"}, "dob": "2005-11-04T12:00:00"}
]';

SELECT *
FROM OPENJSON(@json)
  WITH (
    id INT 'strict $.id',
    firstName NVARCHAR(50) '$.info.name',
    lastName NVARCHAR(50) '$.info.surname',
    age INT,
    dateOfBirth DATETIME2 '$.dob'
  );
```

**結果**

|ID|firstName|lastName|age|dateOfBirth|  
|--------|---------------|--------------|---------|-----------------|  
|2|John|Smith|25||  
|5|Jane|Smith||2005-11-04T12:00:00|  
  
**OPENJSON** 會將 JSON 物件的陣列將轉換為資料表，每個物件顯示為一個資料列，而索引鍵/值組會以資料格形式傳回。 輸出會遵循下列規則：

- **OPENJSON** 將 JSON 值轉換為 **WITH** 子句中指定的類型。
- **OPENJSON** 可以處理單層式金鑰值組和巢狀階層組織的物件。
- 您不必傳回 JSON 文字包含的所有欄位。
- 如果 JSON 值不存在，**OPENJSON** 會傳回 NULL 值。
- 您可以選擇在類型規格之後指定路徑，以參考巢狀的屬性或參考不同名稱的屬性。
- JSON 文字中必須有在路徑中指定指定屬性值的選擇性 **嚴格** 前置詞。

如需詳細資訊，請參閱[使用 OPENJSON 將 JSON 資料轉換成資料列和資料行 (SQL Server)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md) 和 [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)。  

JSON 文件可能會有不能直接對應到標準關聯式資料行的子項目和階層式資料。 在此情況下，您可以藉由聯結父實體和子陣列來壓平合併 JSON 階層。

在下列範例中，陣列中的第二個物件具有代表人員技能的子陣列。 每個子物件都可以使用其他 `OPENJSON` 函式呼叫加以剖析：

```sql  
DECLARE @json NVARCHAR(MAX);
SET @json = N'[  
  {"id": 2, "info": {"name": "John", "surname": "Smith"}, "age": 25},
  {"id": 5, "info": {"name": "Jane", "surname": "Smith", "skills": ["SQL", "C#", "Azure"]}, "dob": "2005-11-04T12:00:00"}  
]';

SELECT *  
FROM OPENJSON(@json)  
  WITH (
    id INT 'strict $.id',
    firstName NVARCHAR(50) '$.info.name',
    lastName NVARCHAR(50) '$.info.surname',  
    age INT,
    dateOfBirth DATETIME2 '$.dob',
    skills NVARCHAR(MAX) '$.info.skills' AS JSON
  )
OUTER APPLY OPENJSON(skills)
  WITH (skill NVARCHAR(8) '$');
```

第一個 `OPENJSON` 傳回的 **skills** 陣列作為原始的 JSON 文字片段，並使用 `APPLY` 運算子傳遞給另一個 `OPENJSON` 函式。 第二個 `OPENJSON` 函式會剖析 JSON 陣列並傳回字串值作為單一資料行資料列集，與第一個 `OPENJSON` 的結果聯結。
下表顯示此查詢的結果：

**結果**

|ID|firstName|lastName|age|dateOfBirth|skill|  
|--------|---------------|--------------|---------|-----------------|----------|  
|2|John|Smith|25|||  
|5|Jane|Smith||2005-11-04T12:00:00|SQL|
|5|Jane|Smith||2005-11-04T12:00:00|C#|
|5|Jane|Smith||2005-11-04T12:00:00|Azure|

`OUTER APPLY OPENJSON` 會聯結第一個層級的實體和子陣列，並傳回壓平合併的結果集。 因為「聯結」的緣故，每個技能都會重複第二個資料列。

### <a name="convert-sql-server-data-to-json-or-export-json"></a>將 SQL Server 資料轉換為 JSON 或匯出 JSON

>[!NOTE]
>目前不支援將 Azure SQL 資料倉儲資料轉換成 JSON 或匯出 JSON。

將 **FOR JSON** 子句加入至 **SELECT** 陳述式，以將 SQL Server 資料或 SQL 查詢結果格式化為 JSON。 使用 **FOR JSON** 將您用戶端應用程式的 JSON 輸出格式設定委派給 SQL Server。 如需詳細資訊，請參閱[使用 FOR JSON 將查詢結果格式化為 JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)。  
  
下列範例示範搭配 **FOR JSON** 子句使用 PATH 模式：  
  
```sql  
SELECT id, firstName AS "info.name", lastName AS "info.surname", age, dateOfBirth AS dob
FROM People
FOR JSON PATH;
```

星期 **FOR JSON** 子句會將 SQL 結果格式化為 JSON 文字，提供給任何了解 JSON 的應用程式。 PATH 選項會在 SELECT 子句中使用點分隔的別名，巢狀化查詢結果中的物件。  
  
**結果**

```json  
[
  {
    "id": 2,
    "info": {
      "name": "John",
      "surname": "Smith"
    },
    "age": 25
  },
  {
    "id": 5,
    "info": {
      "name": "Jane",
      "surname": "Smith"
    },
    "dob": "2005-11-04T12:00:00"
  }
]
```  
  
如需詳細資訊，請參閱[使用 FOR JSON 將查詢結果格式化為 JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md) 和 [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)。  

## <a name="use-cases-for-json-data-in-sql-server"></a>SQL Server 中 JSON 資料的使用案例

SQL Server 與 Azure SQL Database 中的 JSON 支援，可讓您能結合關聯式概念與 NoSQL 概念。 您可以輕鬆地將關聯式資料轉換為半結構化的資料，反之亦然。 但 JSON 並非取代現有的關聯式模型。 以下是一些受益於 SQL Server 與 SQL Database 中 JSON 支援的特定使用案例。

### <a name="simplify-complex-data-models"></a>簡化複雜的資料模型

請考慮將您的資料模型去除正規化，用 JSON 欄位來取代多個子資料表。

### <a name="store-retail-and-e-commerce-data"></a>儲存零售及電子商務資料

將具有各式各樣變化特質的產品相關資訊，儲存在非正規化模型中以保留彈性。

### <a name="process-log-and-telemetry-data"></a>處理記錄檔與遙測資料

載入、查詢及分析儲存為 JSON 檔案的記錄資料，同時具備 TRANSACT-SQL 語言的所有功能。

### <a name="store-semi-structured-iot-data"></a>儲存半結構化的 IoT 資料

當您需要即時的 IoT 資料分析時，請將內送資料直接載入資料庫，而非將其暫置於儲存體位置。

### <a name="simplify-rest-api-development"></a>簡化 REST API 開發

輕鬆地將您資料庫中的關聯式資料，轉換為支援您的網站之 REST API 所使用的 JSON 格式。

## <a name="combine-relational-and-json-data"></a>合併關聯式資料和 JSON 資料

SQL Server 提供混合模型，讓您使用標準 Transact-SQL 語言儲存兼處理關聯式與 JSON 資料。 您可以使用完整的 Transact-SQL 在資料表中組織 JSON 文件的集合、建立它們之間的關聯性、結合儲存於資料表中的強類型純量資料行和儲存於 JSON 資料行中的彈性索引鍵/值組，以及在一或多個資料表中查詢純量和 JSON 值。

JSON 文字儲存在 `VARCHAR` 或 `NVARCHAR` 資料行中，並以純文字建立索引。 任何支援文字的 SQL Server 功能或元件都支援 JSON，因此 JSON 和其他 SQL Server 功能之間幾乎沒有任何互動限制。 您可以將 JSON 儲存在記憶體內部或時態表中、在 JSON 文字上套用資料列層級安全性的述詞等。

如果您有想要在其中使用專為處理 JSON 文件而設定之查詢語言的 JSON 工作負載，請考慮使用 Microsoft Azure [Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)。  
  
以下提供數個使用案例，示範如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中使用內建的 JSON 支援。  

## <a name="store-and-index-json-data-in-sql-server"></a>在 SQL Server 中儲存 JSON 資料並編製索引

JSON 是文字格式，因此 JSON 文件都可以儲存在 SQL Database 的 `NVARCHAR` 資料行中。 因為所有 SQL Server 子系統都支援 `NVARCHAR` 類型，所以您可將 JSON 文件放在具有 **CLUSTERED COLUMNSTORE** 索引的資料表、**經記憶體最佳化的**資料表，或是可以使用 OPENROWSET 或 PolyBase 讀取的外部檔案中。

若要深入了解在 SQL Server 中將 JSON 儲存、編製索引和最佳化的選項，請參閱下列文章：

- [將 JSON 文件儲存在 SQL Server 或 SQL Database](store-json-documents-in-sql-tables.md)
- [索引 JSON 資料](index-json-data.md)
- [使用記憶體內部 OLTP 最佳化 JSON 處理](optimize-json-processing-with-in-memory-oltp.md)

### <a name="load-json-files-into-sql-server"></a>將 JSON 檔案載入 SQL Server  

您可以將儲存在檔案中的資訊格式化為標準 JSON 或以行分隔的 JSON。 SQL Server 可匯入 JSON 檔案的內容，使用 **OPENJSON** 或 **JSON_VALUE** 函式對其剖析，並將其載入資料表。  
  
-   如果您的 JSON 文件儲存於本機檔案、共用網路磁碟機，或可透過 SQL Server 存取的 Azure 檔案位置，您就能使用大量匯入將 JSON 資料載入 SQL Server。
  
-   如果以行分隔的 JSON 檔案儲存在 Azure Blob 儲存體或 Hadoop 檔案系統中，您就可以使用 Polybase 來載入 JSON 文字、在 Transact-SQL 程式碼中對其剖析，並將其載入資料表。  

### <a name="import-json-data-into-sql-server-tables"></a>將 JSON 資料匯入 SQL Server 資料表

如果必須將外部服務的 JSON 資料載入 SQL Server，您可以改用 **OPENJSON** 將資料匯入 SQL Server，而不需在應用程式層剖析資料。  
  
```sql  
DECLARE @jsonVariable NVARCHAR(MAX);

SET @jsonVariable = N'[
  {
    "Order": {  
      "Number":"SO43659",  
      "Date":"2011-05-31T00:00:00"  
    },  
    "AccountNumber":"AW29825",  
    "Item": {  
      "Price":2024.9940,  
      "Quantity":1  
    }  
  },  
  {  
    "Order": {  
      "Number":"SO43661",  
      "Date":"2011-06-01T00:00:00"  
    },  
    "AccountNumber":"AW73565",  
    "Item": {  
      "Price":2024.9940,  
      "Quantity":3  
    }  
  }
]';

-- INSERT INTO <sampleTable>  
SELECT SalesOrderJsonData.*
FROM OPENJSON (@jsonVariable, N'$')
  WITH (
    Number VARCHAR(200) N'$.Order.Number',
    Date DATETIME N'$.Order.Date',
    Customer VARCHAR(200) N'$.AccountNumber',
    Quantity INT N'$.Item.Quantity'
  ) AS SalesOrderJsonData;
```

您可以透過外部 REST 服務提供 JSON 變數的內容、從用戶端的 JavaScript 架構以參數形式加以傳送，或從外部檔案載入。 您可以輕鬆地將 JSON 文字的結果插入、更新或合併至 SQL Server 資料表。

## <a name="analyze-json-data-with-sql-queries"></a>使用 SQL 查詢分析 JSON 資料

如果您基於報表用途而必須篩選或彙總 JSON 資料，可以使用 **OPENJSON**，將 JSON 轉換為關聯式格式。 然後使用標準 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和內建函式來準備報表。  
  
```sql
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date
FROM SalesOrderRecord AS Tab
CROSS APPLY OPENJSON (Tab.json, N'$.Orders.OrdersArray')
  WITH (
    Number VARCHAR(200) N'$.Order.Number',
    Date DATETIME N'$.Order.Date',
    Customer VARCHAR(200) N'$.AccountNumber',
    Quantity INT N'$.Item.Quantity'
  ) AS SalesOrderJsonData
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified;
```  
  
您可以在相同的查詢中同時使用 JSON 文字的標準資料表資料行和值。 您可以在 `JSON_VALUE(Tab.json, '$.Status')` 運算式上新增索引，以提升查詢效能。 如需詳細資訊，請參閱[建立 JSON 資料的索引](../../relational-databases/json/index-json-data.md)。

## <a name="return-data-from-a-sql-server-table-formatted-as-json"></a>傳回格式化為 JSON 的 SQL Server 資料表資料

如果您有從資料庫層取得資料，並將其以 JSON 格式傳回的 Web 服務，或有接受格式化為 JSON 之資料的 JavaScript 架構或程式庫，可以在 SQL 查詢中直接將 JSON 輸出格式化。 您可以使用 **FOR JSON** 將 JSON 格式設定委派給 SQL Server，而不需要撰寫程式碼或包含程式庫，以轉換表格式查詢結果，再將物件序列化為 JSON 格式。  
  
例如，您可能想要產生符合 OData 規格的 JSON 輸出。 Web 服務預期具備下列格式的要求和回應： 
  
- 要求： `/Northwind/Northwind.svc/Products(1)?$select=ProductID,ProductName`  

- 回應︰ `{"@odata.context": "https://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity", "ProductID": 1, "ProductName": "Chai"}`  
  
此 OData URL 表示對於 `ID` 1 的產品之 ProductID 和 ProductName 資料行的要求。 您可以使用 **FOR JSON**，以 SQL Server 的預期方式來格式化輸出。  
  
```sql  
SELECT 'https://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity' AS '@odata.context',
  ProductID,
  Name as ProductName
FROM Production.Product
WHERE ProductID = 1
FOR JSON AUTO;
```  
  
此查詢的輸出是完全符合 OData 規格的 JSON 文字。格式設定和逸出是由 SQL Server 處理。 SQL Server 也能以任何格式將查詢結果格式化，例如 OData JSON 或 GeoJSON。  
  
## <a name="test-drive-built-in-json-support-with-the-adventureworks-sample-database"></a>隨附 AdventureWorks 範例資料庫的內建 JSON 支援試用產品

若要取得 AdventureWorks 範例資料庫，至少要從 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=49502)下載資料庫檔案、資料庫範本和指令碼檔案。

將範例資料庫還原到 SQL Server 2016 的執行個體後，請將範例檔案解壓縮，並從 JSON 資料夾開啟 *JSON Sample Queries procedures views and indexes.sql* 檔案。 執行此檔案中的指令碼，將部分存在的資料重新格式化為 JSON 資料、測試有關 JSON 資料的範例查詢和報告、編製 JSON 資料的索引，以及匯入和匯出 JSON。  
  
您可以使用檔案中所含指令碼執行的動作如下：  
  
- 將現有的結構描述反正規化來建立 JSON 資料的資料行。

  - 將來自 SalesReasons、SalesOrderDetails、SalesPerson、Customer，以及其他包含銷售訂單相關資訊的資料表儲存於 SalesOrder_json 資料表的 JSON 資料行中。  
  
  - 將 Person_json 資料表中 EmailAddresses/PersonPhone 資料表的資訊儲存為 JSON 物件的陣列。  
  
- 建立查詢 JSON 資料的程序和檢視。  
  
- 建立 JSON 資料的索引。 在 JSON 屬性上建立索引及建立全文檢索索引。  
  
- 匯入和匯出 JSON。 建立並執行將 Person 和 SalesOrder 資料表內容匯出為 JSON 結果的程序，以及使用 JSON 輸入匯入並更新 Person 和 SalesOrder 資料表的程序。  
  
- 執行查詢範例。 執行某些查詢來呼叫在步驟 2 和 4 中建立的預存程序和檢視。  
  
- 清除指令碼。 如果您想要保留在步驟 2 和 4 中建立的預存程序和檢視，則不執行這部分。  
  
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>深入了解 SQL Server 和 Azure SQL Database 中的 JSON  
  
### <a name="microsoft-videos"></a>Microsoft 影片

如需 SQL Server 和 Azure SQL Database 中內建 JSON 支援的觀看式簡介，請參閱下列影片：

*使用 SQL Server 2016 和 Azure SQL Database 中的 JSON*
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database/player]

*使用 SQL Server 以 JSON 函數建置 REST API*
> [!VIDEO https://www.youtube.com/embed/0m6GXF3-5WI]

### <a name="reference-articles"></a>參考文章

- [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md) (FOR JSON)  
- [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)  
- [JSON 函式 (Transact-SQL)](../../t-sql/functions/json-functions-transact-sql.md)  
  - [ISJSON (Transact-SQL)](../../t-sql/functions/isjson-transact-sql.md)  
  - [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)  
  - [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)  
  - [JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md)  
