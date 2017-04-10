---
title: "使用 OPENJSON 將 JSON 資料轉換成資料列和資料行 (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OPENJSON"
  - "JSON, 匯入"
  - "匯入 JSON"
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# 使用 OPENJSON 將 JSON 資料轉換成資料列和資料行 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  **OPENJSON** 資料列集函數可讓您將 JSON 文字轉換成一組資料列和資料行。 您可以使用 **OPENJSON** 在 JSON 集合上執行 SQL 查詢，或將 JSON 文字匯入至 SQL Server 資料表。  
  
> [!NOTE] **OPENJSON** 函數僅適用於**相容性層級 130** 以下。 如果您的資料庫相容性層級低於 130，SQL Server 將找不到且無法執行 **OPENJSON** 函數。 其他 JSON 函數適用於所有的相容性層級。 您可以在 sys.databases 檢視或資料庫屬性中查看相容性層級。
> 
>   您可以使用下列命令變更資料庫的相容性層級：   
>   ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130  
  
 **OPENJSON** 函數會接受單一 JSON 物件或 JSON 物件的集合，並將其轉換成一或多個資料列。 依預設，**OPENJSON** 函數會傳回 JSON 物件的第一個層級中可找到的所有索引鍵值組，或 JSON 陣列中的所有元素及其索引。  
  
 您可以使用 WITH 子句，指定 **OPENJSON** 函數要傳回之資料列的結構描述。 此明確結構描述會定義輸出的結構。  
  
## 使用不含結果結構描述的 OPENJSON

以下是簡單的範例，其使用 **OPENJSON**  與預設結構描述，並傳回 JSON 物件每個屬性的一個資料列。  
 
當您使用不含所傳回結果之指定結構描述的 **OPENJSON** 函數 (例如 OPENJSON 後面沒有 WITH 子句)，此函數會傳回具有三個資料行的資料表 - 輸入物件中的屬性名稱 (或輸入陣列元素的索引)、屬性或陣列元素的值，以及類型 (例如字串、數字、布林值、陣列或物件)。 每個資料列中所傳回之 JSON 物件 (或陣列元素) 的屬性。  

-   如需詳細資訊和範例，請參閱[搭配使用 OPENJSON 與預設結構描述 &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)。
-   如需語法和使用方式，請參閱 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)。 

```tsql  
SET @json = '{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';  
  
SELECT *  
FROM OPENJSON(@json);  
```  
  
**結果**  
  
|索引鍵|value|型別|  
|---------|-----------|----------|  
|name|John|1|  
|surname|Doe|1|  
|age|45|2|  
|skills|["SQL","C#","MVC"]|4|
    
## 使用 OPENJSON 與明確結構描述

以下是簡單的範例，其使用 **OPENJSON** 與明確指定的結構描述。  
  
當您在 **OPENJSON** 函數的 WITH 子句中指定所傳回結果的結構描述時，此函數會傳回您在 WITH 子句中定義之具有資料行的資料表。 在 WITH 子句中，您可以指定一組輸出資料行、其類型，以及每個輸出值的 JSON 來源屬性路徑。 **OPENJSON** 會逐一查看 JSON 物件的陣列、讀取為每個資料行指定之路徑上的值，並將值轉換成指定的類型。  

-   如需詳細資訊和範例，請參閱[使用 OPENJSON 與明確結構描述 &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)。
-   如需語法和使用方式，請參閱 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)。
  
```tsql  
SET @json =   
 N'[  
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
  
SELECT * FROM  
OPENJSON ( @json )  
WITH (   
             Number   varchar(200) '$.Order.Number' ,  
             Date     datetime     '$.Order.Date',  
             Customer varchar(200) '$.AccountNumber',  
             Quantity int          '$.Item.Quantity'  
)  
```  
  
**結果**  
  
|Number|日期|客戶|Quantity|  
|------------|----------|--------------|--------------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|  
|SO43661|2011-06-01T00:00:00|AW73565|3|  
  
 此函數會傳回並格式化為 JSON 陣列的元素。  
  
-   針對 JSON 陣列中的每個元素，**OPENJSON** 會在輸出資料表中產生新的資料列。 JSON 陣列中的兩個元素會轉換成所傳回資料表中的兩個資料列。  
  
-   針對使用 `colName type json_path` 語法指定的每個資料行，**OPENJSON** 函數會轉換指定路徑上陣列元素中所找到的值、將其轉換成指定的類型，並填入輸出資料表中的資料格。 在此範例中，[日期] 資料行的值取自路徑 `$.Order.Date` 上的每個物件，並轉換成日期時間值。  
  
一旦您將 JSON 集合轉換成資料列集，即可在所傳回的資料上執行任何 SQL 查詢，或將其插入至資料表。  
  
## 深入了解 SQL Server 中的 OPENJSON 與內建 JSON 支援  
 [Microsoft 專案經理 Jovan Popovic 的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## 另請參閱  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  