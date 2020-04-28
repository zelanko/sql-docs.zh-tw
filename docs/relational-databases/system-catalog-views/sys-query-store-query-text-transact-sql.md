---
title: sys.databases query_store_query_text （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_QUERY_TEXT
- QUERY_STORE_QUERY_TEXT
- SYS.QUERY_STORE_QUERY_TEXT_TSQL
- QUERY_STORE_QUERY_TEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_store_query_text catalog view
- query_store_query_text catalog view
ms.assetid: f7032fa0-7c16-4492-bb82-685806c63a8c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b90f6641724ed526a9f7b496b792bb6cf786105f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "70000800"
---
# <a name="sysquery_store_query_text-transact-sql"></a>sys.databases query_store_query_text （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  包含查詢[!INCLUDE[tsql](../../includes/tsql-md.md)]的文字和 SQL 控制碼。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**query_text_id**|**bigint**|主索引鍵。|  
|**query_sql_text**|**nvarchar(max)**|查詢的 SQL 文字，由使用者提供。 包含空格、提示和批註。 查詢文字前後的註解和空格會被忽略。 不會忽略文字內的註解和空格。|  
|**statement_sql_handle**|**vabinary （64）**|個別查詢的 SQL 控制碼。|  
|**is_part_of_encrypted_module**|**bit**|查詢文字是加密模組的一部分。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**has_restricted_text**|**bit**|查詢文字包含密碼或其他 unmentionable 字組。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
  
## <a name="permissions"></a>權限  
 需要**VIEW DATABASE STATE**許可權。  
  
## <a name="see-also"></a>另請參閱  
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [query_coNtext_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [使用查詢存放區監視效能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [&#40;Transact-sql&#41;的目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢存放區預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
