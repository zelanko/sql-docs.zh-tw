---
title: "decimal 和 numeric (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- decimal
- decimal_TSQL
- numeric
- numeric_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decimal data type
- decimal data type, about decimal data type
- numeric data type
- numeric data type, about numeric data type
ms.assetid: 9d862a90-e6b7-4692-8605-92358dccccdf
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c6c8ec4ea2255e8496b6e5ed464fbff220d270e7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="decimal-and-numeric-transact-sql"></a>decimal 和 numeric (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

具有固定有效位數和小數位數的數值資料類型。 Decimal 和 numeric 是同義字，可以交換使用。
  
## <a name="arguments"></a>引數  
**十進位**[ **(***p*[ **，***s*] **)**] 和**數值**[ **(***p*[ **，***s*] **)**]  
固定有效位數和小數位數的數字。 當使用最大有效位數時，有效的值是從 - 10^38 +1 到 10^38 - 1。 ISO 同義字**十進位**是**dec**和**dec (***p*， *s***)**. **數值**其作用相當於**十進位**。
  
p (有效位數)  
可儲存的最大十進位數總數，小數點左右兩側都包括在內。 有效位數必須是從 1 到最大有效位數 38 的值。 預設有效位數是 18。
  
> [!NOTE]  
>  Informatica 只支援不論的有效位數和小數位數指定 16 有效位數。  
  
*s* （小數位數）  
小數點右側所能儲存的十進位數。 這個數字減去*p*以判斷小數點左邊數字的數目上限。 小數點右側所能儲存的最大十進位數。 小數位數必須介於 0 到*p*。 只有在指定了有效位數時，才能指定小數位數。 預設小數位數為 0;因此，0 < = *s* \< =  *p*。 最大儲存體大小會隨著有效位數而不同。
  
|有效位數|儲存體位元組|  
|---|---|
|1 - 9|5|  
|10-19|9|  
|20-28|13|  
|29-38|17|  
  
> [!NOTE]  
>  Informatica （透過 SQL Server PDW Informatica 連接器已連線） 只支援不論的有效位數和小數位數指定 16 有效位數。  
  
## <a name="converting-decimal-and-numeric-data"></a>轉換 decimal 和 numeric 資料
如**十進位**和**數值**資料型別，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會考慮不同的資料類型為每個特定組合的有效位數和小數位數。 例如， **decimal(5,5)**和**decimal(5,0)**會被視為不同的資料類型。
  
在[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式，以小數點的常數會自動轉換成**數值**資料值，使用最小有效位數，而且必要的調整規模。 例如，常數 12.345 會轉換成**數值**5 個有效位數與小數位數為 3 的值。
  
從轉換**十進位**或**數值**至**float**或**真實**可能會造成部分有效位數遺失。 從轉換**int**， **smallint**， **tinyint**， **float**，**真實**， **money**，或**smallmoney**為**十進位**或**數值**可能會造成溢位。
  
根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]轉換的數字時會使用四捨五入**十進位**或**數值**較低的有效位數和小數位數的值。 但是，如果 SET ARITHABORT 選項是 ON，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在發生溢位時產生錯誤。 只是流失有效位數與小數位數還不足以產生錯誤。
  
將浮點值或實數值轉換成十進位或數值時，十進位值一定不會超過 17 個小數位數。 任何浮點值若 < 5E-18 一律會轉換為 0。
  
## <a name="examples"></a>範例  
下列範例會建立資料表，使用**十進位**和**數值**資料型別。  值插入每個資料行，並透過 SELECT 陳述式傳回結果。
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyDecimalColumn decimal(5,2)  
,MyNumericColumn numeric(10,5)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (123, 12345.12);  
GO  
SELECT MyDecimalColumn, MyNumericColumn  
FROM dbo.MyTable;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyDecimalColumn                         MyNumericColumn  
--------------------------------------- ---------------------------------------  
123.00                                  12345.12000  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>另請參閱
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[sys.types &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

