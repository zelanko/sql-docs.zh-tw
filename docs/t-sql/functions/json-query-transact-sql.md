---
title: "JSON_QUERY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JSON_QUERY
- JSON_QUERY_TSQL
helpviewer_keywords:
- JSON, extracting
- JSON, querying
- JSON_QUERY function
ms.assetid: 1ab0d90f-19b6-4988-ab4f-22fdf28b7c79
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 310d85e26226cd54eff5d1c99e94b235348a90f7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="jsonquery-transact-sql"></a>JSON_QUERY (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 從 JSON 字串擷取物件或陣列。  
  
 若要從而不是物件或陣列的 JSON 字串擷取純量值，請參閱[JSON_VALUE &#40;TRANSACT-SQL &#41;](../../t-sql/functions/json-value-transact-sql.md). 如需之間的差異資訊**JSON_VALUE**和**JSON_QUERY**，請參閱[比較 JSON_VALUE 與 JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
JSON_QUERY ( expression [ , path ] )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 運算式。 通常變數或資料行包含 JSON 文字的名稱。  
  
 如果**JSON_QUERY**尋找不是有效的 JSON*運算式*它找到的值所識別之前*路徑*，函數會傳回錯誤。 如果**JSON_QUERY**找不到所識別的值*路徑*，它會掃描整個文字傳回錯誤，如果它發現 JSON 中的任何位置無效*運算式*。  
  
 *路徑*  
 指定物件或擷取陣列的 JSON 路徑。

在[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]和[!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]，您可以提供變數的值為*路徑*。

JSON 路徑可以指定用於剖析 lax 或 strict 模式。 如果您未指定剖析模式，lax 模式是預設值。 如需詳細資訊，請參閱[JSON 路徑運算式 &#40;SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  

預設值為*路徑*是 '$'。 如此一來，如果您沒有提供的值*路徑*， **JSON_QUERY**傳回輸入*運算式*。

如果格式*路徑*不是有效的**JSON_QUERY**會傳回錯誤。  
  
## <a name="return-value"></a>傳回值  
 傳回 JSON 片段類型 nvarchar （max）。 傳回值的定序時輸入運算式的定序相同。  
  
 如果值不是物件或陣列：  
  
-   在 lax 模式中， **JSON_QUERY**會傳回 null。  
  
-   在 strict 模式中， **JSON_QUERY**會傳回錯誤。  
  
## <a name="remarks"></a>備註  

### <a name="lax-mode-and-strict-mode"></a>Lax 模式和 strict 模式

 請考慮下列 JSON 文字：  
  
```json  
{
    "info": {
        "type": 1,
        "address": {
            "town": "Bristol",
            "county": "Avon",
            "country": "England"
        },
        "tags": ["Sport", "Water polo"]
    },
    "type": "Basic"
} 
```  
  
 下表將比較的行為**JSON_QUERY** lax 模式和 strict 模式。 如需詳細的選擇性路徑模式規格 （lax 或 strict） 的詳細資訊，請參閱[JSON 路徑運算式 &#40;SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|路徑|Lax 模式中的傳回值|在 strict 模式中的傳回值|其他資訊|  
|----------|------------------------------|---------------------------------|---------------|  
|$|傳回完整的 JSON 文字。|傳回完整的 JSON 文字。|N/a|  
|$。 info.type|NULL|錯誤|無法為物件或陣列。<br /><br /> 使用**JSON_VALUE**改為。|  
|$。 info.address.town|NULL|錯誤|無法為物件或陣列。<br /><br /> 使用**JSON_VALUE**改為。|  
|$.info。 」位址 」|N'{"城鎮":"Bristol"，"郡":"Avon 」、 「 國家/地區 」:"的 England"}'|N'{"城鎮":"Bristol"，"郡":"Avon 」、 「 國家/地區 」:"的 England"}'|N/a|  
|$。 info.tags|N '["運動"，"上限 polo"]'|N '["運動"，"上限 polo"]'|N/a|  
|$。 info.type[0]|NULL|錯誤|非陣列。|  
|$。 info.none|NULL|錯誤|屬性不存在。|  

### <a name="using-jsonquery-with-for-json"></a>使用 FOR JSON 與 JSON_QUERY

**JSON_QUERY**傳回有效的 JSON 片段。 如此一來， **FOR JSON**不逸出特殊字元**JSON_QUERY**傳回值。

如果您正在使用 FOR JSON，傳回結果，而且您要包括已經是 JSON 格式 （在資料行或運算式的結果） 的資料，換行的 JSON 資料**JSON_QUERY**沒有*路徑*參數。

## <a name="examples"></a>範例  
  
### <a name="example-1"></a>範例 1  
 下列範例示範如何傳回 JSON 片段從`CustomFields`查詢結果中的資料行。  
  
```sql  
SELECT PersonID,FullName,
 JSON_QUERY(CustomFields,'$.OtherLanguages') AS Languages
FROM Application.People
```  
  
### <a name="example-2"></a>範例 2  
下列範例會示範如何在 FOR JSON 子句的輸出中包含 JSON 片段。  
  
```sql  
SELECT StockItemID, StockItemName,
         JSON_QUERY(Tags) as Tags,
         JSON_QUERY(CONCAT('["',ValidFrom,'","',ValidTo,'"]')) ValidityPeriod
FROM Warehouse.StockItems
FOR JSON PATH
```  
  
## <a name="see-also"></a>請參閱＜  
 [JSON 路徑運算式 &#40;SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON 資料 &#40;SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
