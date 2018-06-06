---
title: SOUNDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SOUNDEX
- SOUNDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SOUNDEX function
- comparing string data
- strings [SQL Server], similarity
- strings [SQL Server], comparing
- SOUNDEX values
ms.assetid: 8f1ed34e-8467-4512-a211-e0f43dee6584
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1256b573bd1fd2c1bee7de27e0a25a6dae3510a0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="soundex-transact-sql"></a>SOUNDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回四個字元的 (SOUNDEX) 代碼來評估兩個字串的相似度。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SOUNDEX ( character_expression )  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 為字元資料的英數[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 *character_expression* 可以是常數、變數或資料行。  
  
## <a name="return-types"></a>傳回類型  
 **varchar**  
  
## <a name="remarks"></a>Remarks  
 SOUNDEX 會根據字串發音，將英數字串轉換為四個字元的代碼。 代碼的第一個字元是 *character_expression* 的第一個字元，轉換成大寫。 代碼的第二到第四個字元是數字，代表運算式中的字母。 字母 A、E、I、O、U、H、W 和 Y 除非是字串的第一個字母，否則會忽略它們。 如果需要產生四個字元的代碼，則在尾端加入零。 如需 SOUNDEX 代碼的詳細資訊，請參閱 [Soundex 索引系統](https://www.archives.gov/research/census/soundex.html)。  
  
 不同字串的 SOUNDEX 代碼可以相比較，來查看字串發音相似度。 DIFFERENCE 函數會在兩個字串上執行 SOUNDEX，並傳回整數，表示這些字串的 SOUNDEX 代碼相似度。  
  
 SOUNDEX 會區分定序。 字串函數可以是巢狀函數。  
  
## <a name="soundex-compatibility"></a>SOUNDEX 相容性  
 在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，SOUNDEX 函數套用 SOUNDEX 規則的子集。 在資料庫相容性層級 110 或更高層級下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 套用一組更完整的規則。  
  
 升級到相容性層級 110 或更高層級之後，您可能需要重建使用 SOUNDEX 函式的索引、堆積或 CHECK 條件約束。  
  
-   在執行 `ALTER TABLE <table> REBUILD` 陳述式重建堆積之前，無法查詢包含使用 SOUNDEX 定義之保存的計算資料行的堆積。  
  
-   在升級後，會停用使用 SOUNDEX 定義的 CHECK 條件約束。 若要啟用條件約束，請執行 `ALTER TABLE <table> WITH CHECK CHECK CONSTRAINT ALL` 陳述式。  
  
-   如果索引 (包括索引檢視表) 包含使用 SOUNDEX 定義之保存的計算資料行，在執行 `ALTER INDEX ALL ON <object> REBUILD` 陳述式重建索引之前，將無法查詢這類索引。  
  
## <a name="examples"></a>範例  
 下列範例會顯示 SOUNDEX 函數和相關的 DIFFERENCE 函數。 在第一個範例中，傳回所有子音的標準 `SOUNDEX` 值。 傳回 `SOUNDEX` 和 `Smith` 的 `Smythe`，會傳回相同的 SOUNDEX 結果，因為所有母音、`y` 字母、雙重字母和 `h` 字母都不包括在內。  
  
```  
-- Using SOUNDEX  
SELECT SOUNDEX ('Smith'), SOUNDEX ('Smythe');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] 針對 Latin1_General 定序有效。  
  
```  
  
----- -----   
S530  S530    
  
(1 row(s) affected)  
```  
  
 `DIFFERENCE` 函數會比較 `SOUNDEX` 模式結果的差異。 下列範例會顯示母音不同的兩個字串。 傳回的差異是 `4`，這是最低的可能差異。  
  
```  
-- Using DIFFERENCE  
SELECT DIFFERENCE('Smithers', 'Smythers');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] 針對 Latin1_General 定序有效。  
  
```  
-----------   
4             
  
(1 row(s) affected)  
```  
  
 在下列範例中，字串的子音不同；因此，傳回的差異是 `2`，差異比較大。  
  
```  
SELECT DIFFERENCE('Anothers', 'Brothers');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] 針對 Latin1_General 定序有效。  
  
```  
-----------   
2             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [DIFFERENCE &#40;Transact-SQL&#41;](../../t-sql/functions/difference-transact-sql.md)   
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

