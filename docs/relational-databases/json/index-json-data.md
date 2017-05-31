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
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cf3c58c7d71a98bfaa1f27611762bf7fb3fe8725
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="index-json-data"></a>索引 JSON 資料
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  資料庫索引可改善篩選和排序作業的效能。 若不使用索引，則 SQL Server 在您每次查詢資料時必須執行完整的資料表掃描。  
  
 JSON 並非 SQL Server 2016 中的內建資料類型，而 SQL Server 2016 並無自訂 JSON 索引。 不過，您可使用標準索引最佳化所有 JSON 文件的查詢。  
  
## <a name="index-json-properties-by-using-computed-columns"></a>使用計算資料行的索引 JSON 屬性  
 您將 JSON 資料儲存於 SQL Server 時，通常會想要依 JSON 文件的屬性來篩選或排序查詢結果。  
  
 在此範例中，AdventureWorks SalesOrderHeader 資料表具有包含各種銷售訂單相關資訊的「資訊」資料行 - 例如關於客戶、銷售人員、出貨/帳單地址等項目的資訊。 您想要使用來自「資訊」資料行的值，篩選客戶的銷售訂單。 以下是您想要使用索引最佳化的查詢。  
  
```tsql  
SELECT SalesOrderNumber,OrderDate,JSON_VALUE(Info,'$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info,'$.Customer.Name')=N'Aaron Campbell' 
```  
  
 若您想要針對 JSON 文件中的屬性加速篩選或 ORDER BY 子句處理，則可使用與其他資料行相同的索引。 不過，您無法直接參考 JSON 文件中的屬性。 首先您必須建立「虛擬資料行」，傳回您想要用於篩選的值。 然後您必須在該虛擬資料行建立索引。  
  
 下列範例會建立可用於索引的計算資料行，然後在該資料行上建立索引。 此範例會建立公開客戶名稱的資料行，其儲存於 JSON 文件中的 $.Customer.Name 路徑。  
  
```tsql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
  
 系統不會保存計算資料行。 其不會佔用資料表中的額外空間。 僅在需要重建索引時才會執行計算。  
  
 務必使用您計劃在查詢中所用的相同運算式，建立計算資料行 - 在此範例中為 `JSON_VALUE(Info, '$.Customer.Name')`。  
  
 您無須重寫查詢。 若您使用具 JSON_VALUE 函數的運算式，則 SQL Server 會查看具有相同運算式的同等計算資料行，並盡可能套用索引。 以下是此範例中的查詢執行計劃。  
  
 ![執行計畫](../../relational-databases/json/media/jsonindexblog1.png "執行計畫")  
  
 SQL Server 會使用索引搜尋非叢集索引，並尋找滿足指定條件的資料列，而不會使用完整資料表掃描。 接著其會在 SalesOrderHeader 資料表中使用索引鍵查詢，以擷取查詢中參考的其他資料行 -  在此範例中為 SalesOrderNumber 和 OrderDate。  
  
 若您在 JSON 索引中新增必要資料行，則可避免資料表執行此額外查詢作業。 您可新增這些資料行做為標準內含資料行，如下列範例所示。  
  
```tsql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
 在此情況下，SQL Server 不會讀取來自 SalesOrderHeader 資料表的其他資料，這是因為在非叢集 JSON 索引中已包含所有需要的資訊。 這是在查詢中合併 JSON 與資料行資料，以及針對工作負載建立最佳化索引的理想方法。  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>JSON 索引是感知定序的索引  
 感知定序是 JSON 索引的重要功能。 JSON_VALUE 函數產生的結果為文字值，其會繼承來自輸入運算式的定序。 因此，在索引中的值會使用來源資料行中定義的定序規則加以排序。  
  
 為了示範這點，下列範例會建立具有主索引鍵與 JSON 內容的簡單集合物件資料表。  
  
```tsql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
 上述命令會針對 JSON 資料行指定塞爾維亞文 (斯拉夫) 定序。 下列範例會在名稱屬性上填入資料表並建立索引。  
  
```tsql  
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
  
 上述命令會在計算資料行 vName 上建立標準索引，其代表來自 JSON $.name 屬性的值。 在塞爾維亞文 (斯拉夫) 字碼頁中，字母順序如下：‘А’、’Б’、’В’、’Г’、’Д’、’Ђ’、’Е’ 等等。索引中的項目順序會與塞爾維亞文 (斯拉夫) 規則相容，這是因為 JSON_VALUE 函數的結果會繼承其來自來源資料行的定序。 下列範例會查詢此集合物件，並依名稱排序結果。  
  
```tsql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 若您查看實際執行計劃，則會發現其使用來自非叢集索引的排序值。  
  
 ![執行計畫](../../relational-databases/json/media/jsonindexblog2.png "執行計畫")  
  
 雖然查詢具有 ORDER BY 子句，但執行計劃不會使用 Sort 運算子。 JSON 索引已根據塞爾維亞文 (斯拉夫) 規則執行排序。 因此，SQL Server 可在已排序的結果中，使用非叢集索引。  
  
 不過，若我們變更依運算式的順序定序 (例如在 JSON_VALUE 函數後方加上 `COLLATE French_100_CI_AS_SC` )，則會得到不同的查詢執行計劃。  
  
 ![執行計畫](../../relational-databases/json/media/jsonindexblog3.png "執行計畫")  
  
 由於索引中的值順序不符合法文定序規則，因此 SQL Server 無法使用索引來排序結果。 因此，其會使用法文定序規則新增 Sort 運算子來排序結果。  
  
  

