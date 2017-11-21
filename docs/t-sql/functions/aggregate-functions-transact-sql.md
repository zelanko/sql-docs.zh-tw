---
title: "彙總函式 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5a97d68c641d2a3deb1d3fd3a674f65cafc3854c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="aggregate-functions-transact-sql"></a>彙總函式 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

彙總函式會根據一組值來執行計算，再傳回單一值。 除了 COUNT，彙總函式會忽略 Null 值。 彙總函式經常用來搭配 SELECT 陳述式的 GROUP BY 子句使用。
  
所有彙總函式都具有決定性。 這表示每當彙總函式是使用一組特定輸入值來進行呼叫時，它們都會傳回相同的值。 如需函數決定論的詳細資訊，請參閱[決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。 [OVER 子句](../../t-sql/queries/select-over-clause-transact-sql.md)可能會遵照 GROUPING 和 GROUPING_ID 除外的所有彙總函式。
  
只有下列情況才能利用彙總函式來作為運算式：
-   SELECT 陳述式的選取清單 (子查詢或外部查詢)。  
-   HAVING 子句。  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 提供下列彙總函式：
  
|||  
|-|-|  
|[AVG](../../t-sql/functions/avg-transact-sql.md)|[最小值](../../t-sql/functions/min-transact-sql.md)|  
|[CHECKSUM_AGG](../../t-sql/functions/checksum-agg-transact-sql.md)|[總和](../../t-sql/functions/sum-transact-sql.md)|  
|[計數](../../t-sql/functions/count-transact-sql.md)|[STDEV 函數](../../t-sql/functions/stdev-transact-sql.md)|  
|[COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)|[STDEVP](../../t-sql/functions/stdevp-transact-sql.md)|  
|[群組](../../t-sql/functions/grouping-transact-sql.md)|[VAR](../../t-sql/functions/var-transact-sql.md)|  
|[GROUPING_ID](../../t-sql/functions/grouping-id-transact-sql.md)|[VARP](../../t-sql/functions/varp-transact-sql.md)|  
|[最大值](../../t-sql/functions/max-transact-sql.md)||  
  
## <a name="see-also"></a>另請參閱
[內建函數 &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

