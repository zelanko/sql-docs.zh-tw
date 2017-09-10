---
title: "之間 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/28/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BETWEEN
- BETWEEN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- inclusive ranges
- testing range
- exclusive ranges
- NOT BETWEEN operator
- BETWEEN operator
- range to test [SQL Server]
ms.assetid: a5d5b050-203e-4355-ac85-e08ef5ca7823
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 71bc6e3bee0176f895dac6037219294acdab52d0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="between-transact-sql"></a>BETWEEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定要測試的範圍。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
test_expression [ NOT ] BETWEEN begin_expression AND end_expression  
```  
  
## <a name="arguments"></a>引數  
 *test_expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)來測試所定義的範圍中*begin_expression*和*end_expression*。 *test_expression*必須是相同的資料類型為 雙向*begin_expression*和*end_expression*。  
  
 NOT  
 指定執行否定運算的述詞結果。  
  
 *begin_expression*  
 任何有效的運算式。 *begin_expression*必須是相同的資料類型為 雙向*test_expression*和*end_expression*。  
  
 *end_expression*  
 任何有效的運算式。 *end_expression*必須是相同的資料類型為 雙向*test_expression*和*begin_expression*。  
  
 與  
 做為一個預留位置，表示*test_expression*應該在所指定的範圍內*begin_expression*和*end_expression*。  
  
## <a name="result-types"></a>結果類型  
 **布林**  
  
## <a name="result-value"></a>結果值  
 BETWEEN 會傳回**TRUE**如果的值*test_expression*大於或等於值*begin_expression*且小於或等於值*end_expression*。  
  
 NOT BETWEEN 會傳回**TRUE**如果的值*test_expression*的值少於*begin_expression*或更高的值*end_expression*.  
  
## <a name="remarks"></a>備註  
 若要指定獨佔範圍，請使用大於 (>) 和小於運算子 (<)。 如果 BETWEEN 或 NOT BETWEEN 述詞的任何輸入是 NULL，結果就是 UNKNOWN。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-between"></a>A. 使用 BETWEEN  
 下列範例會傳回資料庫中的資料庫角色的相關資訊。 第一個查詢會傳回所有角色。 第二個範例會使用`BETWEEN`子句來限制為指定的角色`database_id`值。  
  
```sql  
SELECT principal_id, name 
FROM sys.database_principals
WHERE type = 'R';

SELECT principal_id, name 
FROM sys.database_principals
WHERE type = 'R'
AND principal_id BETWEEN 16385 AND 16390;
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]   
```  
principal_id    name
------------  ---- 
0               public
16384           db_owner
16385           db_accessadmin
16386           db_securityadmin
16387           db_ddladmin
16389           db_backupoperator
16390           db_datareader
16391           db_datawriter
16392           db_denydatareader
16393           db_denydatawriter
```  
```  
principal_id    name
------------  ---- 
16385           db_accessadmin
16386           db_securityadmin
16387           db_ddladmin
16389           db_backupoperator
16390           db_datareader
```  
  
### <a name="b-using--and--instead-of-between"></a>B. 利用 > 和 < 來取代 BETWEEN  
 下列範例使用大於 (`>`) 和小於 (`<`) 運算子，因為這些運算子頭尾不包括在內，因此，不像前一個範例傳回 10 個資料列，它只會傳回 9 個資料列。  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.FirstName, e.LastName, ep.Rate  
FROM HumanResources.vEmployee e   
JOIN HumanResources.EmployeePayHistory ep   
    ON e.BusinessEntityID = ep.BusinessEntityID  
WHERE ep.Rate > 27 AND ep.Rate < 30  
ORDER BY ep.Rate;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 FirstName   LastName             Rate  
 ---------   -------------------  ---------  
 Paula       Barreto de Mattos    27.1394  
 Janaina     Bueno                27.4038  
 Dan         Bacon                27.4038  
 Ramesh      Meyyappan            27.4038  
 Karen       Berg                 27.4038  
 David       Bradley              28.7500  
 Hazem       Abolrous             28.8462  
 Ovidiu      Cracium              28.8462  
 Rob         Walters              29.8462  
 ```    
  
### <a name="c-using-not-between"></a>C. 使用 NOT BETWEEN  
 下列範例會找出不在指定範圍 `27` 到 `30` 之間的所有資料列。  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.FirstName, e.LastName, ep.Rate  
FROM HumanResources.vEmployee e   
JOIN HumanResources.EmployeePayHistory ep   
    ON e.BusinessEntityID = ep.BusinessEntityID  
WHERE ep.Rate NOT BETWEEN 27 AND 30  
ORDER BY ep.Rate;  
GO  
```  
  
### <a name="d-using-between-with-datetime-values"></a>D. 使用含有 datetime 值的 BETWEEN  
 下列範例會擷取資料列**datetime**之間的值為`'20011212'`和`'20020105'`(含） 之間。  
  
```sql  
-- Uses AdventureWorks  
  
SELECT BusinessEntityID, RateChangeDate  
FROM HumanResources.EmployeePayHistory  
WHERE RateChangeDate BETWEEN '20011212' AND '20020105';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 BusinessEntityID RateChangeDate  
 ----------- -----------------------  
 3           2001-12-12 00:00:00.000  
 4           2002-01-05 00:00:00.000  
 ```  
 
 此查詢會擷取預期的資料列，因為查詢中的日期值和**datetime**中所儲存值`RateChangeDate`指定沒有日期的時間部分的資料行。 未指定時間部分時，它會預設為上午 12:00。 請注意，若資料列包含 2002-01-05 上午 12:00 之後的時間部分， 此查詢將不會傳回該資料列，因為它是在範圍之外。  
  
  
## <a name="see-also"></a>另請參閱  
 [&#62;&#40;大於 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/greater-than-transact-sql.md)   
 [&#60;&#40;小於 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/less-than-transact-sql.md)   
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [其中 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  



