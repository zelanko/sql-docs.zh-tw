---
title: "PATINDEX (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/19/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PATINDEX
- PATINDEX_TSQL
dev_langs: TSQL
helpviewer_keywords:
- first occurrence of pattern [SQL Server]
- searches [SQL Server], pattern starting position
- starting position of patten search
- pattern searching [SQL Server]
- PATINDEX function
ms.assetid: c0dfb17f-2230-4e36-98da-a9b630bab656
caps.latest.revision: "53"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: fd0df5a4dba946748dc39c245fcd54d50f1e97e5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
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
 *模式*  
 這是字元運算式，其中包含要尋找的順序。 可以使用萬用字元;不過，%字元必須放在之前，並且遵照*模式*（除非要搜尋第一個或最後一個字元）。 *模式*是字元字串資料類型類別目錄的運算式。 *模式*限制為 8000 個字元。  
  
 *expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)，通常搜尋指定模式的資料行。 *運算式*是字元字串資料類型類別目錄。  
  
## <a name="return-types"></a>傳回類型  
 **bigint**如果*運算式*屬於**varchar （max)**或**nvarchar （max)**資料類型，否則為**int**。  
  
## <a name="remarks"></a>備註  
 如果有任一個*模式*或*運算式*是 NULL，PATINDEX 會傳回 NULL。  
  
 PATINDEX 會以輸入的定序為基礎來執行比較。 若要執行指定定序的比較，您可以利用 COLLATE，將明確定序套用至輸入。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
 當使用 SC 定序時，傳回值將會計算任何 utf-16 surrogate 字組*運算式*參數做為單一字元。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
 0x0000 (**char(0)**) 是 Windows 定序中未定義的字元，不包含在 PATINDEX 中。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-patindex-example"></a>A. PATINDEX 的簡單範例  
 下列範例會檢查簡短字串 (`interesting data`) 的字元位置起始`ter`。  
  
```  
SELECT PATINDEX('%ter%', 'interesting data');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `3`  
  
### <a name="b-using-a-pattern-with-patindex"></a>B. 搭配 PATINDEX 使用模式  
 下列範例會尋找 `ensure` 模式在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫之 `DocumentSummary` 資料表中 `Document` 資料行之特定資料列中的起始位置。  
  
```  
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
  
```  
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
  
```  
USE tempdb;  
GO  
SELECT PATINDEX ( '%ein%', 'Das ist ein Test'  COLLATE Latin1_General_BIN) ;  
GO  
```  
  
### <a name="e-using-a-variable-to-specify-the-pattern"></a>E. 使用變數來指定模式  
 下列範例會使用變數值傳遞至*模式*參數。 這個範例會使用[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]資料庫。  
  
```  
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
  

  
## <a name="see-also"></a>請參閱＜  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [&#40;萬用字元-字元 &#40; s &#41;若要比對 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#40;萬用字元-字元 &#40; s &#41;不到相符項目 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)   
 [_ &#40;萬用字元-符合一個字元 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)   
 [百分比字元 &#40;萬用字元-字元 &#40; s &#41;若要比對 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)  
  
  


