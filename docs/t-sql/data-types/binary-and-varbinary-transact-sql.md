---
title: binary 和 varbinary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 8/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- binary_TSQL
- varbinary_TSQL
- binary
- varbinary
dev_langs:
- TSQL
helpviewer_keywords:
- varbinary data type
- binary [SQL Server], about binary data type
ms.assetid: bcce65f9-10db-4b3e-bfaf-dfc06c6f820f
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 624a2b764d6c397b950796fe822764b7983664ae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33051525"
---
# <a name="binary-and-varbinary-transact-sql"></a>binary 和 varbinary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

固定長度或可變長度的二進位資料類型。
  
## <a name="arguments"></a>引數  
**binary** [ ( *n* ) ] 固定長度的二進位資料，其長度為 *n* 位元組，其中 *n* 是 1 到 8,000 的值。 儲存體大小是 *n* 位元組。
  
**varbinary** [ ( *n* | **max**) ] 可變長度的二進位資料。 *n* 可以是從 1 到 8,000 之間的值。 **max** 表示儲存體大小上限是 2^31-1 個位元組。 儲存體大小是輸入資料的實際長度再加上 2 位元組。 輸入的資料有可能是 0 位元組。 **varbinary** 的 ANSI SQL 同義字是 **binary varying**。
  
## <a name="remarks"></a>Remarks  
當資料定義或變數宣告陳述式中沒有指定 *n* 時，預設長度為 1。 當 *n* 不是由 CAST 函式指定時，預設長度為 30。

| 資料類型 | 使用時機... |
| --- | --- |
| **binary** | 當資料行資料項目的大小一致時。|
| **varbinary** | 當資料行資料項目的大小變化相當大時。|
| **varbinary(max)** | 當資料行資料項目超過 8,000 位元組時。|


## <a name="converting-binary-and-varbinary-data"></a>轉換 binary 與 varbinary 資料
當資料是從字串資料類型 (**char**、**varchar**、**nchar**、**nvarchar**、**binary**、**varbinary**、**text**、**ntext** 或 **image**) 轉換成長度不同的 **binary** 或 **varbinary** 資料類型時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會填補或截斷位於右側的資料。 將其他資料類型轉換成 **binary** 或 **varbinary** 時，則在左側填補或截斷資料。 使用十六進位零進行填補。
  
若 **binary** 資料是搬移資料最簡易的方式，則將資料轉換成 **binary** 和 **varbinary** 資料類型會非常有幫助。 將各種資料類型的值轉換為有足夠大小的二進位值，然後將值轉換回原來的資料類型時，若兩個轉換都在相同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上進行，那麼將會得到相同的值。 數值的二進位表示法可能會隨著不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本而變更。
  
您可以將 **int**、**smallint** 和 **tinyint** 轉換成 **binary** 或 **varbinary**，但如果您將 **binary** 值轉換回整數值，若有發生截斷，則此值會與原始的整數值不同。 例如，下列 SELECT 陳述式所顯示的整數值 `123456`，通常會儲存為二進位的 `0x0001e240`：
  
```sql
SELECT CAST( 123456 AS BINARY(4) );  
```  
  
但是，下列 `SELECT` 陳述式顯示如果 **binary** 目標太小，放不下整個值，就會自動將前面的位數截斷，所以同一個數字會儲存為 `0xe240`：
  
```sql
SELECT CAST( 123456 AS BINARY(2) );  
```  
  
下列批次顯示悄悄截斷可能在不產生錯誤的情況下影響算術運算：
  
```sql
DECLARE @BinaryVariable2 BINARY(2);  
  
SET @BinaryVariable2 = 123456;  
SET @BinaryVariable2 = @BinaryVariable2 + 1;  
  
SELECT CAST( @BinaryVariable2 AS INT);  
GO  
```  
  
最後的結果是 `57921`，不是 `123457`。
  
> [!NOTE]  
>  於不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中在任何資料類型與 **binary** 資料類型之間轉換，不保證結果都會一樣。  
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[資料類型轉換 &#40;資料庫引擎&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
