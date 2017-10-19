---
title: "OPENJSON (TRANSACT-SQL) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENJSON
- OPENJSON_TSQL
helpviewer_keywords:
- OPENJSON rowset function
- JSON, importing
- JSON, converting from
ms.assetid: 233d0877-046b-4dcc-b5da-adeb22f78531
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: 27eeb54d6493bb200e56caada1238d6fafb5b339
ms.contentlocale: zh-tw
ms.lasthandoff: 10/11/2017

---
# <a name="openjson-transact-sql"></a>OPENJSON (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

**OPENJSON**是資料表值函式會剖析 JSON 文字，然後從 JSON 輸入傳回物件和屬性，做為資料列和資料行。 換句話說， **OPENJSON**提供的 JSON 文件上的資料列集檢視。 您可以在資料列集和用來擴展的資料行的 JSON 屬性路徑中明確指定資料行。 因為**OPENJSON**傳回一組資料列，您可以使用**OPENJSON**中`FROM`子句[!INCLUDE[tsql](../../includes/tsql-md.md)]就像您可以使用任何其他資料表、 檢視或資料表值函式的陳述式。  
  
使用**OPENJSON** JSON 資料匯入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或將 JSON 資料轉換為關聯式格式的應用程式或服務，無法直接取用 JSON。  
  
> [!NOTE]  
>  **OPENJSON**函式是僅適用於相容性層級 130 或更高版本。 如果您的資料庫相容性層級低於 130，SQL Server 將找不到且無法執行 **OPENJSON** 函式。 其他 JSON 函數適用於所有的相容性層級。
> 
> 您可以在 `sys.databases` 檢視或資料庫屬性中查看相容性層級。 您可以變更具有下列的命令之資料庫的相容性層級：  
> 
> `ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130`
>   
> 相容性層級 120 可能甚至中新的 Azure SQL Database 的預設值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示")[TRANSACT-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
OPENJSON( jsonExpression [ , path ] )  [ <with_clause> ]

<with_clause> ::= WITH ( { colName type [ column_path ] [ AS JSON ] } [ ,...n ] )
```  

**OPENJSON**資料表值函式會剖析*jsonExpression*提供做為第一個引數並傳回一個或多個資料列，其中包含在運算式中的 JSON 物件的資料。 *jsonExpression*可以包含巢狀的子物件。 如果您想要剖析的子物件從*jsonExpression*，您可以指定**路徑**JSON 子物件的參數。

### <a name="openjson"></a>openjson

![OPENJSON TVF 語法](../../relational-databases/json/media/openjson-syntax.png "的 OPENJSON 語法")  

根據預設， **OPENJSON**資料表值函式會傳回三個資料行，其中包含索引鍵的名稱，此值，以及每個索引鍵： 值配對的型別中找到*jsonExpression*。 或者，您可以明確指定結果的結構描述集**OPENJSON**藉由傳回*with_clause*。
  
### <a name="withclause"></a>with_clause
  
![OPENJSON TVF 中子句語法](../../relational-databases/json/media/openjson-shema-syntax.png "WITH OPENJSON 語法")

*with_clause*包含針對其類型的資料行清單**OPENJSON**傳回。 根據預設， **OPENJSON**符合中的索引鍵*jsonExpression*中的資料行名稱*with_clause* （在此情況下，相符項目索引鍵意味著會區分大小寫）。 如果資料行名稱不相符的索引鍵的名稱，您可以提供選擇性*column_path*，也就是[JSON 路徑運算式](../../relational-databases/json/json-path-expressions-sql-server.md)內的索引鍵參考的*jsonExpression*。 

## <a name="arguments"></a>引數  
### <a name="jsonexpression"></a>*jsonExpression*  
這 Unicode 字元運算式包含 JSON 文字。  
  
OPENJSON 逐一查看陣列的元素或屬性的 JSON 運算式中的物件，並傳回一個資料列，每個項目或屬性。 下列範例會傳回每一個屬性的物件提供作為*jsonExpression*:  
  
```sql  
DECLARE @json NVARCHAR(4000) = N'{  
   "StringValue":"John",  
   "IntValue":45,  
   "TrueValue":true,  
   "FalseValue":false,  
   "NullValue":null,  
   "ArrayValue":["a","r","r","a","y"],  
   "ObjectValue":{"obj":"ect"}  
}'

SELECT *
FROM OPENJSON(@json)
```  
  
**結果**  
  
|索引鍵|value|型別|  
|---------|-----------|----------|  
|StringValue|John|1|  
|IntValue|45|2|  
|trueValue|true|3|  
|falseValue|false|3|  
|nullValue|NULL|0|  
|ArrayValue|["a"、"r"、"r"、""、"y"]|4|  
|ObjectValue|{"obj":"ect"}|5|  

### <a name="path"></a>*路徑*  
參考物件或陣列中的選擇性 JSON 路徑運算式*jsonExpression*。 **OPENJSON**在 JSON 文字中指定位置處進行搜尋，並將其參考的片段。 如需詳細資訊，請參閱[JSON 路徑運算式 &#40;SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md).

在[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]和[!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]，您可以提供變數的值為*路徑*。
  
下列範例會傳回巢狀的物件，藉由指定*路徑*:  

```sql  
DECLARE @json NVARCHAR(4000) = N'{  
      "path": {  
            "to":{  
                 "sub-object":["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]  
                 }  
              }  
 }';

SELECT [key], value
FROM OPENJSON(@json,'$.path.to."sub-object"')
```  
  
 **結果**  
  
|索引鍵|值|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
 
當**OPENJSON**剖析 JSON 陣列，此函式傳回之項目的索引 JSON 文字中做為索引鍵。

用來比對和 JSON 運算式屬性路徑步驟，這項比較會區分大小寫和定序感知 （也就是 BIN2 的比較）。 

### <a name="withclause"></a>*with_clause*
明確地定義輸出結構描述**OPENJSON**函數來傳回。 選擇性*with_clause*可以包含下列元素：

*colName*輸出資料行的名稱。  
  
根據預設， **OPENJSON**用於比對的屬性，在 JSON 文字中的資料行名稱。 例如，如果您指定的資料行*名稱*在結構描述中，OPENJSON 會嘗試在填入此資料行屬性的 JSON 文字中的 「 名稱 」。 您可以使用覆寫這個預設對應*column_path*引數。  
  
*type*  
為輸出資料行的資料類型。  

> [!NOTE]
> 如果您同時使用**AS JSON**選項，資料行*類型*必須`NVARCHAR(MAX)`。
  
*column_path*  
是指定要傳回指定的資料行中之屬性的 JSON 路徑。 如需詳細資訊，請參閱描述*路徑*先前在本主題中的參數。  
  
使用*column_path*時要覆寫預設的對應規則的輸出資料行名稱不符合屬性的名稱。  
  
用來比對和 JSON 運算式屬性路徑步驟，這項比較會區分大小寫和定序感知 （也就是 BIN2 的比較）。  
  
如需路徑的詳細資訊，請參閱[JSON 路徑運算式 &#40;SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
*為 JSON*  
使用**AS JSON**資料行定義中的選項，指定參考的屬性包含內部的 JSON 物件或陣列。 如果您指定**AS JSON**選項，資料行的類型必須是 nvarchar （max）。

-   如果您未指定**AS JSON**資料行，函數會傳回純量值 （例如 int、 字串、 true、 false） 從指定的 JSON 屬性上指定的路徑。 如果路徑所表示的物件或陣列，指定路徑上找不到屬性，函式會傳回 null lax 模式中，或在 strict 模式下會傳回錯誤。 此行為是類似的行為**JSON_VALUE**函式。  
  
-   如果您指定**AS JSON**資料行，此函數會傳回 JSON 片段從指定的 JSON 屬性上指定的路徑。 如果路徑表示純量值，指定路徑上找不到屬性，函式會傳回 null lax 模式中，或在 strict 模式下會傳回錯誤。 此行為是類似的行為**JSON_QUERY**函式。  
  
> [!NOTE]  
> 如果您想要從 JSON 屬性傳回巢狀的 JSON 片段，您必須提供**AS JSON**旗標。 如果沒有這個選項，如果找不到屬性，OPENJSON 會傳回 NULL 值，而不是參考的 JSON 物件或陣列，或它在 strict 模式下會傳回執行階段錯誤。  
  
例如，下列查詢會傳回並格式化陣列的項目：  
  
```sql  
DECLARE @json NVARCHAR(MAX) = N'[  
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
   
SELECT *
FROM OPENJSON ( @json )  
WITH (   
              Number   varchar(200)   '$.Order.Number',  
              Date     datetime       '$.Order.Date',  
              Customer varchar(200)   '$.AccountNumber',  
              Quantity int            '$.Item.Quantity',  
              [Order]  nvarchar(MAX)  AS JSON  
 )
```  
  
**結果**  
  
|Number|日期|客戶|Quantity|單|  
|------------|----------|--------------|--------------|-----------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|{"Number":"SO43659"，"Date":"2011年-05-31T00:00:00"}|  
|SO43661|2011-06-01T00:00:00|AW73565|3|{"Number":"SO43661"，"Date":"2011年-06-01T00:00:00"}|  
  

## <a name="return-value"></a>傳回值  
OPENJSON 函式傳回的資料行取決於 WITH 選項。  
  
1. 當您呼叫 OPENJSON 與預設結構描述-也就是當您未在 WITH 子句中指定明確的結構描述函數會傳回下列資料行的資料表：  
    1.  **索引鍵**。 Nvarchar （4000） 值，其中包含指定屬性的名稱或索引的指定陣列中的項目。 索引鍵資料行具有 BIN2 定序。  
    2.  **值**。 Nvarchar （max） 值，其中包含屬性的值。 [值] 欄位會繼承其定序，從*jsonExpression*。
    3.  **型別**。 整數值，其中包含值的類型。 **類型**使用 OPENJSON 與預設結構描述時，才會傳回資料行。 類型資料行具有下列值之一：  
  
        |型別資料行的值|JSON 資料類型|  
        |------------------------------|--------------------|  
        |0|null|  
        |1|string|  
        |2|int|  
        |3|true/false|  
        |4|array|  
        |5|物件 (object)|  
  
     只會傳回第一層級屬性。 如果 JSON 文字的格式不正確，陳述式將會失敗。  

2. 當您呼叫 OPENJSON WITH 子句中指定明確的結構描述，則函數會傳回具有您在 WITH 子句中定義的結構描述的資料表。  

## <a name="remarks"></a>備註  

*json_path*中的第二個引數使用**OPENJSON**或*with_clause*可以開始**lax**或**嚴格**關鍵字。

-   在**lax**模式中， **OPENJSON**不會引發錯誤，如果找不到物件或指定路徑上的值。 如果找不到路徑， **OPENJSON**傳回空的結果集或 NULL 值。
-   在**嚴格**，模式**OPENJSON**傳回錯誤，如果找不到路徑。

在此頁面上的範例部分明確指定 path 模式中，lax 或 strict。 Path 模式是選擇性的。 如果您未明確指定 path 模式，lax 模式是預設值。 如需 path 模式和路徑運算式的詳細資訊，請參閱[JSON 路徑運算式 &#40;SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md).    

中的資料行名稱*with_clause* JSON 文字中的索引鍵與進行比對。 如果您指定的資料行名稱`[Address.Country]`，它會與索引鍵與`Address.Country`。 如果您想要參考的巢狀索引鍵`Country`物件內`Address`，您必須指定路徑`$.Address.Country`路徑資料行中。

*json_path*可能包含英數字元的索引鍵。 逸出中的索引鍵名稱*json_path*雙引號括住，如果您有特殊字元的索引鍵中。 例如，`$."my key $1".regularKey."key with . dot"`相符項目值為 1，下列 JSON 文字中：

```json
{
  "my key $1": {
    "regularKey":{
      "key with . dot": 1
    }
  }
}
```  

## <a name="examples"></a>範例  
  
### <a name="example-1---convert-a-json-array-to-a-temporary-table"></a>範例 1-將 JSON 陣列轉換成暫存資料表  
下列範例提供識別項的清單為 JSON 陣列的數字。 查詢將識別項的資料表中的 JSON 陣列，並篩選具有指定識別碼的所有產品。  
  
```sql  
DECLARE @pSearchOptions NVARCHAR(4000) = N'[1,2,3,4]'

SELECT *
FROM products
INNER JOIN OPENJSON(@pSearchOptions) AS productTypes
 ON product.productTypeID = productTypes.value
```  
  
這個查詢相當於下列的範例。 不過，在下列範例中，您必須內嵌在查詢中，而不是將它們當做參數傳遞的數字。  
  
```sql  
SELECT *
FROM products
WHERE product.productTypeID IN (1,2,3,4)
```  
  
### <a name="example-2---merge-properties-from-two-json-objects"></a>範例 2： 從兩個 JSON 物件的合併屬性  
下列範例會選取兩個 JSON 物件的所有屬性的聯集。 兩個物件具有重複*名稱*屬性。 範例會使用的索引鍵值，從結果中排除重複的資料列。  
  
```sql  
DECLARE @json1 NVARCHAR(MAX),@json2 NVARCHAR(MAX)

SET @json1=N'{"name": "John", "surname":"Doe"}'

SET @json2=N'{"name": "John", "age":45}'

SELECT *
FROM OPENJSON(@json1)
UNION ALL
SELECT *
FROM OPENJSON(@json2)
WHERE [key] NOT IN (SELECT [key] FROM OPENJSON(@json1))
```  
  
### <a name="example-3---join-rows-with-json-data-stored-in-table-cells-using-cross-apply"></a>範例 3-JSON 資料儲存於使用 CROSS APPLY 表格儲存格的聯結資料列  
在下列範例中，`SalesOrderHeader`資料表有`SalesReason`文字資料行包含的陣列`SalesOrderReasons`JSON 格式。 `SalesOrderReasons`物件包含的屬性，例如*品質*和*製造商*。 此範例會建立的報表會聯結每個銷售訂單資料列與相關銷售原因。 如同原因儲存在個別子資料表中，OPENJSON 運算子就會展開銷售原因的 JSON 陣列。 然後 CROSS APPLY 運算子會聯結每個銷售訂單資料列與 OPENJSON 資料表值函數所傳回的資料列。  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
> [!TIP] 
> 當您必須展開 JSON 陣列儲存在個別的欄位，並將它們具有其父資料列，您通常會使用[!INCLUDE[tsql](../../includes/tsql-md.md)]CROSS APPLY 運算子。 如需 CROSS APPLY 的詳細資訊，請參閱[FROM &#40;TRANSACT-SQL &#41;](../../t-sql/queries/from-transact-sql.md).  
  
相同的查詢可以撰寫使用`OPENJSON`與要傳回的資料列明確定義結構描述：  
  
```sql  
SELECT SalesOrderID, OrderDate, value AS Reason  
FROM Sales.SalesOrderHeader  
     CROSS APPLY OPENJSON (SalesReasons) WITH (value nvarchar(100) '$')
```  
  
在此範例中，`$`路徑所參考陣列中的每個項目。 如果您想要傳回的值，明確轉換，您可以使用這種類型的查詢。  
  
### <a name="example-4---combine-relational-rows-and-json-elements-with-cross-apply"></a>範例 4-合併關聯式資料列和 JSON 元素使用 CROSS APPLY  
下列查詢會將關聯式資料列和 JSON 項目結合成下表中顯示的結果。  
  
```sql  
SELECT store.title, location.street, location.lat, location.long  
FROM store  
CROSS APPLY OPENJSON(store.jsonCol, 'lax $.location')   
     WITH (street varchar(500) ,  postcode  varchar(500) '$.postcode' ,  
     lon int '$.geo.longitude', lat int '$.geo.latitude')  
     AS location
```  
  
**結果**  
  
|title|街道|postcode|lon|lat|  
|-----------|------------|--------------|---------|---------|  
|整個食物市場|17991 Redmond 方法|WA 98052|47.666124|-122.10155|  
|Sears|148th Ave NE|WA 98052|47.63024|-122.141246,17|  
  
### <a name="example-5---import-json-data-into-sql-server"></a>範例 5-匯入至 SQL Server 的 JSON 資料  
以下範例會將整個 JSON 物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
```sql  
DECLARE @json NVARCHAR(max)  = N'{  
  "id" : 2,  
  "firstName": "John",  
  "lastName": "Smith",  
  "isAlive": true,  
  "age": 25,  
  "dateOfBirth": "2015-03-25T12:00:00",  
  "spouse": null  
  }';  
   
  INSERT INTO Person  
  SELECT *   
  FROM OPENJSON(@json)  
  WITH (id int,  
        firstName nvarchar(50), lastName nvarchar(50),   
        isAlive bit, age int,  
        dateOfBirth datetime2, spouse nvarchar(50)
```  
  
## <a name="see-also"></a>另請參閱  
 [JSON 路徑運算式 &#40;SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [將 JSON 資料轉換成資料列和資料行與 OPENJSON &#40;SQL Server &#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)   
 [使用 OPENJSON 與預設結構描述 &#40;SQL Server &#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)   
 [使用 OPENJSON 與明確結構描述 &#40;SQL Server &#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)  
  
  

