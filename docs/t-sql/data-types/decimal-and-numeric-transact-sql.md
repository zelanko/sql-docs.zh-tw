---
title: decimal 和 numeric (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9649da8ad800a65589cd934ab6aa630788966103
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43061746"
---
# <a name="decimal-and-numeric-transact-sql"></a>decimal 和 numeric (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

具有固定有效位數和小數位數的數值資料類型。 Decimal 和 numeric 是同義字，可以交換使用。
  
## <a name="arguments"></a>引數  
**decimal**[ **(***p*[ **,***s*] **)**] and **numeric**[ **(***p*[ **,***s*] **)**]  
固定有效位數和小數位數的數字。 當使用最大有效位數時，有效的值是從 - 10^38 +1 到 10^38 - 1。 **decimal** 的 ISO 同義字是 **dec** 和 **dec(***p*, *s***)**。 **numeric** 在功能上相當於 **decimal**。
  
p (有效位數)  
可儲存的最大十進位數總數，小數點左右兩側都包括在內。 有效位數必須是從 1 到最大有效位數 38 的值。 預設有效位數是 18。
  
> [!NOTE]  
>  Informatica 只支援 16 個有效數字，無論指定的有效位數和小數位數為何。  
  
*s* (小數位數)  
小數點右側所能儲存的十進位數。 這個數字會從 *p* 中減去，以判斷小數點左邊的最大位數。 小數位數必須是從 0 到 *p* 的值。 只有在指定了有效位數時，才能指定小數位數。 預設小數位數是 0；因此，0 <= *s* \<= *p*。 最大儲存體大小會隨著有效位數而不同。
  
|有效位數|儲存體位元組|  
|---|---|
|1 - 9|5|  
|10-19|9|  
|20-28|13|  
|29-38|17|  
  
> [!NOTE]  
>  Informatica (透過 SQL Server PDW Informatica Connector 連線) 只支援 16 個有效數字，無論指定的有效位數和小數位數為何。  
  
## <a name="converting-decimal-and-numeric-data"></a>轉換 decimal 與 numeric 資料
對於 **decimal** 和 **numeric** 資料類型，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將每個有效位數和小數位數的特定結合視為不同的資料類型。 例如，**decimal(5,5)** 和 **decimal(5,0)** 會視為是不同的資料類型。
  
在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中，會使用必要的最小有效位數與小數位數，自動將有小數點的常數轉換成 **numeric** 資料值。 例如，常數 12.345 會轉換成有效位數 5、小數位數 3 的 **numeric** 值。
  
從 **decimal** 或 **numeric** 轉換成 **float** 或 **real** 可能會導致有效位數的遺失。 從 **int**、**smallint**、**tinyint**、**float**、**real**、**money**，或 **smallmoney** 轉換成 **decimal** 或 **numeric** 可能會導致溢位。
  
根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在將數字轉換成有效位數與小數位數較小的 **decimal** 或 **numeric** 值時會使用四捨五入。 但是，如果 SET ARITHABORT 選項是 ON，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在發生溢位時產生錯誤。 只是流失有效位數與小數位數還不足以產生錯誤。
  
將浮點值或實數值轉換成十進位或數值時，十進位值一定不會超過 17 個小數位數。 任何浮點值若 < 5E-18 一律會轉換為 0。
  
## <a name="examples"></a>範例  
下列範例會使用 **decimal** 和 **numeric** 資料類型建立資料表。  值插入每個資料行，並透過 SELECT 陳述式傳回結果。
  
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
[sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
