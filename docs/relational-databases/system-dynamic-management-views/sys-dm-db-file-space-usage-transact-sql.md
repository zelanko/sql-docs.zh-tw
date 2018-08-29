---
title: sys.dm_db_file_space_usage (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_file_space_usage
- sys.dm_db_file_space_usage_TSQL
- sys.dm_db_file_space_usage
- dm_db_file_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_file_space_usage dynamic management view
ms.assetid: 148a5276-a8d5-49d2-8146-3c63d24c2144
caps.latest.revision: 45
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4fc8ca096f77d029e9632f01af21cc4a49f95278
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43107333"
---
# <a name="sysdmdbfilespaceusage-transact-sql"></a>sys.dm_db_file_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回資料庫中每一個檔案的空間使用方式資訊。  
  
> [!NOTE]  
>  若要呼叫這個屬性從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或是[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_db_file_space_usage**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|資料庫識別碼。|  
|file_id|**smallint**|檔案識別碼。<br /><br /> file_id 會對應至中的 file_id [sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md)和中的 fileid [sys.sysfiles](../../relational-databases/system-compatibility-views/sys-sysfiles-transact-sql.md)。|  
|filegroup_id|**smallint**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 檔案群組識別碼。|  
|total_page_count|**bigint**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 檔案中的總頁數。|  
|allocated_extent_page_count|**bigint**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 檔案中的已配置範圍中的總頁數。|  
|unallocated_extent_page_count|**bigint**|檔案中的未配置範圍中的總頁數。<br /><br /> 不包含已配置範圍中的未使用頁面。|  
|version_store_reserved_page_count|**bigint**|配置給版本存放區的一致範圍中的總頁數。 絕不從混合範圍配置版本存放區頁面。<br /><br /> 不包含 IAM 頁面，因為它們一律從混合範圍中配置。 如果 PFS 頁面是從一致範圍配置，則會包含它們。<br /><br /> 如需詳細資訊，請參閱 [sys.dm_tran_version_store &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md)。|  
|user_object_reserved_page_count|**bigint**|從一致範圍中配置給資料庫使用者物件的總頁數。 這個計數不包括已配置範圍中的未使用頁面。<br /><br /> 不包含 IAM 頁面，因為它們一律從混合範圍中配置。 如果 PFS 頁面是從一致範圍配置，則會包含它們。<br /><br /> 您可以使用中的 total_pages 資料行[sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)目錄檢視，以傳回使用者物件中的每一個配置單位的保留的頁面計數。 不過請注意，total_pages 資料行包含 IAM 頁面。|  
|internal_object_reserved_page_count|**bigint**|配置給檔案中內部物件之一致範圍中的總頁數。 這個計數不包括已配置範圍中的未使用頁面。<br /><br /> 不包含 IAM 頁面，因為它們一律從混合範圍中配置。 如果 PFS 頁面是從一致範圍配置，則會包含它們。<br /><br /> 沒有目錄檢視或動態管理物件可傳回每一個內部物件的頁數。|  
|mixed_extent_page_count|**bigint**|檔案中已配置混合範圍的已配置和未配置總頁數。 混合範圍包含已配置給不同物件的頁面。 這個計數包含檔案中的所有 IAM 頁面。|
|modified_extent_page_count|**bigint**|**適用於**：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br />中修改的頁面總數前次完整資料庫備份之後，配置檔案的範圍。 已修改的頁面計數可用來追蹤資料庫中的差異變更數量自上次完整備份的詳細資訊，決定如果需要差異備份。|
|pdw_node_id|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 這個分佈是在節點的識別碼。|  
|distribution_id|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 與發佈相關聯的唯一數值識別碼。|  
  
## <a name="remarks"></a>備註  
 頁數一律在範圍層級上產生。 因此，頁數值一定是 8 的倍數。 包含 Global Allocation Map (GAM) 和 Shared Global Allocation Map (SGAM) 配置頁的範圍就是已配置的一致範圍。 上述頁數並不包含它們。 如需有關分頁與範圍的詳細資訊，請參閱 <<c0> [ 分頁與範圍架構指南](../../relational-databases/pages-and-extents-architecture-guide.md)。 
  
 目前的版本存放區的內容位於[sys.dm_tran_version_store](../../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md)。 版本存放區頁面是在檔案層級上追蹤，而不是工作階段和工作層級，因為它們是全域資源。 工作階段可產生版本，但工作階段結束時無法移除版本。 版本存放區清除必須考慮需要存取特定版本之執行最久的交易。 藉由檢視 elapsed_time_seconds 資料行中的，可以探索與版本存放區清除相關最長執行的交易[sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md)。  
  
 mixed_extent_page_count 資料行的經常性變更可指出 SGAM 頁面使用頻繁。 發生這個情形時，您會看到許多 PAGELATCH_UP 等待，其中的等待資源就是 SGAM 頁面。 如需詳細資訊，請參閱[sys.dm_os_waiting_tasks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md)， [sys.dm_os_wait_stats &#40;-&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)，以及[sys.dm_os_latch_統計資料&#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)。  
  
## <a name="user-objects"></a>使用者物件  
 下列物件已包括在使用者物件頁面計數器中：  
  
-   使用者自訂資料表和索引  
  
-   系統資料表和索引  
  
-   全域暫存資料表和索引  
  
-   本機暫存資料表和索引  
  
-   資料表變數  
  
-   資料表值函式中傳回的資料表  
  
## <a name="internal-objects"></a>內部物件  
 內部物件只位於 tempdb 中。 下列物件已包括在內部物件頁面計數器中：  
  
-   用於資料指標或多工緩衝處理作業和暫存大型物件 (LOB) 儲存體的工作資料表  
  
-   用於如雜湊聯結等作業的工作檔案  
  
-   排序執行  
  
## <a name="relationship-cardinalities"></a>關聯性基數  
  
|來源|若要|關聯性|  
|----------|--------|------------------|  
|sys.dm_db_file_space_usage.database_id, file_id|sys.dm_io_virtual_file_stats.database_id, file_id|一對一|  
  
## <a name="permissions"></a>Permissions

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   

## <a name="examples"></a>範例  
  
### <a name="determing-the-amount-of-free-space-in-tempdb"></a>判斷 tempdb 的可用空間量  
 下列查詢會傳回 （單位為 MB) 可在中的所有檔案中的頁數和總空間總數**tempdb**。  
  
```sql
USE tempdb;  
GO  
SELECT SUM(unallocated_extent_page_count) AS [free pages],   
(SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]  
FROM sys.dm_db_file_space_usage;  
```  

### <a name="determining-the-amount-of-space-used-by-user-objects"></a>判斷使用者物件使用的空間量  
 下列查詢會傳回 tempdb 中使用者物件使用的總頁數和使用者物件使用的總空間。  
  
```sql  
USE tempdb;  
GO  
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],  
(SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]  
FROM sys.dm_db_file_space_usage;
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_db_task_space_usage &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
 [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
