---
title: "FOR JSON 如何逸出特殊字元和控制字元 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON, special characters
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 21d0e35636e7c34c395f8c2bfe4f5c7ea07a4d9b
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="how-for-json-escapes-special-characters-and-control-characters-sql-server"></a>FOR JSON 如何逸出特殊字元和控制字元 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  本主題描述 SQL Server **SELECT** 陳述式的 **FOR JSON** 子句如何逸出特殊字元，並在 JSON 輸出中代表控制字元。  

> [!IMPORTANT]
> 此頁面描述 Microsoft SQL Server 中的內建 JSON 支援。 如需 JSON 中逸出和編碼的一般資訊，請參閱 JSON RFC 的第 2.5 節 - [http://www.ietf.org/rfc/rfc4627.txt](http://www.ietf.org/rfc/rfc4627.txt)。

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
|…|…|  
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

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>深入了解 SQL Server 中的內建 JSON 支援  
如需更多特定的解決方案、使用案例和建議，請參閱 SQL Server 和 Azure SQL Database 中 Microsoft 經理專案 Jovan Popovic 所撰寫的[有關內建 JSON 支援的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)。
  
## <a name="see-also"></a>另請參閱  
 [使用 FOR JSON 將查詢結果格式化為 JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
[FOR 子句](../../t-sql/queries/select-for-clause-transact-sql.md)

