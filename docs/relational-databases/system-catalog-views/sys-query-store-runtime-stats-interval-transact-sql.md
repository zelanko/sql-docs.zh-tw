---
title: sys.query_store_runtime_stats_interval (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_RUNTIME_STATS_INTERVAL
- SYS.QUERY_STORE_RUNTIME_STATS_INTERVAL
- QUERY_STORE_RUNTIME_STATS_INTERVAL_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS_INTERVAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_store_runtime_stats_interval catalog view
- query_store_runtime_stats_interval catalog view
ms.assetid: 2be83785-0569-41a3-88c8-59bfa0932e6e
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c9c494ab580d94f82587041c5c28ec60e2481e98
ms.sourcegitcommit: 3d50caa30681bf384f5628b1dd3e06e24fc910cd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2019
ms.locfileid: "54838025"
---
# <a name="sysquerystoreruntimestatsinterval-transact-sql"></a>sys.query_store_runtime_stats_interval (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  包含查詢的執行統計資料資訊已收集的執行階段透過每個間隔的開始和結束時間的資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**runtime_stats_interval_id**|**bigint**|主索引鍵。|
|**start_time**|**datetimeoffset**|間隔的開始時間。|
|**end_time**|**datetimeoffset**|間隔的結束時間。|
|**comment**|**nvarchar(32)**|一律是 NULL。|
  
## <a name="permissions"></a>Permissions  
 需要**VIEW DATABASE STATE**權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.database_query_store_options &#40;-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢存放區預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
