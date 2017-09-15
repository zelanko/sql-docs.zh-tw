---
title: "int、 bigint、 smallint 和 tinyint (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 46ac51971b07b38b73ef18d8a953674fc77b4b17
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="int-bigint-smallint-and-tinyint-transact-sql"></a>int、bigint、smallint 和 tinyint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

使用整數資料的 Exact-number 資料類型。 若要在資料庫中儲存空間，請使用可以可靠地包含所有可能值的最小資料類型。 比方說，tinyint 就足以說明人員時代，因為沒有人居住是 255 歲以上。 但 tinyint 不足夠建築物時代，由於一棟建築物可能超過 255 年。
  
|資料類型|範圍|儲存空間|  
|---|---|---|
|**bigint**|-2^63 (-9,223,372,036,854,775,808) 到 2^63-1 (9,223,372,036,854,775,807)|8 個位元組|  
|**int**|-2^31 (-2,147,483,648) 到 2^31-1 (2,147,483,647)|4 個位元組|  
|**smallint**|-2^15 (-32,768) 到 2^15-1 (32,767)|2 位元組|  
|**tinyint**|0 至 255|1 位元組|  
  
## <a name="remarks"></a>備註  
**Int**資料類型是中的主要整數資料類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 **Bigint**資料型別僅供使用時的整數值可能超過支援的範圍**int**資料型別。
  
**bigint**符合之間**smallmoney**和**int**資料類型優先順序圖表中。
  
函式會傳回**bigint**只有當參數運算式是**bigint**資料型別。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不會自動升級其他整數資料類型 (**tinyint**， **smallint**，和**int**) 至**bigint**。
  
> [!CAUTION]  
>  當您使用 +、-、 \*，/，或 %算術運算子來執行的隱含或明確轉換**int**， **smallint**， **tinyint**，或**bigint**常數值**float**，**真實**，**十進位**或**數值**資料類型、 規則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時它會計算的資料類型和運算式結果的有效位數而有所不同查詢是否為自動參數化，或不適用。  
>   
>  因此，查詢中類似的運算式，有時候也會產生不同的結果。 當查詢不是自動參數化時，常數值會先轉換為**數值**，其有效位數夠大正好足以容納常數的值，再轉換為指定的資料類型。 例如，常數值 1 會轉換成**numeric （1，0）**，250 的常數值會轉換為**數值 （3，0）**。  
>   
>  自動參數化查詢時，常數值一律會轉換成**數值 （10，0）**再轉換為最終資料類型。 如果有用到 / 運算子，則不僅類似查詢的結果類型有效位數不同，結果值也可能不一樣。 例如，包含運算式的自動參數化查詢的結果值`SELECT CAST (1.0 / 7 AS float)`，與不是自動參數化，同一個查詢的結果值不同，因為在自動參數化查詢的結果會截斷才能容納到**數值 （10，0）**資料型別。  
  
## <a name="converting-integer-data"></a>轉換整數資料
當整數隱含地轉換成字元資料類型時，如果該整數太大而無法放入字元欄位中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會輸入 ASCII 字元 42，也就是星號 (*)。
  
大於 2,147,483,647 會轉換成整數常數**十進位**資料類型，而不**bigint**資料型別。 下列範例示範當超過臨界值時，從變更結果的資料型別**int**至**十進位**。
  
```sql
SELECT 2147483647 / 2 AS Result1, 2147483649 / 2 AS Result2 ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result1      Result2  
1073741823   1073741824.500000  
```  
  
## <a name="examples"></a>範例  
下列範例會建立資料表，使用**bigint**， **int**， **smallint**，和**tinyint**資料型別。 值插入每個資料行，並在 SELECT 陳述式中傳回值。
  
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
[sys.types &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

