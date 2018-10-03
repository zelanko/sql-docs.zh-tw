---
title: 管理資料收集 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
keywords:
- 資料收集
helpviewer_keywords:
- data collection [SQL Server]
- data collector [SQL Server], Transact-SQL
- data collector [SQL Server], SQL Server Management Studio
ms.assetid: bc137daa-9f37-4c01-9766-8b7350c75af8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1c181dc687f2e00ff566ca37ca0de7583cab121e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721776"
---
# <a name="manage-data-collection"></a>管理資料收集
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序和函數來管理資料收集的不同層面，例如啟用或停用資料收集、變更收集組的組態，或是檢視管理資料倉儲中的資料。  
  
## <a name="manage-data-collection-using-ssms"></a>使用 SSMS 管理資料收集  
 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使用物件總管來執行與資料收集器相關的下列工作：  
  
-   [設定管理資料倉儲 &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
-   [設定資料收集器的屬性](../../relational-databases/data-collection/configure-properties-of-a-data-collector.md)  
  
-   [啟用或停用資料收集](../../relational-databases/data-collection/enable-or-disable-data-collection.md)  
  
-   [啟動或停止收集組](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
-   [使用 SQL Server Profiler 來建立 SQL 追蹤收集組 &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/use-sql-server-profiler-to-create-a-sql-trace-collection-set.md)  
  
-   [檢視收集組記錄 &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-collection-set-logs-sql-server-management-studio.md)  
  
-   [檢視或變更收集組排程 &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-or-change-collection-set-schedules-sql-server-management-studio.md)  
  
-   [檢視收集組報表 &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
## <a name="manage-data-collection-using-transact-sql"></a>使用 Transact-SQL 管理資料收集  
 資料收集器會提供預存程序的廣泛集合，您可使用這些預存程序來執行任何資料收集器相關的工作。 例如，您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]來執行下列工作：  
  
-   [設定資料收集參數 &#40;Transact-SQL&#41;](../../relational-databases/data-collection/configure-data-collection-parameters-transact-sql.md)  
  
-   [啟用或停用資料收集](../../relational-databases/data-collection/enable-or-disable-data-collection.md)  
  
-   [啟動或停止收集組](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
-   [建立使用一般 T-SQL 查詢收集器型別的自訂收集組 &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)  
  
-   [將收集項加入收集組 &#40;Transact-SQL&#41;](../../relational-databases/data-collection/add-a-collection-item-to-a-collection-set-transact-sql.md)  
  
 此外，您還可以使用一些函數和檢視來取得 msdb 和管理資料倉儲資料庫的組態資料、執行記錄資料，以及管理資料倉儲中所儲存的資料。  
  
 您可以使用預存程序、函數和檢視，而提供這些項目的目的是要建立您自己的端對端資料收集案例。  
  
>**重要！！** 不同於一般預存程序，資料收集器的預存程序會使用嚴格類型的參數，而且不支援資料類型的自動轉換。 如果沒有依照引數描述所指定，以正確的輸入參數資料類型來呼叫這些參數，預存程序會傳回錯誤。  
  
 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來建立及執行所提供的程式碼範例。 如需詳細資訊，請參閱 [物件總管](../../ssms/object/object-explorer.md)。 另一個替代方法是使用任何編輯器建立查詢，並將它儲存為 .sql 副檔名的文字檔。 您可以使用 **sqlcmd** 公用程式，從 Windows 命令提示字元執行查詢。 如需詳細資訊，請參閱 [使用 sqlcmd 公用程式](../../relational-databases/scripting/sqlcmd-use-the-utility.md)。  
  
### <a name="stored-procedures-and-views"></a>預存程序和檢視表  
 **使用資料收集器**  
  
 下表描述的是您可以用來處理資料收集器的預存程序。  
  
|程序名稱|Description|  
|--------------------|-----------------|  
|[sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)|啟用資料收集器。|  
|[sp_syscollector_disable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)|停用資料收集器。|  
  
 **使用收集組**  
  
 下表描述的是您可以用來處理收集組的預存程序。  
  
|程序名稱|Description|  
|--------------------|-----------------|  
|[sp_syscollector_run_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md)|視需要執行收集組。|  
|[sp_syscollector_start_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql.md)|啟動收集組。|  
|[sp_syscollector_stop_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md)|停止收集組。|  
|[sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)|建立收集組。|  
|[sp_syscollector_delete_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-set-transact-sql.md)|刪除收集組。|  
|[sp_syscollector_update_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-set-transact-sql.md)|變更收集組組態。|  
|[sp_syscollector_upload_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-upload-collection-set-transact-sql.md)|將收集組資料上傳到管理資料倉儲。 這實際上就是視需要的上傳。|  
  
 **使用收集項**  
  
 下表描述的是您可以用來處理收集項的預存程序。  
  
|程序名稱|Description|  
|--------------------|-----------------|  
|[sp_syscollector_create_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)|建立收集項。|  
|[sp_syscollector_delete_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)|刪除收集項。|  
|[sp_syscollector_update_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)|更新收集項。|  
  
 **使用收集器型別**  
  
 下表描述的是您可以用來處理收集器型別的預存程序。  
  
|程序名稱|Description|  
|--------------------|-----------------|  
|[sp_syscollector_create_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collector-type-transact-sql.md)|建立收集器型別。|  
|[sp_syscollector_update_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collector-type-transact-sql.md)|更新收集器型別。|  
|[sp_syscollector_delete_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collector-type-transact-sql.md)|刪除收集器型別。|  
  
 **取得組態資訊**  
  
 下表描述您可用來取得組態資訊與執行記錄資料的檢視。  
  
|檢視表名稱|Description|  
|---------------|-----------------|  
|[syscollector_config_store &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)|取得資料收集器組態。|  
|[syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)|取得收集項資訊。|  
|[syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)|取得收集組資訊。|  
|[syscollector_collector_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)|取得收集器型別資訊。|  
|[syscollector_execution_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-transact-sql.md)|取得有關收集組與封裝執行的資訊。|  
|[syscollector_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)|取得有關工作執行的資訊。|  
|[syscollector_execution_log_full &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql.md)|當執行記錄已滿時取得資訊。|  
  
 **設定對管理資料倉儲的存取**  
  
 下表描述的是您可以用來設定對管理資料倉儲之存取的預存程序。  
  
|程序名稱|Description|  
|--------------------|-----------------|  
|[sp_syscollector_set_warehouse_database_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)|針對管理資料倉儲指定連接字串中所定義的資料庫名稱。|  
|[sp_syscollector_set_warehouse_instance_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)|針對管理資料倉儲指定連接字串中所定義的執行個體。|  
  
 **設定管理資料倉儲**  
  
 下表描述的是您可以用來處理管理資料倉儲組態的預存程序。  
  
|程序名稱|Description|  
|--------------------|-----------------|  
|[core.sp_create_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-create-snapshot-transact-sql.md)|在管理資料倉儲中建立集合快照集。|  
|[core.sp_update_data_source &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-update-data-source-transact-sql.md)|更新資料收集的資料來源。|  
|[core.sp_add_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-add-collector-type-transact-sql.md)|將收集器型別加入到管理資料倉儲。|  
|[core.sp_remove_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-remove-collector-type-transact-sql.md)|從管理資料倉儲中移除收集器型別。|  
|[core.sp_purge_data &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-purge-data-transact-sql.md)|從管理資料倉儲中刪除資料。|  
  
 **使用上傳封裝**  
  
 下表描述的是您可以用來處理上傳封裝的預存程序。  
  
|程序名稱|Description|  
|--------------------|-----------------|  
|[sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)|設定資料上傳的重試次數。|  
|[sp_syscollector_set_cache_directory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)|指定上傳重試之間的資料暫存儲存位置。|  
  
 **使用資料收集執行記錄**  
  
 下表描述的是您可以用來處理資料收集執行記錄的預存程序。  
  
|程序名稱|Description|  
|--------------------|-----------------|  
|[sp_syscollector_delete_execution_log_tree &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-execution-log-tree-transact-sql.md)|從執行記錄中刪除收集組項目。|  
  
### <a name="functions"></a>函數  
 下表描述的是您可以用來取得執行和追蹤資訊的函數。  
  
|函數名稱|Description|  
|-------------------|-----------------|  
|[fn_syscollector_get_execution_details &#40;Transact-SQL&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md)|取得特定封裝的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 執行記錄資料。|  
|[fn_syscollector_get_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-stats-transact-sql.md)|取得收集組或封裝的執行統計資料。 這些資訊包含所記錄的錯誤。|  
|[snapshots.fn_trace_getdata &#40;Transact-SQL&#41;](../../relational-databases/system-functions/snapshots-fn-trace-getdata-transact-sql.md)|取得使用一般 SQL 追蹤收集器型別來收集資料時所記錄的事件。|  
  
## <a name="see-also"></a>另請參閱  
 [執行預存程序](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)   
 [使用 SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)   
 [[資料收集]](../../relational-databases/data-collection/data-collection.md)  
  
  
