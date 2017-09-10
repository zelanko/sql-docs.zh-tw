---
title: "CHARINDEX (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5049508aac52724bbf0b05c9962b154db7af1474
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="charindex-transact-sql"></a>CHARINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

在運算式中搜尋另一個運算式，並在找到時傳回它的開始位置。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
CHARINDEX ( expressionToFind , expressionToSearch [ , start_location ] )   
```  
  
## <a name="arguments"></a>引數  
*expressionToFind*  
是字元[運算式](../../t-sql/language-elements/expressions-transact-sql.md)，其中包含要尋找的順序。 *expressionToFind*限制為 8000 個字元。
  
*expressionToSearch*  
這是要搜尋的字元運算式。
  
*start_location*  
是**整數**或**bigint**是搜尋開始的運算式。 如果*start_location*未指定、 為負數，或為 0，搜尋就會在開頭*expressionToSearch*。
  
## <a name="return-types"></a>傳回型別
**bigint**如果*expressionToSearch*屬於**varchar （max)**， **nvarchar （max)**，或**varbinary （max)**資料型別。否則， **int**。
  
## <a name="remarks"></a>備註  
如果有任一個*expressionToFind*或*expressionToSearch*是 Unicode 資料類型 (**nvarchar**或**nchar**) 和另一個無效，其他會轉換成 Unicode 資料類型。 CHARINDEX 不能與**文字**， **ntext**，和**映像**資料型別。
  
如果有任一個*expressionToFind*或*expressionToSearch*是 NULL，CHARINDEX 會傳回 NULL。
  
如果*expressionToFind*內找不到*expressionToSearch*，CHARINDEX 會傳回 0。
  
CHARINDEX 會以輸入的定序為基礎來執行比較。 若要執行指定定序的比較，您可以利用 COLLATE，將明確定序套用至輸入。
  
傳回的開始位置是以 1 為基準，而不是以 0 為基準。
  
0x0000 (**char(0)**) 是 Windows 定序中未定義的字元，不包含在 CHARINDEX 中。
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
當使用 SC 定序，同時*start_location*和傳回值 surrogate 字組計算成一個字元，而不是兩個。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。
  
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
下列範例會利用選擇性*start_location*開始搜尋參數`vital`第五個字元的`DocumentSummary`中的資料行[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]資料庫。
  
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
下列範例會顯示時的結果集*expressionToFind*內找不到*expressionToSearch*。
  
```sql
DECLARE @document varchar(64);  
  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('bike', @document);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`-----------`
  
 `0`  
  
`(1 row(s) affected)`
  
### <a name="d-performing-a-case-sensitive-search"></a>D. 執行區分大小寫的搜尋  
下列範例會執行區分大小寫的搜尋以下字串`'TEST'`中`'This is a Test``'`。
  
```sql
USE tempdb;  
GO  
--perform a case sensitive search  
SELECT CHARINDEX ( 'TEST',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`-----------`
  
 `0`  
  
下列範例會執行區分大小寫的搜尋以下字串`'Test'`中`'This is a Test'`。
  
```sql
  
USE tempdb;  
GO  
SELECT CHARINDEX ( 'Test',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`-----------`
  
 `13`  
  
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
  
`-----------`
  
 `13`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-searching-from-the-start-of-a-string-expression"></a>F. 從字串運算式的開始搜尋  
下列範例會傳回第一個位置的`is`中`This is a string`開始從字串中的位置 1 （第一個字元）。
  
```sql
SELECT CHARINDEX('is', 'This is a string');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`---------`
  
 `3`  
  
### <a name="g-searching-from-a-position-other-than-the-first-position"></a>G. 從第一個位置以外的位置執行搜尋  
下列範例會傳回第一個位置的`is`中`This is a string`，從第四個位置。
  
```sql
SELECT CHARINDEX('is', 'This is a string', 4);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`---------`
  
 `6`  
  
### <a name="h-results-when-the-string-is-not-found"></a>H. 找不到字串時的結果  
下列範例所示的傳回值時*string_pattern*搜尋字串中找不到。
  
```sql
SELECT TOP(1) CHARINDEX('at', 'This is a string') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`---------`
  
 `0`  
  
## <a name="see-also"></a>另請參閱
[字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[+ &#40;字串串連 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
[定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)
  
  



