---
title: dm_pdw_resource_waits (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/26/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a43ce9a2-5261-41e3-97f0-555ba05ebed9
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 83d4fda9c4e2a4d7f9eabd29a101e51a8d5cd8ab
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197157"
---
# <a name="sysdm_pdw_resource_waits-transact-sql"></a>dm_pdw_resource_waits (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  顯示中所有資源類型的等候資訊 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|要求在等候清單中的位置。|以零為基底的序數。 這在所有等候專案中都不是唯一的。|  
|session_id|**nvarchar(32)**|發生等候狀態之會話的識別碼。|請參閱[dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)中的 session_id。|  
|類型|**nvarchar(255)**|此專案所代表的等候類型。|可能的值：<br /><br /> 連線<br /><br /> 區域變數並行查詢<br /><br /> 分散式查詢並行<br /><br /> DMS 並行<br /><br /> 備份並行|  
|object_type|**nvarchar(255)**|受等候影響的物件類型。|可能的值：<br /><br /> **目標**<br /><br /> **資料**<br /><br /> **筆記本電腦**<br /><br /> **SCHEMA**<br /><br /> **應用程式**|  
|object_name|**Nvarchar (386) **|受等候影響之指定物件的名稱或 GUID。|資料表和 views 會以三個部分的名稱顯示。<br /><br /> 索引和統計資料會顯示四部分名稱。<br /><br /> 名稱、主體和資料庫都是字串名稱。|  
|request_id|**nvarchar(32)**|發生等候狀態之要求的識別碼。|要求的 QID 識別碼。<br /><br /> 載入要求的 GUID 識別碼。|  
|request_time|**datetime**|要求鎖定或資源的時間。||  
|acquire_time|**datetime**|取得鎖定或資源的時間。||  
|state|**nvarchar(50)**|等候狀態的狀態。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|等待專案的優先順序。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**int**|內部|請參閱下方的[監視資源等候](#monitor-resource-waits)|  
|resource_class|**Nvarchar (20) **|內部 |請參閱下方的[監視資源等候](#monitor-resource-waits)|  
  
## <a name="monitor-resource-waits"></a>監視資源等候 
隨著[工作負載群組](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-workload-isolation)的引進，平行存取插槽已不再適用。  使用下列查詢和資料 `resources_requested` 行，以瞭解執行要求所需的資源。

```sql
select rw.wait_id
      ,rw.session_id
      ,rw.type
      ,rw.object_type
      ,rw.object_name
      ,rw.request_id
      ,rw.request_time
      ,rw.acquire_time
      ,rw.state
      ,resources_requested = s.effective_request_min_resource_grant_percent
      ,r.group_name
  from sys.dm_workload_management_workload_groups_stats s
  join sys.dm_pdw_exec_requests r on r.group_name = s.name collate SQL_Latin1_General_CP1_CI_AS
  join sys.dm_pdw_resource_waits rw on rw.request_id = r.request_id
```

## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
