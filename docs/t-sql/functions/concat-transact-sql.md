---
title: CONCAT (Transact-SQL) | Microsoft Docs
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
- CONCAT
- CONCAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT function
ms.assetid: fce5a8d4-283b-4c47-95e5-4946402550d5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1f3a1ef2b55b2f67b6b2e01ceb1965a5076e8476
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="concat-transact-sql"></a>CONCAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

傳回串連兩個以上之字串值的結果字串。 (若要在串連期間新增分隔值，請參閱[CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md)。)
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CONCAT ( string_value1, string_value2 [, string_valueN ] )  
```  
  
## <a name="arguments"></a>引數  
*string_value*  
要串連至其他值的字串值。
  
## <a name="return-types"></a>傳回類型
字串，其長度及類型取決於輸入。
  
## <a name="remarks"></a>Remarks  
**CONCAT** 會採用可變數量的字串引數，並將其連成單一字串。 其至少需要兩個輸入值，否則會引發錯誤。 所有引數皆會以隱含方式轉換為字串類型，然後再行串連。 Null 值以隱含方式轉換為空白字串。 如果所有引數都是 Null，會傳回類型為 **varchar**(1) 的空白字串。 隱含轉換成字串會遵循現有的資料類型轉換規則。 如需資料類型轉換的詳細資訊，請參閱 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)。
  
傳回類型取決於引數類型。 下表說明對應。
  
|輸入類型|輸出類型及長度|  
|---|---|
|如果有任何參數是 SQL CLR 系統類型、SQL CLR UDT 或 `nvarchar(max)`|**nvarchar(max)**|  
|否則，如有任何參數是 **varbinary (max)** 或 **varchar(max)**|**varchar(max)**，除非其中一個參數是任何長度的 **nvarchar**。 若是如此，則結果是 **nvarchar(max)**。|  
|否則，如有任何參數是 **nvarchar**(<= 4000)|**nvarchar**(<= 4000)|  
|否則，在所有其他情況下|**varchar**(<= 8000)，除非其中一個參數是任何長度的 nvarchar。 若是如此，則結果是 **nvarchar(max)**。|  
  
當 **nvarchar** 的引數為 <= 4000，或 **varchar** 的引數為 <= 8000 時，隱含轉換可能會影響結果的長度。 當其他資料類型以隱含方式轉換為字串時，長度會有所不同。 例如，**int** (14) 的字串長度為 12，而 **float**的長度為 32。 因此，串連兩個整數之後長度將不會小於 24。
  
如果輸入引數中無一是受支援的大型物件 (LOB) 類型，則無論傳回何種類型，傳回類型的長度皆會截斷成 8000。 此截斷可以保留空間，讓產生計畫更有效率。
  
CONCAT 函數可在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版及更高版本的連結伺服器上，以遠端方式執行。 對於較舊的連結伺服器，會在連結伺服器傳回非串連值之後，以本機方式執行 CONCAT 作業。
  
## <a name="examples"></a>範例  
  
### <a name="a-using-concat"></a>A. 使用 CONCAT  
  
```sql
SELECT CONCAT ( 'Happy ', 'Birthday ', 11, '/', '25' ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------  
Happy Birthday 11/25  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-concat-with-null-values"></a>B. 使用 CONCAT 搭配 NULL 值  
  
```sql
CREATE TABLE #temp (  
    emp_name nvarchar(200) NOT NULL,  
    emp_middlename nvarchar(200) NULL,  
    emp_lastname nvarchar(200) NOT NULL  
);  
INSERT INTO #temp VALUES( 'Name', NULL, 'Lastname' );  
SELECT CONCAT( emp_name, emp_middlename, emp_lastname ) AS Result  
FROM #temp;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
------------------  
NameLastname  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)   
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  


