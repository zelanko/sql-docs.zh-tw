---
title: "分析函數 (TRANSACT-SQL) |Microsoft 文件"
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
ms.assetid: 60fbff84-673b-48ea-9254-6ecdad20e7fe
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 61b8816c3784f4088c32a54fbefbac7960764f38
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="analytic-functions-transact-sql"></a>分析函數 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

SQL Server 支援下列分析函數。 分析函數會根據資料列群組計算出彙總值。 但不同於彙總函式，其可以傳回每個群組的多個資料列。 您可以使用分析函數計算群組中的移動平均、最新總數、百分比或前 N 個結果。
  
|||  
|-|-|  
|[CUME_DIST &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cume-dist-transact-sql.md)|[負責人 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/lead-transact-sql.md)|  
|[FIRST_VALUE &#40;TRANSACT-SQL &#41;](../../t-sql/functions/first-value-transact-sql.md)|[PERCENTILE_CONT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/percentile-cont-transact-sql.md)|  
|[LAG &#40;TRANSACT-SQL &#41;](../../t-sql/functions/lag-transact-sql.md)|[PERCENTILE_DISC &#40;TRANSACT-SQL &#41;](../../t-sql/functions/percentile-disc-transact-sql.md)|  
|[LAST_VALUE &#40;TRANSACT-SQL &#41;](../../t-sql/functions/last-value-transact-sql.md)|[PERCENT_RANK &#40;TRANSACT-SQL &#41;](../../t-sql/functions/percent-rank-transact-sql.md)|  
  
## <a name="see-also"></a>另請參閱
[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
