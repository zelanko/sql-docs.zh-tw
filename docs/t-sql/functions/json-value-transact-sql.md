---
title: "JSON_VALUE (TRANSACT-SQL) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JSON_VALUE
- JSON_VALUE_TSQL
helpviewer_keywords:
- JSON_VALUE function
- JSON, extracting
- JSON, querying
ms.assetid: cd016e14-11eb-4eaf-bf05-c7cfcc820a10
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ebb940035e4cad1ef898cfe83e1932db573848ab
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="jsonvalue-transact-sql"></a>JSON_VALUE (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  可從 JSON 字串擷取純量值。  
  
 若要擷取物件或陣列從 JSON 字串而非純量值，請參閱[JSON_QUERY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/json-query-transact-sql.md). 如需之間的差異資訊**JSON_VALUE**和**JSON_QUERY**，請參閱[比較 JSON_VALUE 與 JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
JSON_VALUE ( expression , path )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 運算式。 通常變數或資料行包含 JSON 文字的名稱。  
 
 如果**JSON_VALUE**尋找不是有效的 JSON*運算式*它找到的值所識別之前*路徑*，函數會傳回錯誤。 如果 **JSON_VALUE*找不到所識別的值*路徑*，它會掃描整個文字傳回錯誤，如果它發現 JSON 中的任何位置無效*運算式*。
  
 *路徑*  
 指定要擷取之屬性的 JSON 路徑。 如需詳細資訊，請參閱[JSON 路徑運算式 &#40;SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
 
在[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]和[!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]，您可以提供變數的值為*路徑*。
  
 如果格式*路徑*不是有效的**JSON_VALUE**會傳回錯誤。  
  
## <a name="return-value"></a>傳回值  
 傳回一個文字值的類型 nvarchar （4000）。 傳回值的定序時輸入運算式的定序相同。  
  
 如果值大於 4000 個字元：  
  
-   在 lax 模式中， **JSON_VALUE**會傳回 null。  
  
-   在 strict 模式中， **JSON_VALUE**會傳回錯誤。  
  
 如果您必須傳回純量值大於 4000 個字元，使用**OPENJSON**而不是**JSON_VALUE**。 如需詳細資訊，請參閱 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)。  
  
## <a name="remarks"></a>備註

### <a name="lax-mode-and-strict-mode"></a>Lax 模式和 strict 模式

 請考慮下列 JSON 文字：  
  
```json  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
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
```  
  
 下表將比較的行為**JSON_VALUE** lax 模式和 strict 模式。 如需詳細的選擇性路徑模式規格 （lax 或 strict） 的詳細資訊，請參閱[JSON 路徑運算式 &#40;SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|路徑|Lax 模式中的傳回值|在 strict 模式中的傳回值|其他資訊|  
|----------|------------------------------|---------------------------------|---------------|  
|$|NULL|錯誤|不是純量值。<br /><br /> 使用**JSON_QUERY**改為。|  
|$。 info.type|N '1'|N '1'|N/a|  
|$。 info.address.town|N'Bristol'|N'Bristol'|N/a|  
|$.info。 」位址 」|NULL|錯誤|不是純量值。<br /><br /> 使用**JSON_QUERY**改為。|  
|$。 info.tags|NULL|錯誤|不是純量值。<br /><br /> 使用**JSON_QUERY**改為。|  
|$。 info.type[0]|NULL|錯誤|非陣列。|  
|$。 info.none|NULL|錯誤|屬性不存在。|  
  
## <a name="examples"></a>範例  
  
### <a name="example-1"></a>範例 1  
 下列範例會使用 JSON 屬性的值`town`和`state`查詢結果中。 因為**JSON_VALUE**來源，結果的排序次序的定序取決於定序會保留`jsonInfo`資料行。  
  
```sql  
SELECT FirstName,LastName,
 JSON_VALUE(jsonInfo,'$.info.address[0].town') AS Town
FROM Person.Person
WHERE JSON_VALUE(jsonInfo,'$.info.address[0].state') LIKE 'US%'
ORDER BY JSON_VALUE(jsonInfo,'$.info.address[0].town')
```  
  
### <a name="example-2"></a>範例 2  
 下列範例會擷取 JSON 屬性的值`town`放入本機變數。  
  
```sql  
DECLARE @jsonInfo NVARCHAR(MAX)
DECLARE @town NVARCHAR(32)

SET @jsonInfo=N'<array of address info>'

SET @town=JSON_VALUE(@jsonInfo,'$.info.address.town')
```  
  
### <a name="example-3"></a>範例 3  
 下列範例會建立 JSON 屬性的值為基礎的計算資料行。  
  
```sql  
CREATE TABLE dbo.Store
 (
  StoreID INT IDENTITY(1,1) NOT NULL,
  Address VARCHAR(500),
  jsonContent NVARCHAR(8000),
  Longitude AS JSON_VALUE(jsonContent, '$.address[0].longitude'),
  Latitude AS JSON_VALUE(jsonContent, '$.address[0].latitude')
 )
```  
  
## <a name="see-also"></a>另請參閱  
 [JSON 路徑運算式 &#40;SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON 資料 &#40;SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  

