---
description: uniqueidentifier (Transact-SQL)
title: uniqueidentifier (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bf9ac8c8f907da233cc1168df7d4e81cb42c6c53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88368234"
---
# <a name="uniqueidentifier-transact-sql"></a>uniqueidentifier (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

這是 16 位元組的 GUID。
  
## <a name="remarks"></a>備註  
**uniqueidentifier** 資料類型的資料行或本機變數可以利用下列方法，初始化為一個值：
-   使用 [NEWID](../../t-sql/functions/newid-transact-sql.md) 或 [NEWSEQUENTIALID](../../t-sql/functions/newsequentialid-transact-sql.md) 函式。    
-   從 *xxxxxxxx*-*xxxx*-*xxxx*-*xxxx*-*xxxxxxxxxxxx* 格式的字串常數轉換，其中每一個 *x* 是範圍 0-9 或 a-f 的十六進位數字。 例如，6F9619FF-8B86-D011-B42D-00C04FC964FF 是有效的 **uniqueidentifier** 值。  
  
比較運算子可以搭配使用 **uniqueidentifier** 值。 不過排序並不是比較兩值的位元模式加以實作的。 您可以針對 **uniqueidentifier** 值執行的唯一作業是比較 (=、<>、\<, >、\<=, >=) 和檢查其是否為 NULL (IS NULL 和 IS NOT NULL)。 其他算術運算子一律不能使用。 除了 IDENTITY 之外，所有的資料行條件約束和屬性，都可以用於 **uniqueidentifier** 資料類型。
  
具有更新訂閱的合併式複寫和異動複寫，都使用 **uniqueidentifier** 資料行，以確保資料列可以在多份資料表唯一識別。
  
## <a name="converting-uniqueidentifier-data"></a>轉換 Uniqueidentifier 資料  
**uniqueidentifier** 類型會基於轉換字元運算式的用途，而被視為字元類型；因此會受到轉換成字元類型之截斷規則的影響。 亦即，將字元運算式轉換成不同大小的字元資料類型時，對新資料類型而言太大的值會被截斷。 請參閱＜範例＞一節。
  
## <a name="limitations-and-restrictions"></a>限制事項

這些工具和功能不支援 `uniqueidentifier` 資料類型：
- PolyBase
- 適用於平行處理資料倉儲的 [dwloader 載入工具](https://msdn.microsoft.com/sql/analytics-platform-system/dwloader)

## <a name="examples"></a>範例  
下列範例會將 `uniqueidentifier` 值轉換成 `char` 資料類型。
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
下列範例會示範當值對於要轉換的目標資料類型而言太大時，資料的截斷方式。 因為 **uniqueidentifier** 類型限制為 36 個字元，所以超過該長度的字元會被截斷。
  
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
[NEWID &#40;Transact-SQL&#41;](../../t-sql/functions/newid-transact-sql.md)  
[NEWSEQUENTIALID &#40;Transact-SQL&#41;](../../t-sql/functions/newsequentialid-transact-sql.md)    
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)
  
  
