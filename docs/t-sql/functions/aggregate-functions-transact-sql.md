---
title: 彙總函式 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], aggregate
- aggregate functions [SQL Server], about aggregate functions
- summarizing functions
- aggregate functions [SQL Server]
ms.assetid: 0c06ae42-eb0a-4d77-9d74-aa1e7f344009
caps.latest.revision: 30
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb2c15fa21847f8306d54213208e99e5da87f25a
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43082120"
---
# <a name="aggregate-functions-transact-sql"></a>彙總函式 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

彙總函式會根據一組值來執行計算，並傳回單一值。 除了 `COUNT` 之外，彙總函式會忽略 Null 值。 彙總函式經常用來搭配 SELECT 陳述式的 GROUP BY 子句使用。
  
所有彙總函式都具有決定性。 換句話說，使用一組特定輸入值呼叫時，彙總函式會在每次呼叫時傳回相同的值。 如需函式確定性的詳細資訊，請參閱[決定性和非決定性函式](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。 [OVER 子句](../../t-sql/queries/select-over-clause-transact-sql.md)可能會遵循所有彙總函式，但 GROUPING 和 GROUPING_ID 函式除外。
  
只有在下列情況下，才能使用彙總函式作為運算式：
-   SELECT 陳述式的選取清單 (子查詢或外部查詢)。  
-   HAVING 子句。  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 提供下列彙總函式：
  
|||
|-|-|
|[APPROX_COUNT_DISTINCT](../../t-sql/functions/approx-count-distinct-transact-sql.md)| [MIN](../../t-sql/functions/min-transact-sql.md)|
|[AVG](../../t-sql/functions/avg-transact-sql.md)|[STDEV](../../t-sql/functions/stdev-transact-sql.md)|
|[CHECKSUM_AGG](../../t-sql/functions/checksum-agg-transact-sql.md)|[STDEVP](../../t-sql/functions/stdevp-transact-sql.md)|
|[COUNT](../../t-sql/functions/count-transact-sql.md)|[STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md)|
|[COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)|[SUM](../../t-sql/functions/sum-transact-sql.md)|
|[GROUPING](../../t-sql/functions/grouping-transact-sql.md)|[VAR](../../t-sql/functions/var-transact-sql.md)|
|[GROUPING_ID](../../t-sql/functions/grouping-id-transact-sql.md)|[VARP](../../t-sql/functions/varp-transact-sql.md)|
|[MAX](../../t-sql/functions/max-transact-sql.md)||
  
## <a name="see-also"></a>另請參閱
[內建函數 &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[OVER 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
