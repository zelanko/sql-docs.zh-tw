---
title: "dbo.sysjobsteps (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysjobsteps
- dbo.sysjobsteps_TSQL
- sysjobsteps
- sysjobsteps_TSQL
dev_langs: TSQL
helpviewer_keywords: sysjobsteps system table
ms.assetid: 978b8205-535b-461c-91f3-af9b08eca467
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4f316e40cc6bf89cf7296b5a2d864406142f7f87
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysjobsteps-transact-sql"></a>dbo.sysjobsteps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 所要執行之作業中各個步驟的資訊。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|作業的識別碼。|  
|**step_id**|**int**|作業中步驟的識別碼。|  
|**step_name**|**sysname**|作業步驟的名稱。|  
|**子系統**|**nvarchar （40)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 用來執行作業步驟的子系統名稱。|  
|命令|**nvarchar(max)**|要執行的命令**子系統**。|  
|**旗標**|**int**|已保留。|  
|**additional_parameters**|**ntext**|已保留。|  
|**cmdexec_success_code**|**int**|所傳回的錯誤層級值**CmdExec**子系統步驟來表示成功。|  
|**on_success_action**|**tinyint**|當步驟執行成功時，所要執行的動作。|  
|**on_success_step_id**|**int**|當步驟執行成功時，所要執行的下一個步驟的識別碼。|  
|**on_fail_action**|**tinyint**|當步驟執行不成功時，所要執行的動作。|  
|**on_fail_step_id**|**int**|當步驟執行不成功時，所要執行的下一個步驟的識別碼。|  
|**伺服器**|**sysname**|已保留。|  
|**database_name**|**sysname**|所在的資料庫名稱**命令**，就會執行**子系統**是 TSQL。|  
|**database_user_name**|**sysname**|當執行步驟時，將使用其帳戶的資料庫使用者名稱。|  
|**retry_attempts**|**int**|作業失敗時的重試次數。|  
|**retry_interval**|**int**|重試的間隔等待時間。|  
|**os_run_priority**|**int**|已保留。|  
|**output_file_name**|**nvarchar(200)**|儲存步驟輸出所在的檔案名稱時**子系統**是 TSQL、 PowerShell 或**CmdExec***。*|  
|**last_run_outcome**|**int**|作業步驟上次執行的結果。<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **2** = 重試<br /><br /> **3** = 取消<br /><br /> **5** = 未知|  
|**last_run_duration**|**int**|上次執行步驟的持續期間 (hhmmss)。|  
|**last_run_retries**|**int**|作業步驟上次執行的重試次數。|  
|**last_run_date**|**int**|上次開始執行步驟的日期 (yyyymmdd)。|  
|**last_run_time**|**int**|上次開始執行步驟的時間 (hhmmss)。|  
|**proxy_id**|**int**|作業步驟的 Proxy。|  
|**step_uid**|**uniqueidentifier**|作業步驟的識別碼。|  
  
## <a name="see-also"></a>請參閱＜  
 [SQL Server Agent 資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
