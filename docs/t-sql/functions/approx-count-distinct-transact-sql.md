---
title: APPROX_COUNT_DISTINCT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- APPROX_COUNT_DISTINCT
dev_langs:
- TSQL
author: joesackmsft
ms.author: josack
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 08beac97cd70045f073be53cfeb93e9d1e4ad67f
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87113154"
---
# <a name="approx_count_distinct-transact-sql"></a>APPROX_COUNT_DISTINCT (Transact-SQL)

[!INCLUDE [sqlserver2019-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2019-asdb-asdbmi-asa.md)]

此函式會傳回群組中非 Null 的唯一值的近似數目。 
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
-- Syntax for Azure SQL Database, Azure SQL Data Warehouse and Parallel Data Warehouse  

APPROX_COUNT_DISTINCT ( expression )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
*expression*  
任何類型的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)但除了 **image**、**sql_variant**、**ntext**或 **text**之外。 

## <a name="return-types"></a>傳回類型
 **bigint**  
  
## <a name="remarks"></a>備註  
`APPROX_COUNT_DISTINCT( expression )` 會針對群組中的每個資料列評估運算式，然後傳回群組中非 Null 的唯一值的近似數目。 設計此函式的目的是提供大型資料集之間的彙總，在此情況下回應性比絕對精確度更重要。  

`APPROX_COUNT_DISTINCT` 是針對用於大型資料的案例而設計，且已針對以下條件最佳化：
- 存取有數百萬資料行或更多 *and* 的資料集
- 資料行的彙總，或是有需多不同值的資料行的彙總

函式實作保證在 97% 機率內最多 2% 的錯誤率。 

`APPROX_COUNT_DISTINCT` 所需的記憶體比徹底的 COUNT DISTINCT 作業更少。  因為磁碟使用量較小，所以相較於精確的 COUNT DISTINCT 作業，`APPROX_COUNT_DISTINCT` 較不會將記憶體溢出到磁碟。 若要深入了解用於達成此目的的演算法，請參閱 [HyperLogLog](https://en.wikipedia.org/wiki/HyperLogLog) \(英文\)。

> [!NOTE]
> 針對定序區分大小寫的字串，APPROX_COUNT_DISTINCT 是使用二進位比對，且提供的結果是採用 BIN 定序而不是 BIN2。 
  
## <a name="examples"></a>範例  
  
### <a name="a-using-approx_count_distinct"></a>A. 使用 APPROX_COUNT_DISTINCT 
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
  
### <a name="b-using-approx_count_distinct-with-group-by"></a>B. 搭配使用 APPROX_COUNT_DISTINCT 和 GROUP BY 
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
