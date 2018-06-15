---
title: int、bigint、smallint 和 tinyint (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 9/8/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- bigint_TSQL
- smallint
- bigint
- smallint_TSQL
- tinyint_TSQL
- int_TSQL
- int
- tinyint
dev_langs:
- TSQL
helpviewer_keywords:
- exact numeric data [SQL Server]
- numeric data
- tinyint data type
- int data type
- smallint data type
ms.assetid: 9bda5b0b-2380-4931-a1c8-f362fdefa99b
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ddd1dca194c6a80b627dafd62dff7f46ef96906b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33053775"
---
# <a name="int-bigint-smallint-and-tinyint-transact-sql"></a>int、bigint、smallint 和 tinyint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

使用整數資料的 Exact-number 資料類型。 若要節省資料庫中的空間，請使用能夠包含所有可能值的最小資料類型。 例如，若要儲存一個人的年齡，tinyint 便已足夠，因為沒有人的年齡會超過 255 歲。 但 tinyint 在用於建築物的屋齡上便可能不足，因為建築物的屋齡可超過 255 年。
  
|資料類型|範圍|Storage|  
|---|---|---|
|**bigint**|-2^63 (-9,223,372,036,854,775,808) 到 2^63-1 (9,223,372,036,854,775,807)|8 個位元組|  
|**int**|-2^31 (-2,147,483,648) 到 2^31-1 (2,147,483,647)|4 個位元組|  
|**smallint**|-2^15 (-32,768) 到 2^15-1 (32,767)|2 位元組|  
|**tinyint**|0 至 255|1 位元組|  
  
## <a name="remarks"></a>Remarks  
**int** 資料類型是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的主要整數資料類型。 **bigint** 資料類型通常是在整數值可能超過 **int** 資料類型所支援的範圍時使用。
  
**bigint** 位於資料類型優先順序圖表中 **smallmoney** 和 **int** 之間。
  
僅當參數運算式的資料類型是 **bigint** 時，函式才會傳回 **bigint**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會自動將其他整數類型 (**tinyint**、**smallint**，及 **int**) 提升為 **bigint**。
  
> [!CAUTION]  
>  當您使用 +、-、\*、/ 或 % 算術運算子，以隱含或明確方式，將 **int**、**smallint**、**tinyint** 或 **bigint** 常數值轉換為 **float**、**real**、**decimal** 或 **numeric** 資料類型時， 在計算運算式結果的資料類型和有效位數時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所套用的規則，會根據查詢是否自動參數化而有所不同。  
>   
>  因此，查詢中類似的運算式，有時候也會產生不同的結果。 如果查詢不是自動參數化，則常數值會先轉換為 **numeric** (其有效位數只是剛好可以容納常數值) 之後，再轉換為指定的資料類型。 例如，常數值 1 會轉換成 **numeric (1, 0)**，常數值 250 則會轉換成 **numeric (3, 0)**。  
>   
>  當查詢經過自動參數化時，常數值一律會先轉換為 **numeric (10, 0)**，再轉換為最終資料類型。 如果有用到 / 運算子，則不僅類似查詢的結果類型有效位數不同，結果值也可能不一樣。 例如，包含運算式 `SELECT CAST (1.0 / 7 AS float)` 的自動參數化查詢結果值，與非自動化參數之相同查詢的結果值不同，因為自動化參數的查詢結果，會配合 **numeric (10, 0)** 資料類型而被截斷。  
  
## <a name="converting-integer-data"></a>轉換整數資料
當整數隱含地轉換成字元資料類型時，如果該整數太大而無法放入字元欄位中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會輸入 ASCII 字元 42，也就是星號 (*)。
  
大於 2,147,483,647 的整數常數會轉換成 **decimal** 資料類型，而不是 **bigint** 資料類型。 下列範例顯示當超出臨界值時，結果的資料類型會從 **int** 變更為 **decimal**。
  
```sql
SELECT 2147483647 / 2 AS Result1, 2147483649 / 2 AS Result2 ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result1      Result2  
1073741823   1073741824.500000  
```  
  
## <a name="examples"></a>範例  
下列範例會使用 **bigint**、**int**、**smallint**，和 **tinyint** 資料類型建立資料表。 值插入每個資料行，並在 SELECT 陳述式中傳回值。
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyBigIntColumn bigint  
,MyIntColumn  int
,MySmallIntColumn smallint
,MyTinyIntColumn tinyint
);  
  
GO  
  
INSERT INTO dbo.MyTable VALUES (9223372036854775807, 2147483647,32767,255);  
 GO  
SELECT MyBigIntColumn, MyIntColumn, MySmallIntColumn, MyTinyIntColumn  
FROM dbo.MyTable;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyBigIntColumn       MyIntColumn MySmallIntColumn MyTinyIntColumn  
-------------------- ----------- ---------------- ---------------  
9223372036854775807  2147483647  32767            255  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
