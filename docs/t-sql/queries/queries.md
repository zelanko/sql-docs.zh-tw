---
title: "查詢 |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 5ff02a32-e8d3-479c-ae8b-07581e41f5f8
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 8d7e4bf6357fe56f3c9b6a1e67e9e6aeb3675930
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="queries"></a>查詢
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  資料操作語言 (DML) 是一種詞彙，用來擷取和使用中的資料[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和 SQL Database。 最也用於 SQL 資料倉儲和 PDW （檢閱每個個別的陳述式，如需詳細資訊）。 請使用這些陳述式在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中加入、修改、查詢或移除資料。  
  
## <a name="in-this-section"></a>本節內容  
 下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所使用的 DML 陳述式。  
  
|||  
|-|-|  
|[BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)|[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|  
|[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)|  
|[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)|[UPDATETEXT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)|  
|[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)|[WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)|  
|[READTEXT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)||  
  
 下表列出用於多個 DML 陳述式或子句的子句。  
  
|子句|可用於這些陳述式|  
|------------|-------------------------------------|  
|[FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)|DELETE、SELECT、UPDATE|  
|[提示 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/hints-transact-sql.md)|DELETE、INSERT、SELECT、UPDATE|  
|[OPTION 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/option-clause-transact-sql.md)|DELETE、SELECT、UPDATE|  
|[OUTPUT 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)|DELETE、INSERT、MERGE、UPDATE|  
|[搜尋條件 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/search-condition-transact-sql.md)|DELETE、MERGE、SELECT、UPDATE|  
|[資料表值建構函式 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)|FROM、INSERT、MERGE|  
|[TOP &#40;TRANSACT-SQL &#41;](../../t-sql/queries/top-transact-sql.md)|DELETE、INSERT、MERGE、SELECT、UPDATE|  
|[其中 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/where-transact-sql.md)|DELETE、 SELECT、 UPDATE、 相符項目|  
|[與 common_table_expression &#40;TRANSACT-SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)|DELETE、INSERT、MERGE、SELECT、UPDATE|  
  
  
