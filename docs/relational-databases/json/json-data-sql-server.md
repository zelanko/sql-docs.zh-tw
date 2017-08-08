---
title: "JSON 資料 (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- JSON
- JSON, built-in support
ms.assetid: c9a4e145-33c3-42b2-a510-79813e67806a
caps.latest.revision: 47
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: fed02f20beb9bd84dfd5ac2add3c66daf207e07c
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="json-data-sql-server"></a>JSON 資料 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

JSON 是在最新 Web 和行動應用程式中用來交換資料的常見文字資料格式。 JSON 也可用於將非結構化的資料儲存在記錄檔或類似 Microsoft Azure DocumentDB 的 NoSQL 資料庫中。 許多 REST Web 服務會傳回已格式化為 JSON 文字的結果，或接受已格式化為 JSON 的資料。 例如，大部分的 Azure 服務 (例如 Azure 搜尋服務、Azure 儲存體和 Azure DocumentDb) 具有傳回或取用 JSON 的 REST 端點。 JSON 也是使用 AJAX 呼叫在網頁和 Web 伺服器之間交換資料的主要格式。  
  
 以下是 JSON 文字範例︰  
  
```json  
[{
    "name": "John",
    "skills": ["SQL", "C#", "Azure"]
}, {
    "name": "Jane",
    "surname": "Doe"
}]
```  
  
 SQL Server 提供內建函數和運算子，讓您使用 JSON 文字執行下列工作。  
  
-   剖析 JSON 文字，並讀取或修改值。  
  
-   將 JSON 物件的陣列轉換成資料表格式。  
  
-   在已轉換的 JSON 物件上執行任何 Transact SQL 查詢。  
  
-   以 JSON 格式格式化 Transact-SQL 查詢的結果。  
  
 ![內建 JSON 支援的概觀](../../relational-databases/json/media/jsonslides1overview.png "內建 JSON 支援的概觀")  
  
## <a name="key-json-capabilities-of-sql-server"></a>SQL Server 的主要 JSON 功能 
以下是 SQL Server 提供之內建 JSON 支援的主要功能詳細資訊。

### <a name="extract-values-from-json-text-and-use-them-in-queries"></a>從 JSON 文字中擷取值，然後在查詢中使用它們
如有儲存在資料庫資料表中的 JSON 文字，您可以使用內建函式來讀取或修改 JSON 文字中的值。  
  
-   使用 **JSON_VALUE** 函式，從 JSON 字串中擷取純量值。
  
-   使用 **JSON_QUERY**，從 JSON 字串擷取物件或陣列。
  
-   使用 **ISJSON** 函式來測試字串是否包含有效的 JSON。

-   使用 **JSON_MODIFY** 函式，以變更 JSON 字串中的值。

**範例**
  
 在下列範例中，查詢會使用來自資料表的關聯式資料和 JSON 資料 (儲存在名為 `jsonCol` 的資料行中)：  
  
```sql  
SELECT Name,Surname,
 JSON_VALUE(jsonCol,'$.info.address.PostCode') AS PostCode,
 JSON_VALUE(jsonCol,'$.info.address."Address Line 1"')+' '
  +JSON_VALUE(jsonCol,'$.info.address."Address Line 2"') AS Address,
 JSON_QUERY(jsonCol,'$.info.skills') AS Skills
FROM People
WHERE ISJSON(jsonCol)>0
 AND JSON_VALUE(jsonCol,'$.info.address.Town')='Belgrade'
 AND Status='Active'
ORDER BY JSON_VALUE(jsonCol,'$.info.address.PostCode')
```  
  
 應用程式和工具分辨不出從純量資料表資料行取得的值和從 JSON 資料行取得的值有何不同。 您可以在 Transact-SQL 查詢的任意部分 (包括 WHERE、ORDER BY 或 GROUP BY 子句、範圍彙總等等)，使用來自 JSON 文字的值。 JSON 函式會使用類似 JavaScript 的語法來參考 JSON 文字內的值。

如需詳細資訊，請參閱 [使用內建函數，驗證、查詢以及變更 JSON 資料 &#40;SQL Server&#41;](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)、 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)和 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)。  
  
### <a name="change-json-values"></a>變更 JSON 值
如果您需要修改部分 JSON 文字，可以使用 **JSON_MODIFY** 函式來更新 JSON 字串中的屬性值，並傳回更新的 JSON 字串。 下列範例會在包含 JSON 的變數中更新屬性的值。  
  
```sql  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=JSON_MODIFY(@jsonInfo,'$.info.address[0].town','London') 
```  
  
### <a name="convert-json-collections-to-a-rowset"></a>將 JSON 集合轉換為資料列集
您不需要自訂查詢語言也能在 SQL Server 中查詢 JSON。 您可以使用標準的 T-SQL 查詢 JSON 資料。 如果您需要建立 JSON 資料的查詢或報表，可以呼叫 **OPENJSON** 資料列集函式，輕鬆地將 JSON 資料轉換成資料列和資料行。 如需詳細資訊，請參閱 [使用 OPENJSON 將 JSON 資料轉換成資料列和資料行 &#40;SQL Server&#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)。  
  
 下列範例會呼叫 **OPENJSON**，將儲存於 `@json` 變數中的物件陣列轉換為可使用標準 SQL **SELECT** 陳述式查詢的資料列集︰  
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json =  
N'[  
       { "id" : 2,"info": { "name": "John", "surname": "Smith" }, "age": 25 },  
       { "id" : 5,"info": { "name": "Jane", "surname": "Smith" }, "dob": "2005-11-04T12:00:00" }  
 ]'  
   
SELECT *  
FROM OPENJSON(@json)  
  WITH (id int 'strict $.id',  
        firstName nvarchar(50) '$.info.name', lastName nvarchar(50) '$.info.surname',  
        age int, dateOfBirth datetime2 '$.dob')  
```  
  
 **結果**  
  
|id|firstName|lastName|age|dateOfBirth|  
|--------|---------------|--------------|---------|-----------------|  
|2|John|Smith|25||  
|5|Jane|Smith||2005-11-04T12:00:00|  
  
 **OPENJSON** 會將 JSON 物件的陣列將轉換為資料表，每個物件顯示為一個資料列，而索引鍵/值組會以資料格形式傳回。 輸出會遵循下列規則。
-   **OPENJSON** 會將 JSON 值轉換為 **WITH** 子句中指定的類型。
-   **OPENJSON** 可以處理單層式金鑰值組和巢狀階層組織的物件。
-   您不必傳回 JSON 文字包含的所有欄位。
-   如果 JSON 值不存在，**OPENJSON** 會傳回 NULL 值。
-   您可以選擇在類型規格之後指定路徑，以參考巢狀的屬性或參考不同名稱的屬性。
-   JSON 文字中必須有在路徑中指定指定屬性值的選擇性 **嚴格** 前置詞。

如需詳細資訊，請參閱 [使用 OPENJSON 將 JSON 資料轉換成資料列和資料行 &#40;SQL Server&#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md) 和 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)。  
  
### <a name="convert-sql-server-data-to-json-or-export-json"></a>將 SQL Server 資料轉換為 JSON 或匯出 JSON
將 **FOR JSON** 子句加入至 **SELECT** 陳述式，以將 SQL Server 資料或 SQL 查詢結果格式化為 JSON。 使用 FOR JSON，將來自用戶端應用程式的 JSON 輸出的格式設定委派給 SQL Server。 如需詳細資訊，請參閱 [使用 FOR JSON 將查詢結果格式化為 JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)。  
  
 下列範例會搭配 FOR JSON 子句使用 PATH 模式。  
  
```sql  
SELECT id, firstName AS "info.name", lastName AS "info.surname", age, dateOfBirth as dob  
FROM People  
FOR JSON PATH  
```  
  
星期 **FOR JSON** 子句會將 SQL 結果格式化為 JSON 文字，提供給任何了解 JSON 的應用程式。 PATH 選項會在 SELECT 子句中使用點分隔的別名，巢狀化查詢結果中的物件。  
  
 **結果**  
  
```json  
[{
    "id": 2,
    "info": {
        "name": "John",
        "surname": "Smith"
    },
    "age": 25
}, {
    "id": 5,
    "info": {
        "name": "Jane",
        "surname": "Smith"
    },
    "dob": "2005-11-04T12:00:00"
}] 
```  
  
 如需詳細資訊，請參閱[使用 FOR JSON 將查詢結果格式化為 JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md) 和 [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)。  
  
## <a name="combine-relational-and-json-data"></a>合併關聯式資料和 JSON 資料
 SQL Server 提供了混合模型，使用標準的 Transact-SQL 語言來儲存及處理關聯式與 JSON 資料。 您可以在資料表中組織 JSON 文件的集合、建立它們之間的關聯性、結合儲存於資料表中的強類型純量資料行和儲存於 JSON 資料行中的彈性索引鍵/值組，以及使用完整的 Transact-SQL 在一或多個資料表中查詢純量和 JSON 值。
 
JSON 文字通常儲存在 varchar 或 nvarchar 資料行中，並以純文字形式編製索引。 任何支援文字的 SQL Server 功能或元件都支援 JSON，因此 JSON 和其他 SQL Server 功能之間幾乎沒有任何互動限制。 您可以將 JSON 儲存在記憶體內部或暫存資料表中，您可以在 JSON 文字上套用資料列層級安全性的述詞等等。

如只有要使用自訂查詢語言來處理 JSON 文件的 JSON 工作負載，請考慮 Microsoft Azure Microsoft Azure [DocumentDB](https://azure.microsoft.com/services/documentdb/)。  
  
 以下提供數個使用案例，示範如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中使用內建的 JSON 支援。  
  
## <a name="return-data-from-a-sql-server-table-formatted-as-json"></a>傳回格式化為 JSON 的 SQL Server 資料表資料  
 如有 Web 服務是從資料庫層級取得資料，並以 JSON 格式傳回資料，或是在接受格式化為 JSON 之資料的 JavaScript 架構或程式庫中傳回資料，您可以在 SQL 查詢中直接將 JSON 輸出格式化。 您可以使用 FOR JSON 來將 JSON 格式設定委派給 SQL Server，而不需要使用編寫程式碼或包含程式庫來轉換表格式查詢結果，然後將物件序列化為 JSON 格式。  
  
 例如，您可能想要產生符合 OData 規格的 JSON 輸出。 Web 服務預期具備下列格式的要求和回應。  
  
-   要求： `/Northwind/Northwind.svc/Products(1)?$select=ProductID,ProductName`  
  
-   回應︰ `{"@odata.context":"http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity","ProductID":1,"ProductName":"Chai"}`  
  
 此 OData URL 表示對於識別碼 1 的產品的 ProductID 和 ProductName 資料行的要求。 您可以使用 **FOR JSON**，以 SQL Server 的預期方式來格式化輸出。  
  
```sql  
SELECT 'http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity'
 AS '@odata.context',   
 ProductID, Name as ProductName   
FROM Production.Product  
WHERE ProductID = 1  
FOR JSON AUTO  
```  
  
此查詢的輸出是完全符合 OData 規格的 JSON 文字。 格式設定和逸出是由 SQL Server 處理。 SQL Server 也可以將查詢結果格式化為任何格式，例如 OData JSON 或 GeoJSON - 如需詳細資訊，請參閱 [Returning spatial data in GeoJSON format](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/returning-spatial-data-in-geojson-format-part-1) (以 GeoJSON 格式傳回空間資料)。  
  
## <a name="analyze-json-data-with-sql-queries"></a>使用 SQL 查詢分析 JSON 資料  
 如果您基於報告目的而必須篩選或彙總 JSON 資料，您可以使用 **OPENJSON**，將 JSON 轉換為關聯式格式。 然後使用標準的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和內建函數來準備報告。  
  
```sql  
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date  
FROM   SalesOrderRecord AS Tab  
          CROSS APPLY  
     OPENJSON (Tab.json, N'$.Orders.OrdersArray')  
           WITH (  
              Number   varchar(200) N'$.Order.Number',   
              Date     datetime     N'$.Order.Date',  
              Customer varchar(200) N'$.AccountNumber',   
              Quantity int          N'$.Item.Quantity'  
           )  
  AS SalesOrderJsonData  
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'  
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified  
```  
  
 標準的資料表資料行和來自 JSON 文字的值可以在相同的查詢中使用。 您可以在 `JSON_VALUE(Tab.json, '$.Status')` 運算式上新增索引，以提升查詢效能。 如需詳細資訊，請參閱 [索引 JSON 資料](../../relational-databases/json/index-json-data.md)。
  
## <a name="import-json-data-into-sql-server-tables"></a>將 JSON 資料匯入 SQL Server 資料表  
 如果必須將外部服務的 JSON 資料載入 SQL Server，您可以改用 **OPENJSON** 將資料匯入 SQL Server，而不需在應用程式層剖析資料。  
  
```sql  
DECLARE @jsonVariable NVARCHAR(MAX)

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
  ]'
  
INSERT INTO SalesReport  
SELECT SalesOrderJsonData.*  
FROM OPENJSON (@jsonVariable, N'$.Orders.OrdersArray')  
           WITH (  
              Number   varchar(200) N'$.Order.Number',   
              Date     datetime     N'$.Order.Date',  
              Customer varchar(200) N'$.AccountNumber',   
              Quantity int          N'$.Item.Quantity'  
           )  
  AS SalesOrderJsonData;  
```  
  
 JSON 變數的內容可以由外部 REST 服務提供、以參數形式從某些用戶端的 JavaScript 架構傳送，或從外部檔案載入。 您可以輕鬆地將 JSON 文字的結果插入、更新或合併至 SQL Server 資料表。 如需此案例的詳細資訊，請參閱下列部落格文章。
-   [在 SQL Server 中匯入 JSON 資料](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/09/22/openjson-the-easiest-way-to-import-json-text-into-table/)
-   [SQL Server 2016 中的 Upsert JSON 文件](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/03/upsert-json-documents-in-sql-server-2016)
-   [將 GeoJSON 資料載入 SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/loading-geojson-data-into-sql-server/)。  
  
## <a name="load-json-files-into-sql-server"></a>將 JSON 檔案載入 SQL Server  
 儲存在檔案中的資訊可格式化為標準的 JSON 或以行分隔的 JSON。 SQL Server 可以匯入檔案的 JSON 內容、使用 **OPENJSON** 或 **JSON_VALUE** 函式進行剖析，並將它載入資料表。  
  
-   如果您的 JSON 文件儲存於本機檔案、共用的網路磁碟機，或可透過 SQL Server 存取的 Azure 檔案儲存體位置，您就能使用大量匯入，將 JSON 資料載入 SQL Server。 如需此案例的詳細資訊，請參閱 [Importing JSON files into SQL Server using OPENROWSET (BULK)](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2015/10/07/importing-json-files-into-sql-server-using-openrowset-bulk.aspx)(使用 OPENROWSET (BULK) 將 JSON 檔案匯入 SQL Server)。  
  
-   如果以行分隔的 JSON 檔案儲存在 Azure Blob 儲存體或 Hadoop 檔案系統中，您就可以使用 Polybase 來載入 JSON 文字、在 Transact-SQL 程式碼中進行剖析，並將它載入資料表。  
  
## <a name="test-drive-built-in-json-support"></a>測試磁碟機內建的 JSON 支援  
 **使用 AdventureWorks 範例資料庫測試磁碟機內建的 JSON 支援。** 若要取得 AdventureWorks 範例資料庫，至少要從 [這裡](https://www.microsoft.com/en-us/download/details.aspx?id=49502)。 將範例資料庫還原到 SQL Server 2016 的執行個體之後，解壓縮範例檔案，並從 JSON 資料夾開啟「JSON 範例查詢程序檢視和索引.sql」檔案。 執行此檔案中的程式碼，將部分存在的資料重新格式化為 JSON 資料、執行有關 JSON 資料的範例查詢和報告、編製 JSON 資料的索引，以及匯入和匯出 JSON。  
  
 以下是您可以使用檔案中包含的指令碼執行的動作。  
  
1.  將現有的結構描述反正規化來建立 JSON 資料的資料行。  
  
    1.  將來自 SalesReasons、SalesOrderDetails、SalesPerson、Customer，以及其他包含銷售訂單相關資訊的資料表儲存於 SalesOrder_json 資料表的 JSON 資料行中。  
  
    2.  將來自 EmailAddresses/PersonPhone 資料表的資訊儲存至 Person_json 資料表，以做為 JSON 物件的陣列。  
  
2.  建立查詢 JSON 資料的程序和檢視。  
  
3.  編製 JSON 資料的索引 – 在 JSON 屬性上建立索引與全文檢索索引。  
  
4.  匯入和匯出 JSON – 建立並執行匯出 Person 和 SalesOrder 資料表的內容做為 JSON 結果的程序，以及使用 JSON 輸入匯入並更新 Person 和 SalesOrder 資料表的程序。  
  
5.  執行查詢範例 – 執行一些查詢來呼叫在步驟 2 和 4 中建立的預存程序和檢視。  
  
6.  清除指令碼 – 如果您想要保留在步驟 2 和 4 中建立的預存程序和檢視，就不要執行這部分。  
  
## <a name="learn-more-about-built-in-json-support"></a>深入了解內建的 JSON 支援  
  
### <a name="topics-in-this-section"></a>本節主題：  
 [使用 FOR JSON 將查詢結果格式化為 JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
 使用 FOR JSON 子句，將來自用戶端應用程式的 JSON 輸出格式設定委派給 SQL Server。  
  
 [使用 OPENJSON 將 JSON 資料轉換成資料列和資料行 &#40;SQL Server&#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)  
 使用 OPENJSON 來將 JSON 資料匯入 SQL Server，或者針對目前無法直接取用 JSON 的應用程式或服務 (例如 SQL Server Integration Services)，將 JSON 資料轉換為關聯式格式。  
  
 [使用內建函數，驗證、查詢以及變更 JSON 資料 &#40;SQL Server&#41;](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)  
 使用這些內建函式來驗證 JSON 文字，以及擷取純量值、物件或陣列。  
  
 [JSON 路徑運算式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
 使用路徑運算式來指定您想要使用的 JSON 文字。  
  
 [索引 JSON 資料](../../relational-databases/json/index-json-data.md)  
 使用計算資料行，在 JSON 文件的屬性上建立定序感知的索引。  
  
[解決 SQL Server 中的 JSON 常見問題](../../relational-databases/json/solve-common-issues-with-json-in-sql-server.md)  
 尋找關於 SQL Server 中內建 JSON 支援的一些常見問題的解答。  
  
### <a name="microsoft-blog-posts"></a>Microsoft 部落格文章  
  
-   對於大量的特定解決方案、使用案例和建議，請參閱 SQL Server 和 Azure SQL Database 中 Microsoft 經理專案 Jovan Popovic 所撰寫的[有關內建 JSON 支援的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)。  
  
### <a name="reference-topics"></a>參考主題  
  
-   [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md) (FOR JSON)  
  
-   [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
-   [JSON 函數 &#40;Transact-SQL&#41;](../../t-sql/functions/json-functions-transact-sql.md)  
  
    -   [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)  
  
    -   [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)  
  
    -   [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
    -   [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)  
  
  

