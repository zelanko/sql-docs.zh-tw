---
title: CHARINDEX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHARINDEX
- CHARINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], pattern searching
- CHARINDEX function
- pattern searching [SQL Server]
- starting point of expression in character string
ms.assetid: 78c10341-8373-4b30-b404-3db20e1a3ac4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: ed2f5334c0c76288ca31cf07857a87f2d1c72033
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="charindex-transact-sql"></a>CHARINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

在運算式中搜尋另一個運算式，並在找到時傳回它的開始位置。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CHARINDEX ( expressionToFind , expressionToSearch [ , start_location ] )   
```  
  
## <a name="arguments"></a>引數  
*expressionToFind*  
這是字元[運算式](../../t-sql/language-elements/expressions-transact-sql.md)，其中包含要尋找的順序。 *expressionToFind* 限制為 8000 個字元。
  
*expressionToSearch*  
這是要搜尋的字元運算式。
  
*start_location*  
這是搜尋開始的**整數**或 **bigint** 運算式。 如果未指定 *start_location*，或者它是負數或 0，搜尋就會從 *expressionToSearch* 開頭開始。
  
## <a name="return-types"></a>傳回類型
若 *expressionToSearch* 的資料類型為 **varchar(max)**、**nvarchar(max)**，或 **varbinary(max)**，則為 **bigint**，否則為 **int**。
  
## <a name="remarks"></a>Remarks  
如果 *expressionToFind* 或 *expressionToSearch* 是 Unicode 資料類型 (**nvarchar** 或 **nchar**)，而其他的不是，則其他的會轉換為 Unicode 資料類型。 CHARINDEX 不得與 **text****ntext**和 **image** 資料類型一起使用。
  
如果 *expressionToFind* 或 *expressionToSearch* 為 NULL，則 CHARINDEX 會傳回 NULL。
  
如果在 *expressionToSearch*內找不到 *expressionToFind*，則 CHARINDEX 會傳回 0。
  
CHARINDEX 會以輸入的定序為基礎來執行比較。 若要執行指定定序的比較，您可以利用 COLLATE，將明確定序套用至輸入。
  
傳回的開始位置是以 1 為基準，而不是以 0 為基準。
  
0x0000 (**char(0)**) 是 Windows 定序中未定義的字元，而且不得包含在 CHARINDEX 中。
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
使用 SC 定序時，*start_location* 和傳回值會將代理字組計算成一個字元，而不是兩個字元。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-starting-position-of-an-expression"></a>A. 傳回運算式的開始位置  
下列範例會傳回 `bicycle` 字元序列在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫之 `DocumentSummary` 資料表 `Document` 資料行中的起始位置。
  
```sql
DECLARE @document varchar(64);  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('bicycle', @document);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------   
48            
```  
  
### <a name="b-searching-from-a-specific-position"></a>B. 從特定位置執行搜尋  
下列範例會利用選擇性的 *start_location* 參數，在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫之 `DocumentSummary` 資料行的第五個字元開始搜尋 `vital`。
  
```sql
DECLARE @document varchar(64);  
  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('vital', @document, 5);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------   
16            
  
(1 row(s) affected)  
```  
  
### <a name="c-searching-for-a-nonexistent-expression"></a>C. 搜尋不存在的運算式  
下列範例會顯示當 *expressionToSearch* 內找不到 *expressionToFind* 時的結果集。
  
```sql
DECLARE @document varchar(64);  
  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('bike', @document);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
0
  
(1 row(s) affected)
```
  
### <a name="d-performing-a-case-sensitive-search"></a>D. 執行區分大小寫的搜尋  
下列範例會在 `'This is a Test``'` 中，以區分大小寫的方式搜尋 `'TEST'` 字串。
  
```sql
USE tempdb;  
GO  
--perform a case sensitive search  
SELECT CHARINDEX ( 'TEST',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
0
```  
  
下列範例會在 `'This is a Test'` 中，以區分大小寫的方式搜尋 `'Test'` 字串。
  
```sql
  
USE tempdb;  
GO  
SELECT CHARINDEX ( 'Test',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
13
```  
  
### <a name="e-performing-a-case-insensitive-search"></a>E. 執行不區分大小寫的搜尋  
下列範例會在 `'TEST'` 中，以不區分大小寫的方式搜尋 `'This is a Test'` 字串。
  
```sql
  
USE tempdb;  
GO  
SELECT CHARINDEX ( 'TEST',  
       'This is a Test'  
       COLLATE Latin1_General_CI_AS);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
13
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-searching-from-the-start-of-a-string-expression"></a>F. 從字串運算式的開頭搜尋  
下列範例會傳回 `This is a string` 中 `is` 字串的第一個位置，從字串中的位置 1 (第一個字元) 開始。
  
```sql
SELECT CHARINDEX('is', 'This is a string');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
3
```  
  
### <a name="g-searching-from-a-position-other-than-the-first-position"></a>G. 從第一個位置以外的位置執行搜尋  
下列範例會傳回 `This is a string` 中 `is` 字串的第一個位置，從第四個位置開始。
  
```sql
SELECT CHARINDEX('is', 'This is a string', 4);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
 6
 ```  
  
### <a name="h-results-when-the-string-is-not-found"></a>H. 找不到字串時的結果  
下列範例會顯示在搜尋字串中找不到 *string_pattern* 時的傳回值。
  
```sql
SELECT TOP(1) CHARINDEX('at', 'This is a string') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
0
```  
  
## <a name="see-also"></a>另請參閱
 [LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)  
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
 [+ &#40;字串串連&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
 [定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  


