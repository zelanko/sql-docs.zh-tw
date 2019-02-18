---
title: Stretch Database 的擴充事件 | Microsoft Docs
ms.date: 06/14/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 70485e74-2e25-4e7e-be6c-9dd1780a42e3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 87199dc69a19f5328df495cc31276e6f16c8e0bd
ms.sourcegitcommit: ec1f01b4bb54621de62ee488decf9511d651d700
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2019
ms.locfileid: "56240782"
---
# <a name="extended-events-for-stretch-database"></a>Stretch Database 的擴充事件
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


Stretch Database 提供一組疑難排解用的擴充事件。  
  
如需詳細資訊，請參閱 [擴充事件](../../relational-databases/extended-events/extended-events.md)。 如需如何開始進行疑難排解之擴充事件工作階段的詳細資訊，請參閱 [建立擴充事件工作階段](https://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74)  
  
## <a name="list-of-extended-events-for-stretch-database"></a>Stretch Database 的擴充事件清單  
  
事件名稱|事件描述   
---------|---------  
remote_data_archive_db_ddl|在處理用於延伸資料的資料庫 T-SQL ddl 時發生。  
remote_data_archive_provision_operation|在佈建作業開始或結束時發生。  
remote_data_archive_query_rewrite|為 Stretch 進行查詢重寫期間取代 RelOp_Get 時發生。  
remote_data_archive_table_ddl|在處理用於延伸資料的資料表 T-SQL ddl 時發生。  
remote_data_archive_telemetry|每次內部部署系統傳輸遙測事件至 Azure 資料庫時發生。  
remote_data_archive_telemetry_rejected|每次 Azure 資料庫伸展遙測事件遭拒時發生  
repopulate_stretch_schema_task_queue_complete|報告重新填入延展結構描述工作佇列已完成。  
repopulate_stretch_schema_task_queue_start|報告重新填入延展結構描述工作佇列已開始。  
stretch_codegen_errorlog|回報來自程式碼產生器的輸出  
stretch_codegen_start|回報伸展程式碼產生的開始處  
stretch_create_remote_table_start|回報遠端資料表建立的開始處  
stretch_database_disable_completed|回報完成 ALTER DATABASE SET REMOTE_DATA_ARCHIVE OFF 命令  
stretch_database_enable_completed|回報完成 ALTER DATABASE SET REMOTE_DATA_ARCHIVE ON 命令  
stretch_database_reauthorize_completed|回報已完成 sp_rda_reauthorize_db 規格程序  
stretch_index_reconciliation_codegen_completed|報告伸展遠端索引作業的程式碼產生完成  
stretch_index_update_step_completed|報告伸展的索引更新作業持續時間  
stretch_migration_debug_trace|伸展移轉動作的偵錯追蹤。  
stretch_migration_dequeue_migration|當資料庫的彈性移轉作業從佇列中清除時，即會引發此事件。  
stretch_migration_queue_migration|將封包排入佇列以開始移轉資料庫與物件。  
stretch_migration_requeue_migration|當彈性移轉作業封包重新排入佇列時，即會引發此事件。  
stretch_migration_start_migration|開始移轉資料庫與物件。  
stretch_migration_start_unmigration|開始取消移轉資料庫與物件。  
stretch_remote_column_execution_completed|回報完成遠端執行伸展資料行程式碼產生  
stretch_remote_column_reconciliation_codegen_completed|回報已完成延展遠端資料行調整的程式碼產生作業  
stretch_remote_index_execution_completed|回報完成遠端執行伸展索引程式碼產生  
stretch_schema_queue_task|報告封包何時進入佇列來處理資料庫和物件的結構描述工作。  
stretch_schema_script_execution_completed|報告已在處理延展結構描述工作的期間完成執行延展指令碼。  
stretch_schema_script_execution_skipped|報告已在處理延展結構描述工作的期間略過延展指令碼的執行。  
stretch_schema_script_execution_start|報告已在處理延展結構描述工作的期間開始執行延展指令碼。  
stretch_schema_task_failed|報告在延展結構描述工作期間的延展結構描述函數已失敗。  
stretch_schema_task_skipped|回報在延展結構描述函數期間已略過延展結構描述工作。  
stretch_schema_task_start|報告伸展結構描述工作期間的伸展結構描述函數開始。  
stretch_schema_task_succeeded|報告在延展結構描述工作期間的延展結構描述函數已成功完成。  
stretch_sp_migration_get_batch_id|呼叫 sp_stretch_get_batch_id  
stretch_sync_metadata_start|回報移轉工作期間中繼資料檢查的開始處。  
stretch_table_codegen_completed|回報完成伸展資料表的程式碼產生  
stretch_table_complete_data_reconciliation|完成資料庫與物件的資料調整。  
stretch_table_data_reconciliation_event|回報完成某批資料列的資料調整  
stretch_table_data_reconciliation_results_event|回報已成功完成幾批資料列的資料調整，或作業發生錯誤  
stretch_table_hinted_admin_delete_event|回報使用系統管理提示來執行延展刪除 DML 作業  
stretch_table_hinted_admin_update_event|回報使用系統管理提示來執行延展更新 DML 作業  
stretch_table_provisioning_step_completed|回報伸展的資料表佈建作業的期間  
stretch_table_query_error|報告彈性查詢重新寫入期間擲回的錯誤  
stretch_table_remote_creation_completed|回報完成遠端執行伸展資料表程式碼產生  
stretch_table_row_migration_event|回報完成資料列批次移轉  
stretch_table_row_migration_results_event|回報已成功完成幾批資料列的移轉，或作業發生錯誤  
stretch_table_row_unmigration_event|回報完成取消資料列批次移轉  
stretch_table_row_unmigration_results_event|回報已成功完成幾批資料列的取消移轉，或作業發生錯誤  
stretch_table_start_data_reconciliation|啟動資料庫與物件的資料調整。  
stretch_table_unprovision_completed|回報完成移除未伸展的資料表本機資源  
stretch_table_validation_error|回報完成使用者啟用伸展時的資料表驗證  
stretch_unprovision_table_start|回報伸展資料表解除佈建的開始處  
  
## <a name="see-also"></a>另請參閱  
[管理 Stretch Database 並對其進行疑難排解](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  

