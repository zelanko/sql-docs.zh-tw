---
title: sys.query_context_settings (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/22/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS
- QUERY_CONTEXT_SETTINGS
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_context_settings catalog view
ms.assetid: 3c1887df-6bd8-491e-82fc-d25ad9589faf
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9be8b645cf0a5f08132110dd1eca43c19726d75a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysquerycontextsettings-transact-sql"></a>sys.query_context_settings (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  包含與查詢相關聯的內容設定會影響語意的相關資訊。 許多內容設定中有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的影響 （定義正確結果的查詢） 的查詢語意。 在不同設定下所編譯的相同查詢文字可能會產生不同的結果 （取決於基礎資料中）。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**context_settings_id**|**bigint**|主索引鍵。 查詢，這個值會公開執行程序表 XML 中。|  
|**set_options**|**varbinary(8)**|反映的數個 SET 選項的狀態位元遮罩。 如需詳細資訊，請參閱[sys.dm_exec_plan_attributes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)。|  
|**language_id**|**smallint**|語言識別碼。 如需詳細資訊，請參閱[sys.syslanguages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)。|  
|**date_format**|**smallint**|日期的格式。 如需詳細資訊，請參閱 [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md)。|  
|**date_first**|**tinyint**|日期的第一個值。 如需詳細資訊，請參閱 [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md)。|  
|**status**|**varbinary(2)**|位元遮罩欄位指出類型的查詢或執行查詢的內容。 <br />資料行的值可以是多個旗標 （以十六進位表示） 的組合：<br /><br /> 0x0-一般查詢 （沒有特定的旗標）<br /><br /> 0x1-透過資料指標 Api 預存程序的其中一個已執行的查詢<br /><br /> 0x2-通知查詢<br /><br /> 0x4-內部的查詢<br /><br /> 0x8-沒有通用的參數化的自動參數化查詢<br /><br /> 0x10-資料指標提取的重新整理查詢<br /><br /> 0x20-資料指標更新要求中所使用的查詢<br /><br /> 0x40-初始會傳回結果集資料指標開啟時 （資料指標自動擷取）<br /><br /> 0x80 – 加密的查詢<br /><br /> 0x100 – 中的資料列層級安全性述詞的內容查詢|  
|**required_cursor_options**|**int**|使用者指定的資料指標選項，例如資料指標類型。|  
|**acceptable_cursor_options**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會隱含轉換的目標資料指標選項，以支援執行陳述式。|  
|**sys.dm_exec_plan_attributes**|**smallint**|觸發程序執行計劃做為結果型別**合併**陳述式。<br /><br /> 0 表示非觸發程序計畫，不會導致執行觸發程序計畫**合併**陳述式或導致執行觸發程序計畫**合併**陳述式只指定**刪除**動作。<br /><br /> 1 表示**插入**而導致執行觸發程序計畫**合併**陳述式。<br /><br /> 2 表示**更新**而導致執行觸發程序計畫**合併**陳述式。<br /><br /> 3 表示**刪除**而導致執行觸發程序計畫**合併**陳述式包含對應**插入**或**更新**動作。<br /><br /> <br /><br /> 巢狀觸發程序來串聯式動作執行，這個值會是動作的**合併**造成串聯的陳述式。|  
|**default_schema_id**|**int**|預設結構描述，用來解析不完整的名稱識別碼。|  
|**is_replication_specific**|**bit**|用於複寫。|  
|**is_contained**|**varbinary(1)**|1 表示自主的資料庫。|  
  
## <a name="permissions"></a>Permissions  
 需要**VIEW DATABASE STATE**權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.database_query_store_options &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢存放區預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
