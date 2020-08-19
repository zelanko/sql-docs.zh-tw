---
description: 分析函數 (Transact-SQL)
title: 分析函式 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 60fbff84-673b-48ea-9254-6ecdad20e7fe
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2227508b89336fca543f12f60b76e22094cb78f7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422842"
---
# <a name="analytic-functions-transact-sql"></a>分析函數 (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

SQL Server 支援以下分析函式：

- [CUME_DIST &#40;Transact-SQL&#41;](../../t-sql/functions/cume-dist-transact-sql.md)
- [FIRST_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/first-value-transact-sql.md)
- [LAG &#40;Transact-SQL&#41;](../../t-sql/functions/lag-transact-sql.md)
- [LAST_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/last-value-transact-sql.md)
- [LEAD &#40;Transact-SQL&#41;](../../t-sql/functions/lead-transact-sql.md)
- [PERCENT_RANK &#40;Transact-SQL&#41;](../../t-sql/functions/percent-rank-transact-sql.md)
- [PERCENTILE_CONT &#40;Transact-SQL&#41;](../../t-sql/functions/percentile-cont-transact-sql.md)  
- [PERCENTILE_DISC&#40;Transact-SQL&#41;](../../t-sql/functions/percentile-disc-transact-sql.md)
  
分析函式會根據資料列的群組計算彙總值。 與彙總函式不同，分析函式可以針對各群組傳回多個資料列。 使用分析函式可計算群組內的移動平均值、執行總計、百分比或前 N 個結果。
 
## <a name="see-also"></a>另請參閱

[OVER 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
