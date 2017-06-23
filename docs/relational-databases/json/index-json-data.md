---
title: "索引 JSON 資料 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, indexing JSON data
- indexing JSON data
ms.assetid: ced241e1-ff09-4d6e-9f04-a594a9d2f25e
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 3ed7a51b28d2b17b3239f971d0f4f684bec145cd
ms.contentlocale: zh-tw
ms.lasthandoff: 06/23/2017

---
# <a name="index-json-data"></a>索引 JSON 資料
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

在 SQL Server 2016 中，JSON 不是內建資料類型，以及 SQL Server 並沒有自訂 JSON 索引。 您可以最佳化查詢所有 JSON 文件，不過，使用標準索引。 

資料庫索引可改善篩選和排序作業的效能。 若不使用索引，則 SQL Server 在您每次查詢資料時必須執行完整的資料表掃描。  
  
## <a name="index-json-properties-by-using-computed-columns"></a>使用計算資料行的索引 JSON 屬性  
當您將 JSON 資料儲存在 SQL Server 時，通常您想要篩選或排序查詢結果的一個或多個*屬性*JSON 文件。  

### <a name="example"></a>範例 
在此範例中，假設 AdventureWorks`SalesOrderHeader`資料表有`Info`包含各種銷售訂單相關以 JSON 格式資訊的資料行。 例如，其包含客戶、 銷售人員、 出貨和帳單地址等等的相關資訊。 您想要使用來自值`Info`篩選客戶的銷售訂單的資料行。

### <a name="query-to-optimize"></a>若要最佳化的查詢
以下是查詢的您想要使用索引最佳化類型的範例。  
  
```sql  
SELECT SalesOrderNumber,
    OrderDate,
    JSON_VALUE(Info, '$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info, '$.Customer.Name') = N'Aaron Campbell' 
```  

### <a name="example-index"></a>範例索引
如果您想要加速您的篩選條件或`ORDER BY`子句的 JSON 文件中的屬性上，您可以使用您已在其他資料行使用相同的索引。 不過，您不能*直接*參考 JSON 文件中的屬性。
    
1.  首先，您必須建立 「 虛擬資料行 」，傳回您想要用於篩選的值。
2.  然後您必須在該虛擬資料行建立索引。  
  
下列範例會建立可用於索引的計算資料行。 然後它會在新的計算資料行上建立索引。 這個範例會建立公開客戶名稱會儲存在資料行`$.Customer.Name`JSON 資料中的路徑。 
  
```sql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
### <a name="more-info-about-the-computed-column"></a>計算資料行的詳細資訊 
系統不會保存計算資料行。 僅在需要重建索引時才會執行計算。 其不會佔用資料表中的額外空間。   
  
請務必建立計算資料行具有相同運算式您打算使用您的查詢-在此範例中，運算式是`JSON_VALUE(Info, '$.Customer.Name')`。  
  
您無須重寫查詢。 如果您使用具有運算式`JSON_VALUE`函式，如上述，範例查詢中所示 SQL Server 會查看，但具有相同運算式的同等計算資料行，並盡可能套用索引。

### <a name="execution-plan-for-this-example"></a>此範例中的執行計畫
以下是此範例中的查詢執行計畫。  
  
![執行計畫](../../relational-databases/json/media/jsonindexblog1.png "執行計畫")  
  
SQL Server 會使用索引搜尋非叢集索引，並尋找滿足指定條件的資料列，而不會使用完整資料表掃描。 然後它會使用中的索引鍵查閱`SalesOrderHeader`以擷取其他資料行中查詢-在此範例中，所參考的資料表`SalesOrderNumber`和`OrderDate`。  
 
### <a name="optimize-the-index-further-with-included-columns"></a>最佳化的索引進一步使用內含資料行
如果在索引中新增必要資料行，您可以避免此額外查詢資料表中。 您可以新增這些資料行做為標準內含資料行，如下列範例中，以擴充所示`CREATE INDEX`如上所示的範例。  
  
```sql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
SQL Server 沒有在此情況下會讀取來自其他資料`SalesOrderHeader`資料表，因為它需要的所有項目包含在非叢集 JSON 索引中。 這是合併 JSON 與資料行在查詢中的資料，以及針對您的工作負載建立最佳化索引的理想方法。  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>JSON 索引是感知定序的索引  
索引 JSON 資料的重要功能是感知定序的索引。 結果`JSON_VALUE`建立計算資料行時所使用的函式是其定序繼承來自輸入運算式的文字值。 因此，在索引中的值加以排序使用來源資料行中定義的定序規則。  
  
為了示範這點，下列範例會建立具有主索引鍵與 JSON 內容的簡單集合物件資料表。  
  
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
  
上述命令會建立標準索引計算資料行上`vName`，表示從 JSON 值`$.name`屬性。 在塞爾維亞文 (斯拉夫) 字碼頁中，字母順序如下：‘А’、’Б’、’В’、’Г’、’Д’、’Ђ’、’Е’ 等等。在索引中的項目順序會與塞爾維亞文 （斯拉夫） 規則相容因為結果`JSON_VALUE`函式會將其定序繼承的來源資料行。 下列範例會查詢此集合物件，並依名稱排序結果。  
  
```sql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 若您查看實際執行計劃，則會發現其使用來自非叢集索引的排序值。  
  
 ![執行計畫](../../relational-databases/json/media/jsonindexblog2.png "執行計畫")  
  
 雖然查詢具有`ORDER BY`子句中，執行計劃不會使用 Sort 運算子。 JSON 索引已根據塞爾維亞文 (斯拉夫) 規則執行排序。 因此，SQL Server 可在已排序的結果中，使用非叢集索引。  
  
 不過，若我們變更定序`ORDER BY`expression-例如，如果我們將`COLLATE French_100_CI_AS_SC`之後`JSON_VALUE`函式-我們取得不同的查詢執行計畫。  
  
 ![執行計畫](../../relational-databases/json/media/jsonindexblog3.png "執行計畫")  
  
 由於索引中的值順序不符合法文定序規則，因此 SQL Server 無法使用索引來排序結果。 因此，其會使用法文定序規則新增 Sort 運算子來排序結果。  
 
## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>深入了解內建 JSON 支援 SQL Server 中  
針對特定的解決方案，大量使用案例和建議，請參閱[有關內建 JSON 支援的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)Microsoft 經理專案 jovan popovic 的 Azure SQL Database 和 SQL Server 中。

