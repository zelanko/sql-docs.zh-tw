---
title: "uniqueidentifier (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- uniqueidentifier
- uniqueidentifier_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- uniqueidentifier data type
- globally unique identifiers [SQL Server]
- GUIDs [SQL Server]
ms.assetid: b026035b-f3d2-4d70-989d-3884b4ca0233
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: d9a995f7d29fe91e14affa9266a9bce73acc9010
ms.openlocfilehash: 1450aa86e3f47ef27be5acd5b5410fe40dd5983e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="uniqueidentifier-transact-sql"></a>uniqueidentifier (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

這是 16 位元組的 GUID。
  
## <a name="remarks"></a>備註  
資料行或本機變數**uniqueidentifier**資料型別可以下列方式初始化為一個值：
-   使用 NEWID 函數。  
-   從字串常數形式轉換*xxxxxxxx*-*xxxx*-*xxxx*-*xxxx*- *xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx*，每位*x*是範圍 0-9 或 a-f 的十六進位數字。 例如，6F9619FF-8B86-D011-B42D-00C04FC964FF 是有效**uniqueidentifier**值。  
  
比較運算子可以搭配**uniqueidentifier**值。 不過排序並不是比較兩值的位元模式加以實作的。 可以針對執行的運算只有**uniqueidentifier**值是一種比較 (=、 <>， \<，>， \<=、 > =) 以及檢查 NULL （IS NULL 和 IS NOT NULL）。 其他算術運算子一律不能使用。 所有資料行條件約束和身分識別，以外的屬性，可以用於**uniqueidentifier**資料型別。
  
合併式複寫和異動複寫具有更新訂閱使用**uniqueidentifier**保證個資料表的多個複本可唯一識別資料列的資料行。
  
## <a name="converting-uniqueidentifier-data"></a>轉換 Uniqueidentifier 資料  
**Uniqueidentifier**類型轉換為字元運算式，從的用途而言都視為字元類型，因此容易將轉換為字元類型之截斷規則。 亦即，將字元運算式轉換成不同大小的字元資料類型時，對新資料類型而言太大的值會被截斷。 請參閱＜範例＞一節。
  
## <a name="limitations-and-restrictions"></a>限制事項

這些工具和功能不支援`uniqueidentifier`資料類型：
- PolyBase
- [dwloader 載入工具](https://msdn.microsoft.com/sql/analytics-platform-system/dwloader)平行資料倉儲

## <a name="examples"></a>範例  
下列範例會將 `uniqueidentifier` 值轉換成 `char` 資料類型。
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
下列範例會示範當值對於要轉換的目標資料類型而言太大時，資料的截斷方式。 因為**uniqueidentifier**類型限制為 36 個字元，超過該長度的字元會被截斷。
  
```sql
DECLARE @ID nvarchar(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';  
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[NEWID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/newid-transact-sql.md)  
[NEWSEQUENTIALID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/newsequentialid-transact-sql.md) 
[設定@local_variable&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)
  
  

