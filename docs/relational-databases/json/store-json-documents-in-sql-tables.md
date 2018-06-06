---
title: 將 JSON 文件儲存在 SQL Server 或 SQL Database | Microsoft Docs
ms.description: This article describes why and how to store and index JSON documents in SQL Server or SQL Database, and how to optimize queries over the JSON documents.
ms.custom: ''
ms.date: 01/04/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.openlocfilehash: 330e4d3bf4bf0059fc713d0b8969505e00d775c3
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34689196"
---
# <a name="store-json-documents-in-sql-server-or-sql-database"></a>將 JSON 文件儲存在 SQL Server 或 SQL Database
SQL Server 和 Azure SQL Database 有原生 JSON 函式，可讓您使用標準 SQL 語言剖析 JSON 文件。 現在您可以在 SQL Server 或 SQL Database 中儲存 JSON 文件和查詢 JSON 資料，如同在 NoSQL 資料庫中一樣。 本文描述將 JSON 文件儲存在 SQL Server 或 SQL Database 中的選項。

## <a name="classic-tables"></a>傳統的資料表

將 JSON 文件儲存在 SQL Server 或 SQL Database 的最簡單方式是建立雙資料行資料表，其中包含文件的識別碼和文件的內容。 例如：

```sql
create table WebSite.Logs (
    _id bigint primary key identity,
    log nvarchar(max)
);
```

這個結構相等於您可以在傳統文件資料庫中找到的集合。 主索引鍵 `_id` 是一個自動遞增的值，它為每份文件提供唯一的識別碼，而且可供快速查閱。 此結構對於您要依識別碼擷取文件或依識別碼更新儲存文件的傳統 NoSQL 案例而言是不錯的選擇。

Nvarchar(max) 資料類型可讓您儲存大小高達 2 GB 的 JSON 文件。 不過如果您確定 JSON 文件不大於 8 KB，基於效能的考量，我們建議您使用 NVARCHAR(4000) 而不要使用 NVARCHAR(max)。

在上述範例中建立的範例資料表假設，有效的 JSON 文件會儲存在 `log` 資料行。 如果您想要確定有效的 JSON 會儲存在 `log` 資料行，您可以新增資料行的 CHECK 條件約束。 例如：

```sql
ALTER TABLE WebSite.Logs
    ADD CONSTRAINT [Log record should be formatted as JSON]
                   CHECK (ISJSON(log)=1)
```

每次有人插入或更新資料表中的文件時，這個條件約束會驗證 JSON 文件已正確格式化。 如果沒有條件約束，資料表最適合插入，因為任何 JSON 文件會直接新增到資料行，而不進行任何處理。

當您將 JSON 文件儲存到資料表中時，您可以使用標準的 Transact-SQL 語言來查詢文件。 例如：

```sql
SELECT TOP 100 JSON_VALUE(log, ‘$.severity’), AVG( CAST( JSON_VALUE(log,’$.duration’) as float))
 FROM WebSite.Logs
 WHERE CAST( JSON_VALUE(log,’$.date’) as datetime) > @datetime
 GROUP BY JSON_VALUE(log, ‘$.severity’)
 HAVING AVG( CAST( JSON_VALUE(log,’$.duration’) as float) ) > 100
 ORDER BY AVG( CAST( JSON_VALUE(log,’$.duration’) as float) ) DESC
```

有一項強大的優點，就是您可以使用「任何」T-SQL 函式和查詢子句來查詢 JSON 文件。 SQL Server 和 SQL Database 不會導入查詢中您可用來分析 JSON 文件的任何條件約束。 您可以使用 `JSON_VALUE` 函式從 JSON 文件擷取值，並像任何其他值將其用於查詢。

可使用豐富的 T-SQL 查詢語法的這項功能是 SQL Server 和 SQL Database 與傳統 NoSQL 資料庫之間的主要差異 – 在 Transact-SQL 中，您可能有處理 JSON 資料所需的任何函式。

## <a name="indexes"></a>索引

如果您發現您的查詢經常以某個屬性來搜尋文件 (例如，JSON 文件中的 `severity` 屬性)，您可以在屬性上新增傳統的 NONCLUSTERED 索引以加速查詢。

您可以建立計算資料行，從指定的路徑 (也就是在路徑 `$.severity`) 上的 JSON 資料行公開 JSON 值，並在這個計算資料行上建立標準索引。 例如：

```sql
create table WebSite.Logs (
    _id bigint primary key identity,
    log nvarchar(max),

    severity AS JSON_VALUE(log, '$.severity'),
    index ix_severity (severity)
);
```

此範例中使用的計算資料行，是不會將額外的空間新增至資料表的非持續性或虛擬資料行。 它由索引 `ix_severity` 用來改善查詢的效能，如下列範例所示：

```sql
SELECT log
FROM Website.Logs
WHERE JSON_VALUE(log, '$.severity') = 'P4'
```

此索引的一項重要特性是感知定序。 如果原始的 NVARCHAR 資料行有 COLLATION 屬性 (例如，區分大小寫或日文)，則索引會根據語言規則或與 NVARCHAR 資料行建立關聯的區分大小寫規則而組織。 如果您正在為需要使用自訂語言規則來處理 JSON 文件的全球市場開發應用程式，這個感知定序可能是一項重要功能。

## <a name="large-tables--columnstore-format"></a>大型資料表和資料行存放區格式

如果您預期在集合中有大量的 JSON 文件，我們建議在集合上新增 CLUSTERED COLUMNSTORE 索引，如下列範例所示：

```sql
create sequence WebSite.LogID as bigint;
go
create table WebSite.Logs (
    _id bigint default(next value for WebSite.LogID),
    log nvarchar(max),

    INDEX cci CLUSTERED COLUMNSTORE
);
```

CLUSTERED COLUMNSTORE 索引能提供高資料壓縮 (最多 25 倍)，大幅減少您的儲存空間需求、降低儲存體的成本，以及提升您的工作負載 I/O 效能。 此外，CLUSTERED COLUMNSTORE 索引針對您 JSON 文件上的資料表掃描和分析而最佳化，因此這種類型的索引可能是記錄分析的最佳選項。

上述範例中使用序列物件將值指派給 `_id` 資料行。 序列和身分識別都是識別碼資料行的有效選項。

## <a name="frequently-changing-documents--memory-optimized-tables"></a>經常變更的文件和記憶體最佳化的資料表

如果您預期在集合中會有大量的更新、插入和刪除作業，您可以在記憶體最佳化資料表中儲存 JSON 文件。 記憶體最佳化的 JSON 集合一律會將資料保存在記憶體中，因此沒有儲存體 I/O 額外負荷。 此外，記憶體最佳化 JSON 集合完全無鎖定 – 也就是對文件的動作不會封鎖任何其他作業。

要將傳統集合轉換成記憶體最佳化的集合，您唯一要做的是在資料表定義之後指定 **with (memory_optimized=on)** 選項，如下列範例所示。 然後，您便有記憶體最佳化版本的 JSON 集合。

```sql
create table WebSite.Logs (
  _id bigint identity primary key nonclustered,
  log nvarchar(4000)
) with (memory_optimized=on)
```

記憶體最佳化的資料表是最適合經常變更之文件的選項。 當您考慮記憶體最佳化資料表時，也請考慮效能。 可能的話，請針對記憶體最佳化集合中的 JSON 文件使用 NVARCAR(4000) 而不是 NVARCHAR(max)，因為它可能會大幅提升效能。

如同傳統的資料表，您可以對使用計算資料行，公開在記憶體最佳化資料表中的欄位，新增索引。 例如：

```sql
create table WebSite.Logs (

  _id bigint identity primary key nonclustered,
  log nvarchar(4000),

  severity AS cast(JSON_VALUE(log, '$.severity') as tinyint) persisted,
  index ix_severity (severity)

) with (memory_optimized=on)
```

為了充分發揮效能，將 JSON 值轉換成可用來保存屬性值的最小可能類型。 在上述範例中，使用了 **tinyint**。

您也可以將更新 JSON 文件的 SQL 查詢，放在預存程序中以善加利用原生編譯。 例如：

```sql
CREATE PROCEDURE WebSite.UpdateData(@Id int, @Property nvarchar(100), @Value nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION

AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    UPDATE WebSite.Logs
    SET log = JSON_MODIFY(log, @Property, @Value)
    WHERE _id = @Id;

END
```

此原生編譯的程序會採用查詢，並建立執行查詢的 .DLL 程式碼。 原生編譯的程序是能更快速查詢和更新資料的方法。

## <a name="conclusion"></a>結論

SQL Server 和 SQL Database 中的原生 JSON 函式，讓您能像在 NoSQL 資料庫中一樣地處理 JSON 文件。 每個資料庫不論是關聯式還是 NoSQL，都有一些 JSON 資料處理方面的優缺點。 將 JSON 文件儲存在 SQL Server 或 SQL Database 的主要優點是 SQL 語言的完整支援。 您可以使用豐富的 Transact-SQL 語言來處理資料，以及設定各種不同的儲存體選項 (從高壓縮和快速分析用的資料行存放區索引，到無鎖定處理用的記憶體最佳化資料表)。 同時，您會受益於成熟的安全性和國際化功能，並且可以輕鬆地重複用於 NoSQL 案例中。 本文中所描述的理由是考慮將 JSON 文件儲存在 SQL Server 或 SQL Database 中的絕佳原因。

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>深入了解 SQL Server 和 Azure SQL Database 中的 JSON  
  
### <a name="microsoft-blog-posts"></a>Microsoft 部落格文章  
  
如需特定的解決方案、使用案例和建議，請參閱這些[部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)，了解 SQL Server 和 Azure SQL Database 中的內建 JSON 支援。  

### <a name="microsoft-videos"></a>Microsoft 影片

如需 SQL Server 和 Azure SQL Database 中內建 JSON 支援的觀看式簡介，請參閱下列影片：

-   [SQL Server 2016 和 JSON 支援](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [使用 SQL Server 2016 和 Azure SQL Database 中的 JSON](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL 與關聯式領域之間的橋樑 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
