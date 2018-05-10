---
title: sys.dm_exec_background_job_queue (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_background_job_queue
- sys.dm_exec_background_job_queue_TSQL
- dm_exec_background_job_queue_TSQL
- sys.dm_exec_background_job_queue
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_background_job_queue dynamic management function
ms.assetid: 05d9884f-b74c-4e3c-a23b-c90c1ea5ef02
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ac977a052ae482b4c8693e7a7d7b10aeb73552ec
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmexecbackgroundjobqueue-transact-sql"></a>sys.dm_exec_background_job_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對每一個排程要非同步 (背景) 執行的查詢處理器作業，各傳回一個資料列。  
  
> **注意！！** 若要呼叫從**[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]** 或**[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**，使用名稱**sys.dm_pdw_nodes_exec_background_job_queue**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**time_queued**|**datetime**|將作業加入佇列的時間。|  
|**job_id**|**int**|作業識別碼。|  
|**database_id**|**int**|執行作業的資料庫。|  
|**object_id1**|**int**|此值將視作業類型而定。 如需詳細資訊，請參閱＜備註＞一節。|  
|**object_id2**|**int**|此值將視作業類型而定。 如需詳細資訊，請參閱＜備註＞一節。|  
|**object_id3**|**int**|此值將視作業類型而定。 如需詳細資訊，請參閱＜備註＞一節。|  
|**object_id4**|**int**|此值將視作業類型而定。 如需詳細資訊，請參閱＜備註＞一節。|  
|**error_code**|**int**|因為失敗而重新插入作業的錯誤碼。 如果是已暫停 (而不是已收取或已完成)，則為 NULL。|  
|**request_type**|**smallint**|作業要求的類型。|  
|**retry_count**|**smallint**|從佇列挑選作業以及因為缺乏資源或其他原因而重新插入的次數。|  
|**in_progress**|**smallint**|指出作業是否已經開始執行。<br /><br /> 1 = 已啟動<br /><br /> 0 = 仍在等候中|  
|**session_id**|**smallint**|工作階段識別碼。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="permissions"></a>Permissions

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
  
## <a name="remarks"></a>備註  
 這個檢視只會傳回非同步更新統計資料作業的資訊。 如需有關非同步更新統計資料的詳細資訊，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。  
  
 值**object_id1**透過**object_id4**作業要求的類型而定。 下表將摘錄這些資料行在不同作業類型的意義。  
  
|要求類型|object_id1|object_id2|object_id3|object_id4|  
|------------------|-----------------|-----------------|-----------------|-----------------|  
|非同步更新統計資料|資料表或檢視識別碼|統計資料識別碼|未使用|未使用|  
  
## <a name="examples"></a>範例  
 下列範例會傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中，每個資料庫背景佇列的作用中非同步作業數。  
  
```  
SELECT DB_NAME(database_id) AS [Database], COUNT(*) AS [Active Async Jobs]  
FROM sys.dm_exec_background_job_queue  
WHERE in_progress = 1  
GROUP BY database_id;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [執行相關動態管理檢視和函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [統計資料](../../relational-databases/statistics/statistics.md)   
 [KILL STATS JOB &#40;Transact SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)  
  
  



