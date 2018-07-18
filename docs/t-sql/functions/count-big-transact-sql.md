---
title: COUNT_BIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COUNT_BIG_TSQL
- COUNT_BIG
dev_langs:
- TSQL
helpviewer_keywords:
- totals [SQL Server], COUNT_BIG function
- counting items in group
- groups [SQL Server], number of items in
- number of group items
- COUNT_BIG function
ms.assetid: f2e3601f-487e-4917-bb01-47b1047908cd
caps.latest.revision: 44
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 550dc639c3b949926c1bd95b7c89e04823b68f68
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37781249"
---
# <a name="countbig--sql"></a>COUNT_BIG (-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

此函數會傳回群組中找到的項目數。 `COUNT_BIG` 的運作方式類似 [COUNT](../../t-sql/functions/count-transact-sql.md) 函數。 這些函數唯一的差別就是其傳回值的資料類型。 `COUNT_BIG` 一律會傳回 **bigint** 資料類型值。 `COUNT` 一律會傳回 **int** 資料類型值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
-- Syntax for SQL Server and Azure SQL Database  
  
COUNT_BIG ( { [ ALL | DISTINCT ] expression } | * )  
   [ OVER ( [ partition_by_clause ] [ order_by_clause ] ) ]  
```  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Aggregation Function Syntax  
COUNT_BIG ( { [ [ ALL | DISTINCT ] expression ] | * } )  
  
-- Analytic Function Syntax  
COUNT_BIG ( { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>引數  
ALL  
將彙總函式套用至所有值。 全部都可以當作預設值。
  
DISTINCT  
指定 `COUNT_BIG` 傳回唯一非 Null 值的數目。
  
*expression*  
任意類型的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 請注意，`COUNT_BIG` 不支援運算式中的彙總函數或子查詢。
  
*\**  
指定 `COUNT_BIG` 應該計算所有資料列，以判斷要傳回的總資料表資料列計數。 `COUNT_BIG(*)` 不接受任何參數，而且不支援使用 DISTINCT。 `COUNT_BIG(*)` 不需要 *expression* 參數，因為依照定義，它不會使用任何特定資料行的相關資訊。 `COUNT_BIG(*)` 會傳回指定資料表的資料列數，而且它會保留重複的資料列。 它會個別計算每個資料列。 其中包括含有 Null 值的資料列。
  
OVER **(** [ *partition_by_clause* ] [ *order_by_clause* ] **)**  
*partition_by_clause* 會將 `FROM` 子句產生的結果集，分割成 `COUNT_BIG` 函數所要套用的資料分割。 如未指定，此函數會將查詢結果集的所有資料列視為單一群組。 *order_by_clause* 會決定作業的邏輯順序。 如需詳細資訊，請參閱 [OVER 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)。
  
## <a name="return-types"></a>傳回類型
**bigint**
  
## <a name="remarks"></a>Remarks  
COUNT_BIG(\*) 會傳回群組中的項目數。 其中包括 NULL 值和複本。
  
COUNT_BIG (ALL *expression*) 會針對群組中的每個資料列來評估 *expression*，且會傳回非 Null 值的數目。
  
COUNT_BIG (DISTINCT *expression*) 會針對群組中的每個資料列來評估 *expression*，且會傳回唯一且非 Null 值的數目。
  
COUNT_BIG ***不搭配*** OVER 和 ORDER BY 子句使用時，是具決定性函數。 ***搭配*** OVER 和 ORDER BY 子句時，則不具決定性。 如需詳細資訊，請參閱[決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。
  
## <a name="examples"></a>範例  
如需範例，請參閱 [COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md)。
  
## <a name="see-also"></a>另請參閱
[彙總函式 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md)  
[int、bigint、smallint 和 tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
[OVER 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
