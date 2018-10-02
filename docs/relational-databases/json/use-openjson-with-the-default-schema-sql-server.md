---
title: 搭配使用 OPENJSON 與預設結構描述 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENJSON, with default schema
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ea2154045da369c045eea39591266cfb02f53722
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630219"
---
# <a name="use-openjson-with-the-default-schema-sql-server"></a>搭配使用 OPENJSON 與預設結構描述 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  搭配使用 **OPENJSON** 與預設結構描述來傳回一份資料表，其中物件的每個屬性或陣列中的每個項目都會有一個資料列。  
  
 以下是搭配使用 **OPENJSON** 與預設結構描述的一些範例。 如需詳細資訊和其他範例，請參閱 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)。  
  
## <a name="example---return-each-property-of-an-object"></a>範例 - 傳回物件的每個屬性  
 **[資料集屬性]**  
  
```sql  
SELECT *
FROM OPENJSON('{"name":"John","surname":"Doe","age":45}') 
```  
  
 **結果**  
  
|索引鍵|ReplTest1|  
|---------|-----------|  
|NAME|John|  
|surname|Doe|  
|age|45|  
  
## <a name="example---return-each-element-of-an-array"></a>範例 - 傳回陣列的每個元素  
 **[資料集屬性]**  
  
```sql  
SELECT [key],value
FROM OPENJSON('["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]') 
```  
  
 **結果**  
  
|索引鍵|ReplTest1|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
  
## <a name="example---convert-json-to-a-temporary-table"></a>範例 - 將 JSON 轉換成暫存資料表  
 下列查詢會傳回 **info** 物件的所有屬性。  
  
```sql  
DECLARE @json NVARCHAR(MAX)

SET @json=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }'

SELECT *
FROM OPENJSON(@json,N'lax $.info')
```  
  
 **結果**  
  
|索引鍵|ReplTest1|類型|  
|---------|-----------|----------|  
|型別|1|0|  
|address|{ "town":"Bristol", "county":"Avon", "country":"England" }|5|  
|標記|[ "Sport", "Water polo" ]|4|  
  
## <a name="example---combine-relational-data-and-json-data"></a>範例 - 合併關聯式資料和 JSON 資料  
 在下列範例中，SalesOrderHeader 資料表的 SalesReason 文字資料行包含 JSON 格式的 SalesOrderReasons 陣列。 SalesOrderReasons 物件包含 "Manufacturer" 和 "Quality" 這類屬性。 此範例所建立的報表會聯結每個銷售訂單資料列與相關銷售原因，方法是展開銷售原因的 JSON 陣列，就像原因是儲存在個別子資料表中一樣。  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
 在此範例中，OPENJSON 會傳回原因顯示為值欄位的銷售原因資料表。 CROSS APPLY 運算子會聯結每個銷售訂單資料列與 OPENJSON 資料表值函數所傳回的資料列。  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>深入了解 SQL Server 和 Azure SQL Database 中的 JSON  
  
### <a name="microsoft-blog-posts"></a>Microsoft 部落格文章  
  
如需特定的解決方案、使用案例和建議，請參閱這些[部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)，了解 SQL Server 和 Azure SQL Database 中的內建 JSON 支援。  

### <a name="microsoft-videos"></a>Microsoft 影片

如需 SQL Server 和 Azure SQL Database 中內建 JSON 支援的觀看式簡介，請參閱下列影片：

-   [SQL Server 2016 和 JSON 支援](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [使用 SQL Server 2016 和 Azure SQL Database 中的 JSON](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL 與關聯式領域之間的橋樑 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>另請參閱  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
