---
title: "使用 OPENJSON 將 JSON 資料轉換成資料列和資料行 (SQL Server) | Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OPENJSON
- JSON, importing
- importing JSON
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ea85d2dff3afe1b5e5b56117255576f8d0ae2180
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="convert-json-data-to-rows-and-columns-with-openjson-sql-server"></a>使用 OPENJSON 將 JSON 資料轉換成資料列和資料行 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

**OPENJSON** 資料列集函數可將 JSON 文字轉換成一組資料列和資料行。 請使用 **OPENJSON** 在 JSON 集合上執行 SQL 查詢，或將 JSON 文字匯入至 SQL Server 資料表。  
  
 **OPENJSON** 函數會接受單一 JSON 物件或 JSON 物件的集合，並將其轉換成一或多個資料列。 依預設，**OPENJSON** 函數會傳回下列資訊。
-   JSON 物件中可在第一個層級找到的所有索引鍵值組。
-   JSON 陣列中的所有陣列元素及其索引。  
  
選擇性地加入 **WITH** 子句，以指定 **OPENJSON** 函數傳回的資料列結構描述。 此明確結構描述會定義輸出的結構。  
  
## <a name="use-openjson-without-an-explicit-schema-for-the-output"></a>使用沒有明確輸出結構描述的 OPENJSON
當您使用 **OPENJSON** 函數而不提供明確的結果結構描述 (也就是在 OPENJSON 之後不使用 **WITH** 子句) 時，此函數會傳回包含下列三個資料行的資料表。
1.  輸入物件中的屬性名稱 (或輸入陣列中元素的索引)。
2.  屬性或陣列元素的值。
3.  型別 (例如字串、數字、布林值、陣列或物件)。

JSON 物件的每個屬性或陣列的每個元素，都會以個別資料列的方式傳回。  

以下是簡單的範例，其使用 **OPENJSON** 與預設結構描述，並傳回 JSON 物件每個屬性的一個資料列。  
 
**範例**
```sql  
DECLARE @json NVARCHAR(MAX)

SET @json='{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';

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

### <a name="more-info"></a>其他資訊

如需詳細資訊和範例，請參閱[搭配使用 OPENJSON 與預設結構描述 &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)。

如需語法和使用方式，請參閱 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)以下。 

    
## <a name="use-openjson-with-an-explicit-schema-for-the-output"></a>使用含有明確輸出結構描述的 OPENJSON
當您使用 **OPENJSON** 函數的 **WITH** 子句指定結果的結構描述時，此函數會傳回只包含您在 **WITH** 子句中所定義之資料行的資料表。 在 **WITH** 子句中，您可以指定一組輸出資料行、其型別，以及每個輸出值的 JSON 來源屬性路徑。 **OPENJSON** 會逐一查看 JSON 物件的陣列、讀取為每個資料行指定之路徑上的值，並將值轉換成指定的型。  

以下是簡單的範例，其使用 **OPENJSON** 與明確指定的結果結構描述。  
  
**範例**
  
```sql  
DECLARE @json NVARCHAR(MAX)
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
  
-   針對 JSON 陣列中的每個元素， **OPENJSON** 會在輸出資料表中產生新的資料列。 JSON 陣列中的兩個元素會轉換成所傳回資料表中的兩個資料列。  
  
-   針對使用 `colName type json_path` 語法指定的每個資料行，**OPENJSON** 函數會將指定路徑上每個陣列元素中所找到的值轉換成指定的型別，並填入輸出資料表中的資料格。 在此範例中，`Date` 資料行的值取自路徑 `$.Order.Date` 上的每個物件，並轉換成日期時間值。  
  
一旦您使用 **OPENJSON** 將 JSON 集合轉換成資料列集，即可在所傳回的資料上執行任何 SQL 查詢，或將其插入至資料表。  

### <a name="more-info"></a>其他資訊
如需詳細資訊和範例，請參閱[使用 OPENJSON 與明確結構描述 &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)。

如需語法和使用方式，請參閱 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)以下。

## <a name="openjson-requires-compatibility-level-130"></a>OPENJSON 需要相容性層級 130
**OPENJSON** 函數僅適用於 **相容性層級 130**以下。 如果您的資料庫相容性層級低於 130，SQL Server 將找不到且無法執行 **OPENJSON** 函數。 其他內建 JSON 函數適用於所有的相容性層級。 您可以在 sys.databases 檢視或資料庫屬性中查看相容性層級。

您可以使用下列命令變更資料庫的相容性層級：   
`ALTER DATABASE <DatabaseName> SET COMPATIBILITY_LEVEL = 130`  

## <a name="learn-more-about-openjson-and-built-in-json-support-in-sql-server"></a>深入了解 SQL Server 中的 OPENJSON 與內建 JSON 支援  
 [Microsoft 專案經理 Jovan Popovic 的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## <a name="see-also"></a>另請參閱  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  

