---
title: "binary 和 varbinary (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 8/16/2017
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
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e6aaf00b8e846316c92897360932703a013150e8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="binary-and-varbinary-transact-sql"></a>binary 和 varbinary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

固定長度或可變長度的二進位資料類型。
  
## <a name="arguments"></a>引數  
**二進位**[(  *n*  )]，長度為固定長度二進位資料 *n* 位元組，其中 *n* 是值從 1 到 8,000。 儲存體大小是 *n* 位元組。
  
**varbinary** [(  *n*   |  **max**)] 可變長度二進位資料。 *n*可以是 1 到 8,000 的值。 **最大**表示最大儲存體大小是 2 ^31-1 位元組。 儲存體大小是輸入資料的實際長度再加上 2 位元組。 輸入的資料有可能是 0 位元組。 ANSI SQL 同義字**varbinary**是**二進位變動**。
  
## <a name="remarks"></a>備註  
當 *n* 中未指定資料定義或變數宣告陳述式中，預設長度為 1。 當 *n* 未利用 CAST 函數，則預設長度為 30。

| 資料類型 | 使用時機... |
| --- | --- |
| **binary** | 資料行資料項目的大小一致。|
| **varbinary** | 資料行資料項目的大小變化。|
| **varbinary(max)** | 資料行資料項目超過 8,000 個位元組。|


## <a name="converting-binary-and-varbinary-data"></a>轉換 binary 與 varbinary 資料
當從字串資料類型轉換資料 (**char**， **varchar**， **nchar**， **nvarchar**，**二進位**， **varbinary**，**文字**， **ntext**，或**映像**) 至**二進位**或**varbinary**不相等的長度資料型別[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會填補或截斷右邊的資料。 當將其他資料類型轉換成**二進位**或**varbinary**，填補或截斷左側的資料。 使用十六進位零進行填補。
  
將資料轉換為**二進位**和**varbinary**很有用的資料型別如果**二進位**資料是最簡單的方式來移動資料。 任何值的任何轉換輸入的大型二進位值足夠大小且然後回型別，一定會造成相同的值這兩種轉換會進行相同的版本上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 數值的二進位表示法可能會隨著不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本而變更。
  
您可以將轉換**int**， **smallint**，和**tinyint**至**二進位**或**varbinary**，但是如果您轉換**二進位**值存回整數值，這個值會從原始的整數值不同，若有發生截斷。 例如，下列 SELECT 陳述式所顯示的整數值 `123456`，通常會儲存為二進位的 `0x0001e240`：
  
```sql
SELECT CAST( 123456 AS BINARY(4) );  
```  
  
不過，下列`SELECT`陳述式顯示如果**二進位**目標是太小，無法容納整個值、 前置數字會以無訊息模式截斷，所以相同的號碼儲存為`0xe240`:
  
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
>  型別之間的任何資料轉換和**二進位**不保證相同版本之間的資料型別[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[資料類型轉換 &#40; Database Engine &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

