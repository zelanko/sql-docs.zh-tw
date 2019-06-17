---
title: PATINDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PATINDEX
- PATINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first occurrence of pattern [SQL Server]
- searches [SQL Server], pattern starting position
- starting position of patten search
- pattern searching [SQL Server]
- PATINDEX function
ms.assetid: c0dfb17f-2230-4e36-98da-a9b630bab656
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0a6f6f8c8699cc911d747d07edd9655fd363d667
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696975"
---
# <a name="patindex-transact-sql"></a>PATINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回指定之運算式中的模式，在所有有效文字和字元資料類型中第一次出現的起始位置，如果找不到模式，便傳回零。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
PATINDEX ( '%pattern%' , expression )  
```  
  
## <a name="arguments"></a>引數  
 *pattern*  
 這是字元運算式，其中包含要尋找的順序。 此處可以使用萬用字元，但是 *pattern* 前後都必須加上 % 字元 (除非要搜尋第一個或最後一個字元)。 *pattern* 是字元字串資料類型類別目錄的運算式。 *pattern* 限制為 8000 個字元。  
  
 *expression*  
 這是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)，通常是搜尋指定之模式的資料行。 *expression* 屬於字元字串資料類型類別目錄。  
  
## <a name="return-types"></a>傳回類型  
若 *expression* 的資料類型為 **varchar(max)** 或 **nvarchar(max)**，則為 **bigint**，否則為 **int**。  
  
## <a name="remarks"></a>Remarks  
如果 *pattern* 或 *expression* 為 NULL，則 PATINDEX 會傳回 NULL。  
 
PATINDEX 的起始位置是 1。
 
PATINDEX 會以輸入的定序為基礎來執行比較。 若要執行指定定序的比較，您可以利用 COLLATE，將明確定序套用至輸入。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
使用 SC 定序時，傳回值會將 *expression* 參數中的任何 UTF-16 代理字組計算為單一字元。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
0x0000 (**char(0)**) 是 Windows 定序中未定義的字元，而且不得包含在 PATINDEX 中。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-patindex-example"></a>A. 簡單的 PATINDEX 範例  
 下例範例會檢查 `ter`字元開頭位置的短字元字串 (`interesting data`)。  
  
```sql  
SELECT PATINDEX('%ter%', 'interesting data');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
`3`  
  
### <a name="b-using-a-pattern-with-patindex"></a>B. 搭配 PATINDEX 使用模式  
下列範例會尋找 `ensure` 模式在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫之 `DocumentSummary` 資料表中 `Document` 資料行之特定資料列中的起始位置。  
  
```sql  
SELECT PATINDEX('%ensure%',DocumentSummary)  
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
GO   
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
64  
(1 row(s) affected)
```  
  
如果您沒有利用 `WHERE` 子句來限制要搜尋的資料列，查詢會傳回資料表的所有資料列，且針對找到模式的所有資料列報告非零值，找不到模式的所有資料列則會報告零。  
  
### <a name="c-using-wildcard-characters-with-patindex"></a>C. 搭配 PATINDEX 使用萬用字元  
 下列範例在指定的字串中 (索引從 1 開始)，使用 % 和 _ 萬用字元來尋找模式 `'en'` 後面接著任何一個字元和 `'ure'` 的開始位置：  
  
```sql  
SELECT PATINDEX('%en_ure%', 'please ensure the door is locked');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
8  
```  
  
`PATINDEX` 的運作方式就像 `LIKE`，所以您可以使用任何萬用字元。 您不必用百分比括住模式。 `PATINDEX('a%', 'abc')` 會傳回 1 且 `PATINDEX('%a', 'cba')` 會傳回 3。  
  
 與 `LIKE` 不同的是，`PATINDEX` 會傳回位置，類似 `CHARINDEX`。  
  
### <a name="d-using-collate-with-patindex"></a>D. 搭配 PATINDEX 使用 COLLATE  
 下列範例利用 `COLLATE` 函數來明確指定所搜尋之運算式的定序。  
  
```sql  
USE tempdb;  
GO  
SELECT PATINDEX ( '%ein%', 'Das ist ein Test'  COLLATE Latin1_General_BIN) ;  
GO  
```  
  
### <a name="e-using-a-variable-to-specify-the-pattern"></a>E. 使用變數來指定模式  
下列範例會使用變數，將值傳遞給 *pattern* 參數。 這個範例會使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫。  
  
```sql  
DECLARE @MyValue varchar(10) = 'safety';   
SELECT PATINDEX('%' + @MyValue + '%', DocumentSummary)   
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
------------  
22
```  
  
## <a name="see-also"></a>另請參閱  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [CHARINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/charindex-transact-sql.md)  
 [LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [&#40;萬用字元 - 相符的字元&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#40;萬用字元 - 不相符的字元&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)   
 [_ &#40;萬用字元 - 符合單一字元&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)   
 [百分比字元&#40;萬用字元 - 相符的字元&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)  
  
  


