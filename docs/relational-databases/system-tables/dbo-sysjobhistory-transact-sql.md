---
title: dbo.sysjobhistory (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.sysjobhistory_TSQL
- dbo.sysjobhistory
- sysjobhistory
- sysjobhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobhistory system table
ms.assetid: 1b1fcdbb-2af2-45e6-bf3f-e8279432ce13
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3ab9fbfb6a574f8f6c91ee15789c67cac204d5f3
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="dbosysjobhistory-transact-sql"></a>dbo.sysjobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 執行排程作業的相關資訊。 這份資料表儲存在**msdb**資料庫。  
  
> **注意：** 只有在 jobstep 完成之後，更新資料。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|資料列的唯一識別碼。|  
|**job_id**|**uniqueidentifier**|作業識別碼。|  
|**step_id**|**int**|作業中步驟的識別碼。|  
|**step_name**|**sysname**|步驟的名稱。|  
|**sql_message_id**|**int**|當作業失敗時，任何傳回的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤訊息的識別碼。|  
|**sql_severity**|**int**|任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤的嚴重性。|  
|**message**|**nvarchar(4000)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤 (如果有的話) 的文字。|  
|**run_status**|**int**|作業執行的狀態：<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **2** = 重試<br /><br /> **3** = 取消<br /><br /> **4** = 進行中|  
|**run_date**|**int**|作業或步驟開始執行的日期。 如果是「進行中」記錄，這就是開始寫入記錄的日期/時間。|  
|**run_time**|**int**|作業或步驟開始的時間。|  
|**run_duration**|**int**|中的作業或步驟中的執行的經過時間**HHMMSS**格式。|  
|**operator_id_emailed**|**int**|作業完成時所通知之操作員的識別碼。|  
|**operator_id_netsent**|**int**|當作業完成時，訊息所通知之操作員的識別碼。|  
|**operator_id_paged**|**int**|當作業完成時，呼叫器所通知之操作員的識別碼。|  
|**retries_attempted**|**int**|作業或步驟的重試次數。|  
|**伺服器**|**sysname**|執行作業的伺服器名稱。|  
  
  ## <a name="example"></a>範例
 下列[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢會將轉換**run_time**和**run_duration**成更多的使用者易記格式的資料行。  執行中的指令碼[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
 
 ```sql
 SET NOCOUNT ON;
 
 SELECT sj.name,
        sh.run_date,
        sh.step_name,
        STUFF(STUFF(RIGHT(REPLICATE('0', 6) +  CAST(sh.run_time as varchar(6)), 6), 3, 0, ':'), 6, 0, ':') 'run_time',
        STUFF(STUFF(STUFF(RIGHT(REPLICATE('0', 8) + CAST(sh.run_duration as varchar(8)), 8), 3, 0, ':'), 6, 0, ':'), 9, 0, ':') 'run_duration (DD:HH:MM:SS)  '
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobhistory sh
ON sj.job_id = sh.job_id
```
