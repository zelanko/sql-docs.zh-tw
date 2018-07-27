---
title: APPROX_COUNT_DISTINCT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- APPROX_COUNT_DISTINCT
dev_langs:
- TSQL
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9bb777a0a73f1a9ed950f860c00a5eae5171d7c0
ms.sourcegitcommit: 84cc5ed00833279da3adbde9cb6133a4e788ed3f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2018
ms.locfileid: "39216919"
---
# <a name="approxcountdistinct-transact-sql"></a>APPROX_COUNT_DISTINCT (Transact-SQL)
[!INCLUDE[appliesto-xx-asdb-asdw-pdw-md](../../includes/appliesto-xx-asdb-asdw-pdw-md.md)]

此函式會傳回群組中非 Null 的唯一值的近似數目。 
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

> [!NOTE]
> APPROX_COUNT_DISTINCT 是公開預覽功能。  
  
## <a name="syntax"></a>語法  
  
```sql
-- Syntax for Azure SQL Database, Azure SQL Data Warehouse and Parallel Data Warehouse  

APPROX_COUNT_DISTINCT ( expression )   
```  
  
## <a name="arguments"></a>引數  
*expression*  
任何類型的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)但除了 **image**、**sql_variant**、**ntext**或 **text**之外。 

## <a name="return-types"></a>傳回類型
 **bigint**  
  
## <a name="remarks"></a>Remarks  
`APPROX_COUNT_DISTINCT( expression )` 會針對群組中的每個資料列評估運算式，然後傳回群組中非 Null 的唯一值的近似數目。 設計此函式的目的是提供大型資料集之間的彙總，在此情況下回應性比絕對精確度更重要。  

`APPROX_COUNT_DISTINCT` 是針對用於大型資料的案例而設計，且已針對以下條件最佳化：
- 存取有數百萬資料行或更多 *and* 的資料集
- 資料行的彙總，或是有需多不同值的資料行的彙總

函式實作保證在 97% 機率內最多 2% 的錯誤率。 

`APPROX_COUNT_DISTINCT` 所需的記憶體比徹底的 COUNT DISTINCT 作業更少。  因為磁碟使用量較小，所以相較於精確的 COUNT DISTINCT 作業，`APPROX_COUNT_DISTINCT` 較不會將記憶體溢出到磁碟。 

> [!NOTE]
> 對於定序區分大小寫的字串，公開預覽版的 APPROX_COUNT_DISTINCT 是使用二進位比對，且提供的結果是採用 BIN 定序而不是 BIN2。 
  
## <a name="examples"></a>範例  
  
### <a name="a-using-approxcountdistinct"></a>A. 使用 APPROX_COUNT_DISTINCT 
此範例會從 orders 資料表傳回不同順序索引鍵的近似數目。
  
```sql
SELECT APPROX_COUNT_DISTINCT(O_OrderKey) AS Approx_Distinct_OrderKey
FROM dbo.Orders;
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Approx_Distinct_OrderKey
------------------------
15164704
```
  
### <a name="b-using-approxcountdistinct-with-group-by"></a>B. 搭配使用 APPROX_COUNT_DISTINCT 和 GROUP BY 
此範例會從 orders 資料表根據順序狀態傳回不同順序索引鍵的近似數目。 
  
```sql
SELECT O_OrderStatus, APPROX_COUNT_DISTINCT(O_OrderKey) AS Approx_Distinct_OrderKey
FROM dbo.Orders
GROUP BY O_OrderStatus
ORDER BY O_OrderStatus; 
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
O_OrderStatus                                                    Approx_Distinct_OrderKey
---------------------------------------------------------------- ------------------------
F                                                                7397838
O                                                                7387803
P                                                                388036
```
    
## <a name="see-also"></a>另請參閱
[彙總函式 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md) 
