---
title: 使用 OPENJSON 剖析及轉換 JSON 資料 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENJSON
- JSON, importing
- importing JSON
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||= azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e09a24d4f75c0b559a247176a7d57516cf75e43e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909444"
---
# <a name="parse-and-transform-json-data-with-openjson-sql-server"></a>使用 OPENJSON 剖析及轉換 JSON 資料 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

**OPENJSON** 資料列集函數可將 JSON 文字轉換成一組資料列和資料行。 一旦您使用 **OPENJSON** 將 JSON 集合轉換成資料列集，即可在所傳回的資料上執行任何 SQL 查詢，或將其插入至 SQL Server 資料表。 
  
**OPENJSON** 函數會接受單一 JSON 物件或 JSON 物件的集合，並將其轉換成一或多個資料列。 根據預設，**OPENJSON** 函式會傳回下列資料：
-   從 JSON 物件，此函式會傳回可在第一層找到的所有索引鍵/值組。
-   從 JSON 陣列，此函式會傳回所有陣列元素及其索引。  

您可以新增選擇性 **WITH** 子句，以提供明確定義輸出結構的結構描述。  
  
## <a name="option-1---openjson-with-the-default-output"></a>選項 1 - 具有預設輸出的 OPENJSON
當您使用 **OPENJSON** 函式而不提供明確的結果結構描述 (也就是在 **OPENJSON** 之後不使用 **WITH** 子句) 時，此函式會傳回包含下列三個資料行的資料表：
1.  輸入物件中的屬性**名稱** (或輸入陣列中元素的索引)。
2.  屬性或陣列元素的**值**。
3.  **類型** (例如字串、數字、布林值、陣列或物件)。

**OPENJSON** 會以個別資料列的方式傳回 JSON 物件的每個屬性，或陣列的每個元素。  

以下是簡單的範例，其使用具有預設結構描述 (也就是不提供選擇性 **WITH** 子句) 的 **OPENJSON**，並以個別資料列的方式傳回 JSON 物件的每個屬性。  

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
|NAME|John|1|  
|surname|Doe|1|  
|age|45|2|  
|skills|["SQL","C#","MVC"]|4|

### <a name="more-info-about-openjson-with-the-default-schema"></a>具有預設結構描述之 OPENJSON 的詳細資訊

如需詳細資訊和範例，請參閱[搭配使用 OPENJSON 與預設結構描述 &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)。

如需語法和使用方式，請參閱 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)以下。 

## <a name="option-2---openjson-output-with-an-explicit-structure"></a>選項 2 - 具有明確結構的 OPENJSON 輸出

當您使用 **OPENJSON** 函數的 **WITH** 子句指定結果的結構描述時，此函數會傳回只包含您在 **WITH** 子句中所定義之資料行的資料表。 在選擇性 **WITH** 子句中，您可以指定一組輸出資料行、其類型，以及每個輸出值的 JSON 來源屬性路徑。 **OPENJSON** 會逐一查看 JSON 物件的陣列、讀取為每個資料行指定之路徑上的值，並將值轉換成指定的型。  

以下是簡單的範例，其使用具有您在 **WITH** 子句中明確指定之輸出結構描述的 **OPENJSON**。  
  
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
  
|Number|date|客戶|Quantity|  
|------------|----------|--------------|--------------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|  
|SO43661|2011-06-01T00:00:00|AW73565|3|  
  
此函數會傳回並格式化為 JSON 陣列的元素。  
  
-   針對 JSON 陣列中的每個元素， **OPENJSON** 會在輸出資料表中產生新的資料列。 JSON 陣列中的兩個元素會轉換成所傳回資料表中的兩個資料列。  
  
-   針對使用 `colName type json_path` 語法指定的每個資料行，**OPENJSON** 會將指定路徑上每個陣列元素中所找到的值轉換成指定的類型。 在此範例中，`Date` 資料行的值取自路徑 `$.Order.Date` 上的每個元素，並已轉換成日期時間值。  
  
### <a name="more-info-about-openjson-with-an-explicit-schema"></a>具有明確結構描述之 OPENJSON 的詳細資訊

如需詳細資訊和範例，請參閱[使用 OPENJSON 與明確結構描述 &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)。

如需語法和使用方式，請參閱 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)以下。

## <a name="openjson-requires-compatibility-level-130"></a>OPENJSON 需要相容性層級 130

**OPENJSON** 函數僅適用於 **相容性層級 130**以下。 如果您的資料庫相容性層級低於 130，SQL Server 將找不到且無法執行 **OPENJSON** 函式。 其他內建 JSON 函數適用於所有的相容性層級。

您可以在 `sys.databases` 檢視或資料庫屬性中查看相容性層級。

您可以使用下列命令變更資料庫的相容性層級：   
`ALTER DATABASE <DatabaseName> SET COMPATIBILITY_LEVEL = 130`  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>深入了解 SQL Server 和 Azure SQL Database 中的 JSON  
  
### <a name="microsoft-videos"></a>Microsoft 影片

如需 SQL Server 和 Azure SQL Database 中內建 JSON 支援的觀看式簡介，請參閱下列影片：

- [SQL Server 2016 和 JSON 支援](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

- [使用 SQL Server 2016 和 Azure SQL Database 中的 JSON](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

- [NoSQL 與關聯式領域之間的橋樑 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>另請參閱  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  