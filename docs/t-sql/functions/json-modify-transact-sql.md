---
title: "JSON_MODIFY (TRANSACT-SQL) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 96bc8255-a037-4907-aec4-1a9c30814651
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70f2c1456da6469c39389fada6a74ccf46383582
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="jsonmodify-transact-sql"></a>JSON_MODIFY (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  更新 JSON 字串中的屬性值，並傳回更新後的 JSON 字串。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
JSON_MODIFY ( expression , path , newValue )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 運算式。 通常變數或資料行包含 JSON 文字的名稱。  
  
 **JSON_MODIFY**如果傳回錯誤*運算式*未包含有效的 JSON。  
  
 *路徑*  
 指定要更新之屬性的 JSON 路徑運算式。

 *路徑*具有下列語法：  
  
 `[append] [ lax | strict ] $.<json path>`  
  
-   *附加*  
    指定新的值應該會附加至所參考的陣列的選擇性修飾詞 *\<json 路徑 >*。  
  
-   *lax*  
    指定所參考之屬性 *\<json 路徑 >*不必存在。 如果屬性不存在，JSON_MODIFY 會嘗試插入新的值，指定路徑上。 如果屬性不能插入路徑上，插入可能會失敗。 如果您未指定*lax*或*嚴格*， *lax*是預設的模式。  
  
-   *嚴格*  
    指定所參考之屬性 *\<json 路徑 >*必須是 JSON 運算式中。 如果屬性不存在，JSON_MODIFY 會傳回錯誤。  
  
-   *\<json 路徑 >*  
    指定要更新之屬性的路徑。 如需詳細資訊，請參閱[JSON 路徑運算式 &#40;SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
在[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]和[!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]，您可以提供變數的值為*路徑*。

**JSON_MODIFY**如果傳回錯誤的格式*路徑*不是有效的。  
  
 *newValue*  
 所指定之屬性的新值*路徑*。  
  
 Lax 模式中，在 JSON_MODIFY 會刪除指定之索引鍵，如果新的值為 NULL。  
  
如果值的類型是 NVARCHAR 或 VARCHAR，JSON_MODIFY 逸出所有的特殊字元，新值。 如果它是正確的文字值未逸出格式 FOR JSON、 JSON_QUERY 或 JSON_MODIFY 所產生的 JSON。  
  
## <a name="return-value"></a>傳回值  
 傳回的更新的值*運算式*為正確格式的 JSON 文字。  
  
## <a name="remarks"></a>備註  
 JSON_MODIFY 函數可讓您更新現有屬性的值、 插入新的索引鍵： 值配對，或刪除基礎模式的組合，並提供值的索引鍵。  
  
 下表將比較的行為**JSON_MODIFY** lax 模式和 strict 模式。 如需詳細的選擇性路徑模式規格 （lax 或 strict） 的詳細資訊，請參閱[JSON 路徑運算式 &#40;SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|現有的值|路徑存在|Lax 模式|Strict 模式|  
|--------------------|-----------------|--------------|-----------------|  
|不是 NULL|是|更新現有的值。|更新現有的值。|  
|不是 NULL|否|嘗試在指定的路徑上建立新的索引鍵： 值配對。<br /><br /> 這可能會失敗。 例如，如果您指定的路徑`$.user.setting.theme`，JSON_MODIFY 不會插入索引鍵`theme`如果`$.user`或`$.user.settings`物件不存在，或如果設定為陣列或純量值。|錯誤 – INVALID_PROPERTY|  
|NULL|是|刪除現有的屬性。|將現有的值設定為 null。|  
|NULL|否|執行任何動作。 第一個引數會傳回結果。|錯誤 – INVALID_PROPERTY|  
  
 在 lax 模式中，JSON_MODIFY 嘗試建立新的索引鍵： 值配對，但在某些情況下可能會失敗。  
  
## <a name="examples"></a>範例  
  
### <a name="example---basic-operations"></a>範例-基本作業  
 下列範例可以使用 JSON 文字的基本作業。  
  
 **查詢**  
  
```sql  

DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update name  

SET @info=JSON_MODIFY(@info,'$.name','Mike')

PRINT @info

-- Insert surname  

SET @info=JSON_MODIFY(@info,'$.surname','Smith')

PRINT @info

-- Delete name  

SET @info=JSON_MODIFY(@info,'$.name',NULL)

PRINT @info

-- Add skill  

SET @info=JSON_MODIFY(@info,'append $.skills','Azure')

PRINT @info
```  
  
 **結果**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---multiple-updates"></a>範例-多個更新  
 使用 JSON_MODIFY 中，您可以更新只有一個屬性。 如果您有多個更新，您可以使用多個 JSON_MODIFY 呼叫。  
  
 **查詢**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Multiple updates  

SET @info=JSON_MODIFY(JSON_MODIFY(JSON_MODIFY(@info,'$.name','Mike'),'$.surname','Smith'),'append $.skills','Azure')

PRINT @info
```  
  
 **結果**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---rename-a-key"></a>範例-重新命名機碼  
 下列範例會示範如何重新命名使用 JSON_MODIFY 函數的 JSON 文字中的屬性。 首先，您可以使用現有屬性的值，並將它插入做為新的索引鍵： 值配對。 然後您可以刪除舊金鑰的舊屬性值設定為 NULL。  
  
 **查詢**  
  
```sql  
DECLARE @product NVARCHAR(100)='{"price":49.99}'

PRINT @product

-- Rename property  

SET @product=
 JSON_MODIFY(
  JSON_MODIFY(@product,'$.Price',CAST(JSON_VALUE(@product,'$.price') AS NUMERIC(4,2))),
  '$.price',
  NULL
 )

PRINT @product
```  
  
 **結果**  
  
```json  
{
    "price": 49.99
} {
    "Price": 49.99
}
```  
  
 如果您不要將新值轉換為數值類型，JSON_MODIFY 視為文字，並以雙引號括住它。  
  
### <a name="example---increment-a-value"></a>範例-遞增的值  
 下列範例會示範如何使用 JSON_MODIFY 函數的 JSON 文字中的屬性的值遞增。 首先，您可以使用現有屬性的值，並將它插入做為新的索引鍵： 值配對。 然後您可以刪除舊金鑰的舊屬性值設定為 NULL。  
  
 **查詢**  
  
```sql  
DECLARE @stats NVARCHAR(100)='{"click_count": 173}'

PRINT @stats

-- Increment value  

SET @stats=JSON_MODIFY(@stats,'$.click_count',
 CAST(JSON_VALUE(@stats,'$.click_count') AS INT)+1)

PRINT @stats
```  
  
 **結果**  
  
```json  
{
    "click_count": 173
} {
    "click_count": 174
}
```  
  
### <a name="example---modify-a-json-object"></a>範例-修改 JSON 物件  
 JSON_MODIFY 將*newValue*引數，即使它包含正確的純文字格式的 JSON 文字。 如此一來，JSON 輸出的函式以雙引號括住，所有的特殊字元會逸出，如下列範例所示。  
  
 **查詢**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array

SET @info=JSON_MODIFY(@info,'$.skills','["C#","T-SQL","Azure"]')

PRINT @info
```  
  
 **結果**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": "["C#","T-SQL","Azure"]"
}
```  
  
 若要避免自動逸出，請提供*newValue*使用 JSON_QUERY 函式。 JSON_MODIFY 知道 JSON_MODIFY 所傳回的值已正確格式化 JSON，因此它不會逸出值。  
  
 **查詢**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array  

SET @info=JSON_MODIFY(@info,'$.skills',JSON_QUERY('["C#","T-SQL","Azure"]'))

PRINT @info
```  
  
 **結果**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": ["C#", "T-SQL", "Azure"]
}
```  
  
### <a name="example---update-a-json-column"></a>範例-更新 JSON 資料行  
 下列範例會更新包含 JSON 的資料表資料行中的屬性值。  
  
```sql  
UPDATE Employee
SET jsonCol=JSON_MODIFY(jsonCol,"$.info.address.town",'London')
WHERE EmployeeID=17
 
```  
  
## <a name="see-also"></a>另請參閱  
 [JSON 路徑運算式 &#40;SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON 資料 &#40;SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  

