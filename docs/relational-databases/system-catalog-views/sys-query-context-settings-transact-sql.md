---
title: sys.databases query_coNtext_settings （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7736c0001c8e22b6cc7c72b2e721e31519d035b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068059"
---
# <a name="sysquery_context_settings-transact-sql"></a>sys.databases query_coNtext_settings （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  包含影響與查詢相關聯之內容設定之語義的相關資訊。 有一些內容設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會影響查詢的語義（定義正確的查詢結果）。 在不同設定下編譯的相同查詢文字，可能會產生不同的結果（視基礎資料而定）。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**coNtext_settings_id**|**Bigint**|主索引鍵。 這個值會在查詢的顯示計畫 XML 中公開。|  
|**set_options**|**varbinary(8)**|用來反映數個 SET 選項之狀態的位元遮罩。 如需詳細資訊，請參閱[dm_exec_plan_attributes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)。|  
|**language_id**|**smallint**|語言的識別碼。 如需詳細資訊，請參閱[sys.syslanguages &#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)。|  
|**date_format**|**smallint**|日期格式。 如需詳細資訊，請參閱 [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md)。|  
|**date_first**|**tinyint**|日期第一個值。 如需詳細資訊，請參閱 [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md)。|  
|**狀態**|**Varbinary （2）**|位元遮罩欄位，表示執行查詢的查詢或內容類型。 <br />資料行值可以是多個旗標的組合（以十六進位表示）：<br /><br /> 0x0-一般查詢（無特定旗標）<br /><br /> 0x1-透過其中一個資料指標 Api 預存程式執行的查詢<br /><br /> 0x2-通知的查詢<br /><br /> 0x4-內部查詢<br /><br /> 0x8-不含通用參數化的自動參數化查詢<br /><br /> 0x10-資料指標提取重新整理查詢<br /><br /> 0x20-正用於資料指標更新要求中的查詢<br /><br /> 0x40-當資料指標開啟時，會傳回初始結果集（資料指標自動提取）<br /><br /> 0x80-加密查詢<br /><br /> 0x100-在資料列層級安全性述詞的內容中查詢|  
|**required_cursor_options**|**int**|使用者指定的資料指標選項，例如資料指標類型。|  
|**acceptable_cursor_options**|**int**|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會隱含轉換的目標資料指標選項，以支援執行陳述式。|  
|**merge_action_type**|**smallint**|當做**MERGE**語句結果使用之觸發程式執行計畫的類型。<br /><br /> 0表示非觸發程式計畫、不會當做**merge**語句結果執行的觸發程式計畫，或是當做**merge**語句結果執行的觸發程式計畫，只會指定**刪除**動作。<br /><br /> 1表示當做**MERGE**語句結果執行的**INSERT**觸發程式計畫。<br /><br /> 2表示當做**MERGE**語句結果執行的**更新**觸發程式計畫。<br /><br /> 3表示當做包含對應**插入**或**更新**動作的**MERGE**語句結果執行的**DELETE**觸發程式計畫。<br /><br /> <br /><br /> 針對由串聯式動作執行的嵌套觸發程式，此值是造成 cascade 之**MERGE**語句的動作。|  
|**default_schema_id**|**int**|預設架構的識別碼，用來解析不完整的名稱。|  
|**is_replication_specific**|**bit**|用於複寫。|  
|**is_contained**|**Varbinary （1）**|1表示自主資料庫。|  
  
## <a name="permissions"></a>權限  
 需要**VIEW DATABASE STATE**許可權。  
  
## <a name="see-also"></a>另請參閱  
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [query_store_wait_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)   
 [query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢存放區預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [fn_stmt_sql_handle_from_sql_stmt &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
