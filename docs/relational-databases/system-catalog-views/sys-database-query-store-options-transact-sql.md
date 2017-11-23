---
title: "sys.database_query_store_options (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASE_QUERY_STORE_OPTIONS_TSQL
- DATABASE_QUERY_STORE_OPTIONS
- SYS.DATABASE_QUERY_STORE_OPTIONS_TSQL
- SYS.DATABASE_QUERY_STORE_OPTIONS
dev_langs: TSQL
helpviewer_keywords:
- database_query_store_options catalog view
- sys.database_query_store_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6a48af2e0a4bef456091385b047685c074097200
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatabasequerystoreoptions-transact-sql"></a>sys.database_query_store_options (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  傳回此資料庫的查詢存放區選項。  
  
**適用於**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**desired_state**|**smallint**|表示查詢存放區，由使用者明確地設定所需的操作模式。<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**nvarchar （64)**|文字的查詢存放區所需的作業模式的詳細描述：<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**於 actual_state**|**smallint**|表示查詢存放區的作業模式。 除了所需的狀態所需的使用者清單中，實際狀態可能是錯誤狀態。<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = 錯誤|  
|**actual_state_desc**|**nvarchar （64)**|查詢存放區的實際作業模式的文字描述。<br />OFF<br />READ_ONLY<br />READ_WRITE<br />ERROR<br /><br /> 有很多情況下，當實際狀態所需的狀態：<br /><br /> 查詢存放區可能會在唯讀模式運作，即使使用者已指定讀寫。 例如，可能會發生如果資料庫處於唯讀模式或查詢存放區大小超過配額。<br /><br /> 極少，查詢存放區最後會處於錯誤狀態因為發生內部錯誤。 如果發生這種情況，無法執行復原查詢存放區**sp_query_store_consistency_check**預存程序內受影響的資料庫。|  
|**readonly_reason**|**int**|當**desired_state_desc**是 READ_WRITE 和**actual_state_desc**是 READ_ONLY， **readonly_reason**傳回一個位元對應指出為什麼查詢存放區中readonly 模式。<br /><br /> 1 – 資料庫處於唯讀模式<br /><br /> 2 – 資料庫處於單一使用者模式<br /><br /> 4 – 資料庫處於緊急模式<br /><br /> 8-資料庫是次要複本 (適用於 Alwayson 和 Azure[!INCLUDE[ssSDS](../../includes/sssds-md.md)]地理複寫)。 這個值可以有效地只上觀察**可讀取**次要複本<br /><br /> 65536 – 查詢存放區已達到到達了 MAX_STORAGE_SIZE_MB 選項所設定的大小限制。<br /><br /> 131072 查詢存放區中不同的陳述式的-數目已達到內部記憶體限制。 建議您移除您不需要的查詢，或升級至較高的服務層，以啟用查詢存放區轉換為讀寫模式。<br />只適用於 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。<br /><br /> 262144 – 等候保存在磁碟上的記憶體中項目的大小已達到內部記憶體限制。 暫時在記憶體中的項目會保存在磁碟上之前，查詢存放區將處於唯讀模式。 <br />只適用於 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。<br /><br />524288 – 資料庫已達到磁碟大小限制。 查詢存放區是資料庫的一部分使用者，因此如果沒有更多可用空間的資料庫，表示查詢存放區無法進一步成長不再。<br />只適用於 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。 <br /> <br /> 若要切換的查詢存放區作業模式下一步 以讀寫，請參閱**確認查詢存放區會持續收集查詢資料**區段[使用查詢存放區的最佳作法](../../relational-databases/performance/best-practice-with-the-query-store.md)。|  
|**current_storage_size_mb**|**bigint**|查詢存放區的大小以 mb 為單位的磁碟上。|  
|**flush_interval_seconds**|**bigint**|定義期間定期排清查詢存放區資料的磁碟。 預設值為 900 （15 分鐘）。<br /><br /> 藉由變更`ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)`陳述式。|  
|**interval_length_minutes**|**bigint**|統計資料彙總間隔。 不允許任意值。 使用下列其中之一： 1、 5、 10、 15、 30、 60 和 1440年分鐘。 預設值是 60 分鐘的時間。|  
|**到達了 max_storage_size_mb**|**bigint**|查詢存放區的最大磁碟大小。 預設值為 100 MB。<br />針對 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium 版本預設值為 1Gb，而針對 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic 版本預設值為 10Mb。<br /><br /> 藉由變更`ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)`陳述式。|  
|**stale_query_threshold_days**|**bigint**|查詢的任何原則設定會保留查詢存放區中的日數。 預設值為 30。 若要停用保留原則設為 0。<br />[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic 版的預設值為 7 天。<br /><br /> 藉由變更`ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )`陳述式。|  
|**max_plans_per_query**|**bigint**|限制預存的計劃的最大數目。 預設值為 200。 如果達到最大值時，查詢存放區會停止擷取新的計畫，該查詢。 設定為 0 會移除與擷取的計劃的數目限制。<br /><br /> 藉由變更`ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)`陳述式。|  
|**query_capture_mode**|**smallint**|目前作用中查詢擷取模式：<br /><br /> 1 = ALL-擷取所有查詢。 這是預設組態值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])。<br /><br /> 2 = AUTO-擷取相關的查詢，根據執行計數和資源耗用。 這是預設組態值[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。<br /><br /> 3 = 無-停止擷取新的查詢。 查詢存放區將會繼續收集已擷取的查詢編譯和執行階段統計資料。 請小心使用此設定，因為您可能會遺失擷取重要的查詢。|  
|**query_capture_mode_desc**|**nvarchar （60)**|查詢存放區的實際擷取模式的文字描述：<br /><br /> 全部 (預設為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])<br /><br /> 自動 (預設為[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)])<br /><br /> 無|  
|**size_based_cleanup_mode**|**smallint**|控制是否清除要自動啟用當總資料量接近大小上限：<br /><br /> 1 = OFF – 大小基礎的清除並不會自動啟動。<br /><br /> 2 = AUTO-大小大小上的磁碟到達 90%時自動啟動根據的清除**到達了 max_storage_size_mb**。 這是預設組態值。<br /><br />大小基礎清除先移除最高和最舊的查詢。 會在大約 80%的到達了 max_storage_size_mb 停止。|  
|**size_based_cleanup_mode_desc**|**smallint**|查詢存放區的實際大小為基礎的清除模式的文字描述：<br /><br /> OFF <br /><br /> 自動 （預設值）|  
|**wait_stats_capture_mode**|**smallint**|可控制查詢存放區是否執行擷取的等待統計資料： <br /><br /> 0 = OFF <br /><br /> 1 = ON |
|**wait_stats_mode_capture_desc**|**nvarchar （60)**|實際的等待統計資料的擷取模式的文字描述： <br /><br /> OFF <br /><br /> （預設值）| 
  
## <a name="permissions"></a>Permissions  
 需要**VIEW DATABASE STATE**權限。  
  
## <a name="see-also"></a>請參閱＜  
 [sys.query_context_settings &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [使用查詢存放區監視效能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)   
 [查詢存放區預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
