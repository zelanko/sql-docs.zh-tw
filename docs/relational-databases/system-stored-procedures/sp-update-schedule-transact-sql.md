---
title: sp_update_schedule (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_update_schedule
- sp_update_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_schedule
ms.assetid: 97b3119b-e43e-447a-bbfb-0b5499e2fefe
caps.latest.revision: 42
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed8a500af524796cf98a16f9da75aae003375c1a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spupdateschedule-transact-sql"></a>sp_update_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 排程的設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_update_schedule   
    {   [ @schedule_id = ] schedule_id   
      | [ @name = ] 'schedule_name' }  
    [ , [ @new_name = ] new_name ]  
    [ , [ @enabled = ] enabled ]  
    [ , [ @freq_type = ] freq_type ]  
    [ , [ @freq_interval = ] freq_interval ]   
    [ , [ @freq_subday_type = ] freq_subday_type ]   
    [ , [ @freq_subday_interval = ] freq_subday_interval ]   
    [ , [ @freq_relative_interval = ] freq_relative_interval ]   
    [ , [ @freq_recurrence_factor = ] freq_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time = ] active_start_time ]   
    [ , [ @active_end_time = ] active_end_time ]   
    [ , [ @owner_login_name = ] 'owner_login_name' ]  
    [ , [ @automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@schedule_id =** ] *schedule_id*  
 這是要修改的排程識別碼。 *schedule_id*是**int**，沒有預設值。 任一*schedule_id*或*schedule_name*必須指定。  
  
 [ **@name =** ]  **'***schedule_name***'**  
 這是要修改的排程名稱。 *schedule_name*是**sysname**，沒有預設值。 任一*schedule_id*或*schedule_name*必須指定。  
  
 [ **@new_name**= ] *new_name*  
 排程的新名稱。 *new_name*是**sysname**，預設值是 NULL。 當*new_name*是 NULL，排程的名稱不會變更。  
  
 [  **@enabled =** ]*啟用*  
 指出排程的目前狀態。 *啟用*是**tinyint**，預設值是**1** （啟用）。 如果**0**，未啟用排程。 當未啟用排程時，不會依據這份排程來執行任何作業。  
  
 [ **@freq_type =** ] *freq_type*  
 指出將執行作業之時間的值。 *freq_type*是**int**，預設值是**0**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月，相對於*頻率間隔*|  
|**64**|在 SQLServerAgent 服務啟動之時執行|  
|**128**|在電腦閒置之時執行|  
  
 [ **@freq_interval =** ] *freq_interval*  
 執行作業的天數。 *freq_interval*是**int**，預設值是**0**，取決於值和*freq_type*。  
  
|值*freq_type*|在影響*freq_interval*|  
|---------------------------|--------------------------------|  
|**1** （一次）|*freq_interval*未使用。|  
|**4** （每天）|每個*freq_interval*天。|  
|**8** （每週）|*freq_interval*是下列一或多個項目 (結合**OR**邏輯運算子):<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **4** = 星期二<br /><br /> **8** = 星期三<br /><br /> **16** = 星期四<br /><br /> **32** = 星期五<br /><br /> **64** = 星期六|  
|**16** （每月）|在*freq_interval*月份的日期。|  
|**32** （每月相對）|*freq_interval*是下列其中之一：<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **3** = 星期二<br /><br /> **4** = 星期三<br /><br /> **5** = 星期四<br /><br /> **6** = 星期五<br /><br /> **7** = 星期六<br /><br /> **8** = 日<br /><br /> **9** = 工作日<br /><br /> **10** = 週末|  
|**64** （當 SQLServerAgent 服務啟動時）|*freq_interval*未使用。|  
|**128**|*freq_interval*未使用。|  
  
 [ **@freq_subday_type =** ] *freq_subday_type*  
 指定的單位*freq_subday_interval * *。* *freq_subday_type*是**int**，預設值是**0**，而且可以是下列值之一。  
  
|Value|描述 (單位)|  
|-----------|--------------------------|  
|**0x1**|在指定的時間|  
|**0x2**|秒|  
|**0x4**|Minutes|  
|**0x8**|小時|  
  
 [ **@freq_subday_interval =** ] *freq_subday_interval*  
 數目*freq_subday_type*期間每次執行作業之間發生。 *freq_subday_interval*是**int**，預設值是**0**。  
  
 [ **@freq_relative_interval =** ] *freq_relative_interval*  
 發生作業的*freq_interval*中每個月，如果*freq_interval*是**32** （每月相對）。 *freq_relative_interval*是**int**，預設值是**0**，而且可以是下列值之一。  
  
|Value|描述 (單位)|  
|-----------|--------------------------|  
|**1**|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
  
 [ **@freq_recurrence_factor =** ] *freq_recurrence_factor*  
 作業的各排程執行之間的週數或月數。 *freq_type*才會使用*freq_type*是**8**， **16**，或**32**。 *freq_type*是**int**，預設值是**0**。  
  
 [ **@active_start_date =** ]  *active_start_date*  
 可以開始執行作業的日期。 *active_start_date*是**int**，預設值是 NULL，表示今天的日期。 日期格式為 YYYYMMDD。 如果*active_start_date*不是 NULL，日期必須大於或等於 19900101。  
  
 建立排程之後，檢閱開始日期，並確認該日期正確。 如需詳細資訊，請參閱 「 排程開始日期 」 一節中[建立及附加排程至作業](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5)。  
  
 [ **@active_end_date =** ] *active_end_date*  
 可以停止執行作業的日期。 *active_end_date*是**int**，預設值是**99991231**，表示年 12 月 31 日到 9999。 格式為 YYYYMMDD。  
  
 [ **@active_start_time =** ] *active_start_time*  
 之間任何一天的時間*active_start_date*和*active_end_date*開始執行的作業。 *active_start_time*是**int**，預設值是 000000，表示 12:00:00 A.M. 必須用 HHMMSS 格式來輸入。  
  
 [ **@active_end_time =** ] *active_end_time*  
 之間任何一天的時間*active_start_date*和*active_end_date*結束執行作業。 *active_end_time*是**int**，預設值是**235959**，表示下午 11:59:59 必須用 HHMMSS 格式來輸入。  
  
 [ **@owner_login_name**= ] **'***owner_login_name***'**]  
 擁有排程之伺服器主體的名稱。 *owner_login_name*是**sysname**，預設值是 NULL，表示排程建立者所擁有。  
  
 [ **@automatic_post =**] *automatic_post*  
 已保留。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 所有使用排程的作業都會立即使用新設定。 不過，變更排程並不會停止目前在執行中的作業。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 只有成員**sysadmin**可以修改另一位使用者所擁有的排程。  
  
## <a name="examples"></a>範例  
 下列範例會將 `NightlyJobs` 排程的啟用狀態改成 `0`，並將擁有者設為 `terrid`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_schedule  
    @name = 'NightlyJobs',  
    @enabled = 0,  
    @owner_login_name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立並附加排程至作業](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5)   
 [排程的作業](http://msdn.microsoft.com/library/f626390a-a3df-4970-b7a7-a0529e4a109c)   
 [建立排程](http://msdn.microsoft.com/library/8c7ef3b3-c06d-4a27-802d-ed329dc86ef3)   
 [SQL Server Agent 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_add_jobschedule &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
