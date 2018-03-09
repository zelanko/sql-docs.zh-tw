---
title: "索引 JSON 資料 | Microsoft Docs"
ms.custom: 
ms.date: 06/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, indexing JSON data
- indexing JSON data
ms.assetid: ced241e1-ff09-4d6e-9f04-a594a9d2f25e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0b6df549ab64edfcc766b4839cf17cc1814efa36
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="index-json-data"></a>索引 JSON 資料
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

在 SQL Server 和 SQL Database 中，JSON 並非內建的資料類型，而且 SQL Server 並沒有自訂 JSON 索引。 不過，您可使用標準索引最佳化所有 JSON 文件的查詢。 

資料庫索引可改善篩選和排序作業的效能。 若不使用索引，則 SQL Server 在您每次查詢資料時必須執行完整的資料表掃描。  
  
## <a name="index-json-properties-by-using-computed-columns"></a>使用計算資料行的索引 JSON 屬性  
您將 JSON 資料儲存於 SQL Server 時，通常會想要依 JSON 文件的一或多個「屬性」來篩選或排序查詢結果。  

### <a name="example"></a>範例 
在此範例中，假設 AdventureWorks `SalesOrderHeader` 資料表含有 `Info` 資料行，其中包含關於銷售訂單的各種資訊 (JSON 格式)。 例如，它包含客戶、銷售人員、收件和帳單地址等相關資訊。 而您要使用資料行 `Info` 的值來篩選客戶的銷售訂單。

### <a name="query-to-optimize"></a>要最佳化的查詢
以下是要透過索引來最佳化的查詢類型的範例。  
  
```sql  
SELECT SalesOrderNumber,
    OrderDate,
    JSON_VALUE(Info, '$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info, '$.Customer.Name') = N'Aaron Campbell' 
```  

### <a name="example-index"></a>範例索引
若您想要針對 JSON 文件中的屬性加速篩選或 `ORDER BY` 子句處理，則可使用與其他資料行所用相同的索引。 不過，您無法「直接」參考 JSON 文件中的屬性。
    
1.  首先您必須建立「虛擬資料行」，傳回您想要用於篩選的值。
2.  然後您必須在該虛擬資料行建立索引。  
  
下列範例會建立可用於索引的計算資料行，然後在該資料行上建立索引。 然後它會在新的計算資料行上建立索引。 此範例會建立公開客戶名稱的資料行，其儲存於 JSON 文件中的 `$.Customer.Name` 路徑。 
  
```sql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
### <a name="more-info-about-the-computed-column"></a>計算資料行的詳細資訊 
系統不會保存計算資料行。 僅在需要重建索引時才會執行計算。 其不會佔用資料表中的額外空間。   
  
請務必使用您計劃在查詢中所用的相同運算式，建立計算資料行 - 在此範例中，運算式為 `JSON_VALUE(Info, '$.Customer.Name')`。  
  
您無須重寫查詢。 若您使用具有 `JSON_VALUE` 函式的運算式 (如之前的範例查詢所示)，則 SQL Server 會發現有一個具有相同運算式的同等計算資料行，並盡可能套用索引。

### <a name="execution-plan-for-this-example"></a>此範例中的執行計畫
以下是此範例中的查詢執行計畫。  
  
![執行計畫](../../relational-databases/json/media/jsonindexblog1.png "執行計畫")  
  
SQL Server 會使用索引搜尋非叢集索引，並尋找滿足指定條件的資料列，而不會使用完整資料表掃描。 接著，其會在 `SalesOrderHeader` 資料表中使用索引鍵查詢，以擷取查詢中參考的其他資料行 -  在此範例中為 `SalesOrderNumber` 和 `OrderDate`。  
 
### <a name="optimize-the-index-further-with-included-columns"></a>利用內含資料行進一步最佳化索引
若您在索引中新增必要資料行，則可避免資料表執行此額外查詢作業。 您可新增這些資料行作為標準內含資料行 (如下列範例所示)，以擴充之前的 `CREATE INDEX` 範例。  
  
```sql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
在此情況下，SQL Server 不必讀取來自 `SalesOrderHeader` 資料表的其他資料，這是因為在非叢集 JSON 索引中已包含所有需要的資訊。 此索引類型是在查詢中合併 JSON 與資料行資料，以及針對工作負載建立最佳化索引的理想方法。  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>JSON 索引是感知定序的索引  
JSON 資料之索引的重要功能是索引能夠感知定序。 您在建立計算資料行時所使用的 `JSON_VALUE` 函數的結果為文字值，其繼承來自輸入運算式的定序。 因此，在索引中的值會使用來源資料行中定義的定序規則加以排序。  
  
為了示範索引能夠感知定序，下列範例會建立具有主索引鍵與 JSON 內容的簡單集合資料表。  
  
```sql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
上述命令會針對 JSON 資料行指定塞爾維亞文 (斯拉夫) 定序。 下列範例會在名稱屬性上填入資料表並建立索引。  
  
```sql  
INSERT INTO JsonCollection
VALUES
(N'{"name":"Иво","surname":"Андрић"}'),
(N'{"name":"Андрија","surname":"Герић"}'),
(N'{"name":"Владе","surname":"Дивац"}'),
(N'{"name":"Новак","surname":"Ђоковић"}'),
(N'{"name":"Предраг","surname":"Стојаковић"}'),
(N'{"name":"Михајло","surname":"Пупин"}'),
(N'{"name":"Борислав","surname":"Станковић"}'),
(N'{"name":"Владимир","surname":"Грбић"}'),
(N'{"name":"Жарко","surname":"Паспаљ"}'),
(N'{"name":"Дејан","surname":"Бодирога"}'),
(N'{"name":"Ђорђе","surname":"Вајферт"}'),
(N'{"name":"Горан","surname":"Бреговић"}'),
(N'{"name":"Милутин","surname":"Миланковић"}'),
(N'{"name":"Никола","surname":"Тесла"}')
GO
  
ALTER TABLE JsonCollection
ADD vName AS JSON_VALUE(json,'$.name')

CREATE INDEX idx_name
ON JsonCollection(vName)
```  
  
上述命令會在計算資料行 `vName` 上建立標準索引，其代表來自 JSON `$.name` 屬性的值。 在塞爾維亞文 (斯拉夫) 字碼頁中，字母順序如下：‘А’、’Б’、’В’、’Г’、’Д’、’Ђ’、’Е’ 等等。索引中的項目順序會與塞爾維亞文 (斯拉夫) 規則相容，這是因為 `JSON_VALUE` 函數的結果會繼承其來自來源資料行的定序。 下列範例會查詢此集合物件，並依名稱排序結果。  
  
```sql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 若您查看實際執行計劃，則會發現其使用來自非叢集索引的排序值。  
  
 ![執行計畫](../../relational-databases/json/media/jsonindexblog2.png "執行計畫")  
  
 雖然查詢具有 `ORDER BY` 子句，但執行計畫不會使用 Sort 運算子。 JSON 索引已根據塞爾維亞文 (斯拉夫) 規則執行排序。 因此，SQL Server 可在已排序的結果中，使用非叢集索引。  
  
 不過，若您變更 `ORDER BY` 運算式的定序 (例如在 `JSON_VALUE` 函式後方新增 `COLLATE French_100_CI_AS_SC`)，則會得到不同的查詢執行計畫。  
  
 ![執行計畫](../../relational-databases/json/media/jsonindexblog3.png "執行計畫")  
  
 由於索引中的值順序不符合法文定序規則，因此 SQL Server 無法使用索引來排序結果。 因此，其會使用法文定序規則新增 Sort 運算子來排序結果。  
 
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>深入了解 SQL Server 和 Azure SQL Database 中的 JSON  
  
### <a name="microsoft-blog-posts"></a>Microsoft 部落格文章  
  
如需特定的解決方案、使用案例和建議，請參閱這些[部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)，了解 SQL Server 和 Azure SQL Database 中的內建 JSON 支援。  

### <a name="microsoft-videos"></a>Microsoft 影片

如需 SQL Server 和 Azure SQL Database 中內建 JSON 支援的觀看式簡介，請參閱下列影片：

-   [SQL Server 2016 與 JSON 支援](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [使用 SQL Server 2016 和 Azure SQL Database 中的 JSON](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL 與關聯式領域之間的橋樑 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
