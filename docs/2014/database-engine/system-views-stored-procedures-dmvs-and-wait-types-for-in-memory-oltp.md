---
title: 記憶體內部 OLTP 的系統檢視、預存程式、Dmv 和等候類型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: efaa59e3-dbfa-407f-b1aa-cb0c6602ea17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d047cbc4fe3ba3f4945acd9da4f627a05992e779
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62842397"
---
# <a name="system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp"></a>記憶體內部 OLTP 的系統檢視表、預存程序、DMV 和等候類型
  本主題提供支援 In-Memory OLTP 的許多資料庫物件的簡短說明及連結。  
  
### <a name="system-views"></a>系統檢視表  
  
|系統檢視表|描述|In-Memory OLTP 功能|  
|-----------------|-----------------|-----------------------------|  
|[sys.data_spaces &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-data-spaces-transact-sql)|檢查檔案群組是否包含記憶體最佳化資料。|下列資料行會顯示其他值： **type**和**type_desc**。|  
|[sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)|檢查索引是否位在記憶體最佳化的資料表上。|下列資料行會顯示其他值： **type**和**type_desc**。|  
|[sys.parameters &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameters-transact-sql)|檢查參數是否不可為 Null (以讓原生編譯預存程序更有效率的執行)。|**is_nullable**資料行。|  
|[all_sql_modules &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql)|檢查預存程序是否為原生編譯。|**uses_native_compilation**資料行。|  
|[sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)|檢查預存程序是否為原生編譯。|**uses_native_compilation**資料行。|  
|[table_types &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-table-types-transact-sql)|檢查資料表是否已針對記憶體最佳化。|**is_memory_optimized**資料行。|  
|[sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|檢查資料表是否為記憶體優化，並檢查資料表的耐久性設定。|**持久性**、 **durability_desc**和**is_memory_optimized**資料行。|  
|[sys.hash_indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-hash-indexes-transact-sql)|顯示記憶體最佳化資料表的雜湊索引。|In-Memory OLTP 特定。|  
  
### <a name="metadata-functions"></a>中繼資料函數  
  
|中繼資料函數|描述|In-Memory OLTP 功能|  
|-----------------------|-----------------|-----------------------------|  
|[OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)|檢查資料庫物件是否已針對記憶體最佳化。|**ExecIsWithNativeCompilation**和**TableIsMemoryOptimized**屬性。<br /><br /> **IsSchemaBound**屬性支援程式物件類型（針對程式傳回0，而不是 Null）。|  
|[SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)|檢查伺服器是否支援 In-Memory OLTP。|**IsXTPSupported**屬性。|  
  
### <a name="system-stored-procedures"></a>系統預存程序  
  
|預存程序|描述|  
|----------------------|-----------------|  
|[sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)|將 In-Memory OLTP 資料庫繫結至資源集區。|  
|[sp_xtp_checkpoint_force_garbage_collection &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-checkpoint-force-garbage-collection-transact-sql)|起始 In-Memory OLTP 資料庫上的記憶體回收。|  
|[sp_xtp_control_proc_exec_stats &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql)|啟用原生編譯預存程序的統計資料收集。|  
|[sp_xtp_control_query_exec_stats &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql)|啟用原生編譯預存程序的每一查詢統計資料收集。|  
|[sp_xtp_merge_checkpoint_files &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql)|合併資料和差異檔案。|  
|[sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)|移除資料庫與資源集區之間的繫結。|  
  
## <a name="dynamic-management-views-dmvs"></a>動態管理檢視 (DMV)  
 記憶體最佳化資料表有數個 DMV。  
  
 如需詳細資訊，請參閱[&#40;transact-sql&#41;的記憶體優化資料表動態管理 Views ](/sql/relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql)。  
  
## <a name="wait-types"></a>等候類型  
 有數個支援 In-Memory OLTP 的等候類型。  
  
 如需詳細資訊，請參閱前面加上**WAIT_XTP**的等候類型，以及[dm_os_wait_stats &#40;transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql)主題中的**XTPPROC** 。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部優化&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)   
 [記憶體中 OLTP 的 Transact-SQL 支援](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
