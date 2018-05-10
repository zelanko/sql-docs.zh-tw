---
title: sys.dm_exec_background_job_queue_stats (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_background_job_queue_stats
- sys.dm_exec_background_job_queue_stats
- dm_exec_background_job_queue_stats_TSQL
- sys.dm_exec_background_job_queue_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_background_job_queue_stats dynamic management view
ms.assetid: 27f62ab5-46c4-417e-814d-8d6437034d1c
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 18691bc0c024327495ff4a44525c9715880b688f
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmexecbackgroundjobqueuestats-transact-sql"></a>sys.dm_exec_background_job_queue_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回提供每一個查詢處理器作業的彙總統計資料的資料列，這些作業已提交進行非同步 (背景) 執行。  
  
> [!NOTE]  
>  若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_exec_background_job_queue_stats**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**queue_max_len**|**int**|佇列的最大長度。|  
|**enqueued_count**|**int**|成功公佈到佇列的要求數目。|  
|**started_count**|**int**|已啟動執行的要求數目。|  
|**ended_count**|**int**|成功或失敗的要求數目。|  
|**failed_lock_count**|**int**|因鎖定競爭或死結而失敗的要求數目。|  
|**failed_other_count**|**int**|因其他原因而失敗的要求數目。|  
|**failed_giveup_count**|**int**|因達到重試限制而失敗的要求數目。|  
|**enqueue_failed_full_count**|**int**|因佇列已滿而失敗的加入佇列嘗試次數。|  
|**enqueue_failed_duplicate_count**|**int**|重複加入佇列的嘗試次數。|  
|**elapsed_avg_ms**|**int**|要求的平均經歷時間 (以毫秒為單位)。|  
|**elapsed_max_ms**|**int**|最長要求的經歷時間 (以毫秒為單位)。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="remarks"></a>備註  
 這個檢視只會傳回非同步更新統計資料作業的資訊。 如需有關非同步更新統計資料的詳細資訊，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。  
  
## <a name="permissions"></a>Permissions

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   

## <a name="examples"></a>範例  
  
### <a name="a-determining-the-percentage-of-failed-background-jobs"></a>A. 判斷背景作業失敗的百分比  
 下列範例會傳回所有執行查詢的背景作業失敗百分比。  
  
```  
SELECT   
        CASE ended_count WHEN 0   
                THEN 'No jobs ended'   
                ELSE CAST((failed_lock_count + failed_giveup_count + failed_other_count) / CAST(ended_count AS float) * 100 AS varchar(20))   
        END AS [Percent Failed]  
FROM sys.dm_exec_background_job_queue_stats;  
GO  
```  
  
### <a name="b-determining-the-percentage-of-failed-enqueue-attempts"></a>B. 判斷嘗試加入佇列失敗的百分比  
 下列範例會傳回所有執行查詢的加入佇列嘗試失敗百分比。  
  
```  
SELECT   
        CASE enqueued_count WHEN 0   
                THEN 'No jobs posted'   
                ELSE CAST((enqueue_failed_full_count + enqueue_failed_duplicate_count) / CAST(enqueued_count AS float) * 100 AS varchar(20))   
        END AS [Percent Enqueue Failed]  
FROM sys.dm_exec_background_job_queue_stats;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [執行相關動態管理檢視和函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


