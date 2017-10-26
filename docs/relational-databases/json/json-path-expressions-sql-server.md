---
title: "JSON 路徑運算式 (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, path expressions
- path expressions (JSON)
ms.assetid: 25ea679c-84cc-4977-867c-2cbe9d192553
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 07c873941669f7a36ff9b93651a938ecae2662b7
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="json-path-expressions-sql-server"></a>JSON 路徑運算式 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 請使用 JSON 路徑運算式來參考 JSON 物件的屬性。  
  
 當您呼叫下列函數時，必須提供路徑運算式。  
  
-   呼叫 **OPENJSON** 以建立 JSON 資料的關聯檢視時。 如需詳細資訊，請參閱 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)。  
  
-   呼叫 **JSON_VALUE** 以從 JSON 文字擷取值時。 如需詳細資訊，請參閱 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)。  
  
-   呼叫 **JSON_QUERY** 以擷取 JSON 物件或陣列時。 如需詳細資訊，請參閱 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)。  
  
-   呼叫 **JSON_MODIFY** 以更新 JSON 字串中的屬性值時。 如需詳細資訊，請參閱 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)。  

## <a name="parts-of-a-path-expression"></a>路徑運算式的組成部分
 路徑運算式有兩個元件。  
  
1.  選擇性[路徑模式](#PATHMODE)，其值為 **lax** 或 **strict**。  
  
2.  [路徑](#PATH) 本身。  

##  <a name="PATHMODE"></a> Path mode  
 在路徑運算式的開頭，指定關鍵字 **lax** 或 **strict**以選擇性地宣告路徑模式。 預設值是 **lax**。  
  
-   在 **lax** 模式中，如果路徑運算式包含錯誤，函數會傳回空白值。 例如，如果您要求值 **$.name**，且 JSON 文字不包含 **name** 索引鍵，則函數會傳回 null，但不會引發錯誤。  
  
-   在 **strict** 模式中，如果路徑運算式包含錯誤，函數會引發錯誤。  

下列查詢會在路徑運算式中明確指定 `lax`模式。

```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{ ... }'

SELECT * FROM OPENJSON(@json, N'lax $.info')
```  
  
##  <a name="PATH"></a> Path  
 選擇性地宣告路徑模式之後，請指定路徑本身。  
  
-   貨幣符號 (`$`) 表示內容項目。  
  
-   屬性路徑是一組路徑步驟。 路徑步驟可包含下列元素和運算子。  
  
    -   索引鍵名稱。 例如， `$.name` 和 `$."first name"`。 如果索引鍵名稱以貨幣符號開頭或包含特殊字元 (例如空格)，請用引號括起。   
  
    -   陣列元素。 例如， `$.product[3]`。 以零為基底的陣列。  
  
    -   點運算子 (`.`) 表示物件的成員。 例如，在 `$.people[1].surname` 中，`surname` 是 `people` 的子系。
  
## <a name="examples"></a>範例  
 本節中的範例參考下列 JSON 文字。  
  
```json  
{
    "people": [{
        "name": "John",
        "surname": "Doe"
    }, {
        "name": "Jane",
        "surname": null,
        "active": true
    }]
}
```  
  
 下表顯示路徑運算式的一些範例。  
  
|路徑運算式|值|  
|---------------------|-----------|  
|$.people[0].name|John|  
|$.people[1]|{ "name": "Jane",  "surname": null, "active": true }|  
|$.people[1].surname|null|  
|$|{ "people": [ { "name": "John",  "surname": "Doe" },<br />   { "name": "Jane",  "surname": null, "active": true } ] }|  
  
## <a name="how-built-in-functions-handle-duplicate-paths"></a>內建函數處理重複路徑的方法  
 如果 JSON 文字包含重複的屬性 (例如相同層級上有兩個同名的索引鍵)，**JSON_VALUE** 和 **JSON_QUERY** 函數會傳回第一個符合路徑的值。 若要剖析包含重複索引鍵的 JSON 物件，請使用 **OPENJSON**，如下列範例所示。  
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{"person":{"info":{"name":"John", "name":"Jack"}}}'

SELECT value
FROM OPENJSON(@json,'$.person.info') 
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>深入了解 SQL Server 中的內建 JSON 支援  
如需更多特定的解決方案、使用案例和建議，請參閱 SQL Server 和 Azure SQL Database 中 Microsoft 經理專案 Jovan Popovic 所撰寫的[有關內建 JSON 支援的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)。
  
## <a name="see-also"></a>另請參閱  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
  

