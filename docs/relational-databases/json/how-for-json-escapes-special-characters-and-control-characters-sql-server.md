---
title: FOR JSON 如何逸出特殊字元和控制字元 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON, special characters
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c3df2557120308cc77b0abbd3f9c3bc5eed73b36
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542498"
---
# <a name="how-for-json-escapes-special-characters-and-control-characters-sql-server"></a>FOR JSON 如何逸出特殊字元和控制字元 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  本主題描述 SQL Server **SELECT** 陳述式的 **FOR JSON** 子句如何逸出特殊字元，並在 JSON 輸出中代表控制字元。  

> [!IMPORTANT]
> 此頁面描述 Microsoft SQL Server 中的內建 JSON 支援。 如需 JSON 中逸出和編碼的一般資訊，請參閱 JSON RFC 的第 2.5 節 - [https://www.ietf.org/rfc/rfc4627.txt](https://www.ietf.org/rfc/rfc4627.txt)。

## <a name="escaping-of-special-characters"></a>逸出特殊字元  
如果來源資料包含特殊字元，**FOR JSON** 子句會以 `\` 逸出 JSON 輸出中的這些字元，如下表所示。 在屬性名稱和它們的值中都會發生這項逸出。  
  
|**特殊字元**|**逸出的輸出**|  
|---------------------------|--------------------------|  
|引號 (")|\\"|  
|反斜線 (\\)|\\\|  
|斜線 (/)|\\/|  
|退格鍵|\b|  
|換頁字元|\f|  
|新行|\n|  
|歸位字元|\r|  
|水平 Tab 鍵|\t|  
  
## <a name="control-characters"></a>控制字元  
如果來源資料包含控制字元，**FOR JSON** 子句會以 `\u<code>` 格式編碼 JSON 輸出中的這些字元，如下表所示。  
  
|**控制字元**|**編碼的輸出**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|...|...|  
|CHAR(31)|\u001f|  
  
## <a name="example"></a>範例  
 以下是來源資料的 **FOR JSON** 輸出範例，而來源資料包括特殊字元和控制字元。  
  
 查詢：  
  
```sql  
SELECT  
  'VALUE\    /  
  "' as [KEY\/"],  
  CHAR(0) as '0',  
  CHAR(1) as '1',  
  CHAR(31) as '31'  
FOR JSON PATH  
```  
  
 結果：  
  
```json  
{
    "KEY\\\t\/\"": "VALUE\\\t\/\r\n\"",
    "0": "\u0000",
    "1": "\u0001",
    "31": "\u001f"
}
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>深入了解 SQL Server 和 Azure SQL Database 中的 JSON  
  
### <a name="microsoft-blog-posts"></a>Microsoft 部落格文章  
  
如需特定的解決方案、使用案例和建議，請參閱這些[部落格文章](https://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)，了解 SQL Server 和 Azure SQL Database 中的內建 JSON 支援。  

### <a name="microsoft-videos"></a>Microsoft 影片

如需 SQL Server 和 Azure SQL Database 中內建 JSON 支援的觀看式簡介，請參閱下列影片：

-   [SQL Server 2016 和 JSON 支援](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [使用 SQL Server 2016 和 Azure SQL Database 中的 JSON](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL 與關聯式領域之間的橋樑 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>另請參閱  
 [使用 FOR JSON 將查詢結果格式化為 JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
[FOR 子句](../../t-sql/queries/select-for-clause-transact-sql.md)
