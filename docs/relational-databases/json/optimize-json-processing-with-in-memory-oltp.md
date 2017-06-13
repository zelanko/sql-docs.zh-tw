---
title: "使用記憶體內部 OLTP 最佳化 JSON 處理 | Microsoft Docs"
ms.custom: 
ms.date: 02/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d9c5adb1-3209-4186-bc10-8e41a26f5e57
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 12ef08a1f90e0346828a9dafb4052864254954d7
ms.contentlocale: zh-tw
ms.lasthandoff: 06/09/2017

---
# <a name="optimize-json-processing-with-in-memory-oltp"></a>使用記憶體內部 OLTP 最佳化 JSON 處理
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

SQL Server 和 Azure SQL Database 可讓您使用格式化為 JSON 的文字。 若要提高可處理 JSON 資料之 OLTP 查詢的效能，您可以使用標準字串資料行 (NVARCHAR 類型)，將 JSON 文件儲存到記憶體最佳化資料表中。

## <a name="store-json-in-memory-optimized-tables"></a>將 JSON 儲存到記憶體最佳化資料表
下列範例示範具有 `Tags` 和 `Data` 這兩個 JSON 資料行的記憶體最佳化 `Product` 資料表。

```sql
CREATE SCHEMA xtp;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED, --standard column
    Name nvarchar(400) NOT NULL, --standard column
    Price float, --standard column

    Tags nvarchar(400),--json stored in string column
    Data nvarchar(4000) --json stored in string column

) WITH (MEMORY_OPTIMIZED=ON);
```
將 JSON 資料儲存在記憶體最佳化資料表時，透過利用無鎖定的記憶體內部資料存取，即可提高查詢效能。

## <a name="optimize-json-with-additional-in-memory-features"></a>使用其他記憶體內部功能最佳化 JSON
SQL Server 和 Azure SQL Database 中提供的新功能可讓您完全整合 JSON 功能與現有記憶體內部 OLTP 技術。 例如，您可以執行下列動作：
 - 使用原生編譯 CHECK 條件約束，來驗證記憶體最佳化資料表中所儲存之 JSON 文件的結構。
 - 使用計算資料行來公開 JSON 文件中所儲存的值，並將其設為強型別。
 - 使用記憶體最佳化索引之 JSON 文件中的索引值。
 - 原生編譯 SQL 查詢，以使用 JSON 文件中的值，或將結果格式化為 JSON 文字。

## <a name="validate-json-columns"></a>驗證 JSON 資料行
SQL Server 和 Azure SQL Database 可讓您新增原生編譯 CHECK 條件約束，來驗證字串資料行中所儲存的 JSON 文件內容，如下列範例所示。

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Tags nvarchar(400)
            CONSTRAINT [Tags should be formatted as JSON]
                CHECK (ISJSON(Tags)=1),
    Data nvarchar(4000)

) WITH (MEMORY_OPTIMIZED=ON);
```

在包含 JSON 資料行的現有資料表上，可以新增原生編譯 CHECK 條件約束：

```sql
ALTER TABLE xtp.Product
    ADD CONSTRAINT [Data should be JSON]
        CHECK (ISJSON(Data)=1)
```

您可以使用原生編譯 JSON CHECK 條件約束，確保記憶體最佳化資料表中所儲存的 JSON 文字格式正確。

## <a name="expose-json-values-using-computed-columns"></a>使用計算資料行公開 JSON 值
計算資料行可讓您公開 JSON 文字中的值，以及存取這些值，而不需要重新評估可從 JSON 文字中擷取值的運算式，也不需要重新剖析 JSON 結構。 公開的值是強型別，並且會實際保存於計算資料行中。 使用保存計算資料行存取 JSON 值，會比存取 JSON 文件中的值還要快。

下列範例示範如何公開下列來自 JSON `Data` 資料行的兩個值：
-   產品的製作國家/地區。
-   產品製造成本。

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float)

) WITH (MEMORY_OPTIMIZED=ON);
```

每次 `Data` 資料行中所儲存的 JSON 文件變更時，都會更新計算資料行 `MadeIn` 和 `Cost`。

## <a name="index-values-in-json-columns"></a>編製 JSON 資料行中值的索引
SQL Server 和 Azure SQL Database 可讓您使用記憶體最佳化索引來編製 JSON 資料行中值的索引。 必須公開要編製索引的 JSON 值，並使用計算資料行將其設為強型別，如下列範例所示。

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float) PERSISTED,

    INDEX [idx_Product_MadeIn] NONCLUSTERED (MadeIn)

) WITH (MEMORY_OPTIMIZED=ON)

ALTER TABLE Product
    ADD INDEX [idx_Product_Cost] NONCLUSTERED HASH(Cost)
        WITH (BUCKET_COUNT=20000)
```
您可以使用標準 NONCLUSTERED 和 HASH 索引來編製 JSON 資料行中值的索引。
-   NONCLUSTERED 索引最佳化查詢的方式是依據某個 JSON 值來選取某範圍的資料列，或依 JSON 值來排序結果。
-   在指定要尋找的確切值來擷取一或多個資料列時，HASH 索引可提供最佳效能。

## <a name="native-compilation-of-json-queries"></a>JSON 查詢的原生編譯
最後，原生編譯 Transact-SQL 程序、函式和觸發程序包含使用 JSON 函式進行的查詢，可提高查詢的效能，並減少執行程序所需的 CPU 循環。 下列範例示範使用下列數個 JSON 函式的原生編譯程序：JSON_VALUE、OPENJSON 和 JSON_MODIFY。

```sql
CREATE PROCEDURE xtp.ProductList(@ProductIds nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    SELECT ProductID,Name,Price,Data,Tags, JSON_VALUE(data,'$.MadeIn') AS MadeIn
    FROM xtp.Product
        JOIN OPENJSON(@ProductIds)
            ON ProductID = value

END;

CREATE PROCEDURE xtp.UpdateProductData(@ProductId int, @Property nvarchar(100), @Value nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    UPDATE xtp.Product
    SET Data = JSON_MODIFY(Data, @Property, @Value)
    WHERE ProductID = @ProductId;

END
```

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>深入了解內建 JSON 支援 SQL Server 中  
針對特定的解決方案，大量使用案例和建議，請參閱[有關內建 JSON 支援的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)Microsoft 經理專案 jovan popovic 的 Azure SQL Database 和 SQL Server 中。

