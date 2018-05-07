---
title: dbo.sysjobactivity (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.sysjobactivity_TSQL
- dbo.sysjobactivity
- sysjobactivity
- sysjobactivity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobactivity system table
ms.assetid: fd17cac9-5d1f-4b44-b2dc-ee9346d8bf1e
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a1d9e79856ac767d231993165b0c6d565d791464
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="dbosysjobactivity-transact-sql"></a>dbo.sysjobactivity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  記錄目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業的活動和狀態。  這份資料表儲存在**msdb**資料庫。
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|儲存在工作階段識別碼**syssessions**資料表中**msdb**資料庫。|  
|**job_id**|**uniqueidentifier**|作業的識別碼。|  
|**run_requested_date**|**datetime**|要求執行作業的日期和時間。|  
|**run_requested_source**|**sysname(nvarchar(128))**|執行作業的要求者。<br /><br /> **1** = SOURCE_SCHEDULER<br /><br /> **2** = SOURCE_ALERTER<br /><br /> **3** = SOURCE_BOOT<br /><br /> **4** = SOURCE_USER<br /><br /> **6** = SOURCE_ON_IDLE_SCHEDULE|  
|**queued_date**|**datetime**|將這項作業放入佇列的日期和時間。 如果是直接執行這項作業，這個資料行就是 NULL。|  
|**start_execution_date**|**datetime**|排程執行作業的日期和時間。|  
|**last_executed_step_id**|**int**|先前執行的最後一個作業步驟的識別碼。|  
|**last_executed_step_**<br /><br /> **date**|**datetime**|最後一個作業步驟開始執行的日期和時間。|  
|**stop_execution_date**|**datetime**|作業執行完成的日期和時間。|  
|**job_history_id**|**int**|用來識別中的資料列**sysjobhistory**資料表。|  
|**next_scheduled_run_date**|**datetime**|排程下一次執行作業的日期和時間。|  

## <a name="example"></a>範例
這個範例會傳回所有的 SQL Server Agent 作業的執行階段狀態。  在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中執行下列 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
```sql
SELECT sj.Name, 
    CASE
        WHEN sja.start_execution_date IS NULL THEN 'Not running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NULL THEN 'Running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NOT NULL THEN 'Not running'
    END AS 'RunStatus'
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobactivity sja
ON sj.job_id = sja.job_id
WHERE session_id = (
    SELECT MAX(session_id) FROM msdb.dbo.sysjobactivity); 
```
  
## <a name="see-also"></a>另請參閱  
 [dbo.sysjobhistory &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
  
  
