---
title: "CHECKSUM_AGG (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKSUM_AGG
- CHECKSUM_AGG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- checksum values
- CHECKSUM_AGG function
- groups [SQL Server], checksum values
ms.assetid: cdede70c-4eb5-4c92-98ab-b07787ab7222
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b202009c2920dfbcdd068ec3d7ab95de13caa7b4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="checksumagg-transact-sql"></a>CHECKSUM_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回群組中各個值的總和檢查碼。 會忽略 Null 值。 後面可以接著[OVER 子句](../../t-sql/queries/select-over-clause-transact-sql.md)。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CHECKSUM_AGG ( [ ALL | DISTINCT ] expression )  
```  
  
## <a name="arguments"></a>引數  
**ALL**  
將彙總函式套用至所有值。 ALL 是預設值。
  
DISTINCT  
指定 CHECKSUM_AGG 傳回唯一值的總和檢查碼。
  
*expression*  
是一個整數[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 不允許彙總函式和子查詢。
  
## <a name="return-types"></a>傳回型別
傳回所有的總和檢查碼*運算式*值做為**int**。
  
## <a name="remarks"></a>備註  
CHECKSUM_AGG 可用來偵測資料表中的變更。
  
資料表中的資料列順序不會影響 CHECKSUM_AGG 的結果。 另外，CHECKSUM_AGG 函數也可以搭配 DISTINCT 關鍵字和 GROUP BY 子句來使用。
  
如果變更了運算式清單中的其中一個值，清單的總和檢查碼通常也會改變。 不過，總和檢查碼也有可能不會變更。
  
CHECKSUM_AGG 的功能相似於其他彙總函式。 如需詳細資訊，請參閱[彙總函式 & #40;TRANSACT-SQL & #41;](../../t-sql/functions/aggregate-functions-transact-sql.md).
  
## <a name="examples"></a>範例  
下列範例會利用 `CHECKSUM_AGG` 來偵測 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中 `Quantity` 資料表之 `ProductInventory` 資料行的變更。
  
```sql
--Get the checksum value before the column value is changed.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
262  
```  
  
```sql
UPDATE Production.ProductInventory   
SET Quantity=125  
WHERE Quantity=100;  
GO  
--Get the checksum of the modified column.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
287  
```  
  
## <a name="see-also"></a>另請參閱
[總和檢查碼 & #40;TRANSACT-SQL & #41;](../../t-sql/functions/checksum-transact-sql.md)  
[OVER 子句 & #40;TRANSACT-SQL & #41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

