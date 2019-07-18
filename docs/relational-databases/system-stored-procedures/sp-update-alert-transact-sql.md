---
title: sp_update_alert (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_alert_TSQL
- sp_update_alert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_alert
ms.assetid: 4bbaeaab-8aca-4c9e-abc1-82ce73090bd3
author: stevestein
ms.author: sstein
ms.openlocfilehash: baecdca82d7edcb27196c7c43d9d071a82adf792
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084953"
---
# <a name="spupdatealert-transact-sql"></a>sp_update_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新現有警示的設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_update_alert   
     [ @name =] 'name'   
     [ , [ @new_name =] 'new_name']   
     [ , [ @enabled =] enabled]   
     [ , [ @message_id =] message_id]   
     [ , [ @severity =] severity]   
     [ , [ @delay_between_responses =] delay_between_responses]   
     [ , [ @notification_message =] 'notification_message']   
     [ , [ @include_event_description_in =] include_event_description_in]   
     [ , [ @database_name =] 'database']   
     [ , [ @event_description_keyword =] 'event_description_keyword']   
     [ , [ @job_id =] job_id | [@job_name =] 'job_name']   
     [ , [ @occurrence_count = ] occurrence_count]   
     [ , [ @count_reset_date =] count_reset_date]   
     [ , [ @count_reset_time =] count_reset_time]   
     [ , [ @last_occurrence_date =] last_occurrence_date]   
     [ , [ @last_occurrence_time =] last_occurrence_time]   
     [ , [ @last_response_date =] last_response_date]   
     [ , [ @last_response_time =] last_response _time]  
     [ , [ @raise_snmp_trap =] raise_snmp_trap]  
     [ , [ @performance_condition =] 'performance_condition' ]   
     [ , [ @category_name =] 'category']  
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @name = ] 'name'` 要更新的警示名稱。 *名稱*已**sysname**，沒有預設值。  
  
`[ @new_name = ] 'new_name'` 警示的新名稱。 名稱必須是唯一的。 *new_name*已**sysname**，預設值是 NULL。  
  
`[ @enabled = ] enabled` 指定是否啟用警示 (**1**)，或未啟用 (**0**)。 *已啟用*已**tinyint**，預設值是 NULL。 您必須啟用警示，才能引發警示。  
  
`[ @message_id = ] message_id` 警示定義新訊息或錯誤號碼。 通常*message_id*對應至中的錯誤號碼**sysmessages**資料表。 *message_id*已**int**，預設值是 NULL。 訊息識別碼可用於警示的嚴重性層級設定才**0**。  
  
`[ @severity = ] severity` 新的嚴重性層級 (從**1**透過**25**) 為警示定義。 任何[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳送至 Windows 應用程式記錄檔，且含有指定嚴重性的訊息都會啟動警示。 *嚴重性*已**int**，預設值是 NULL。 警示的訊息識別碼設定時，才可以使用嚴重性層級**0**。  
  
`[ @delay_between_responses = ] delay_between_responses` 新等待期間，以秒為單位，以警示回應之間。 *delay_between_responses*已**int**，預設值是 NULL。  
  
`[ @notification_message = ] 'notification_message'` 電子郵件，傳送給操作員之附加訊息的修訂的文字**網路傳送**，或呼叫器通知。 *notification_message*已**nvarchar(512)** ，預設值是 NULL。  
  
`[ @include_event_description_in = ] include_event_description_in` 指定是否 popis [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 應用程式記錄檔的錯誤應該包含在通知訊息。 *include_event_description_in*已**tinyint**，預設值是 NULL，而且可以是下列其中一個或多個這些值。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|None|  
|**1**|電子郵件|  
|**2**|呼叫器|  
|**4**|**net send**|  
|**7**|All|  
  
`[ @database_name = ] 'database'` 要引發的警示會因發生錯誤的資料庫名稱。 *資料庫*是**sysname。** 不允許以括號 ([ ]) 括住的名稱。 預設值是 NULL。  
  
`[ @event_description_keyword = ] 'event_description_keyword'` 必須找到的錯誤訊息記錄檔中的錯誤描述中的字元序列。 您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] LIKE 運算式模式比對字元。 *event_description_keyword*已**nvarchar(100)** ，預設值是 NULL。 此參數可用於篩選的物件名稱 (例如 **%customer_table%** )。  
  
`[ @job_id = ] job_id` 作業識別碼中。 *job_id*已**uniqueidentifier**，預設值是 NULL。 如果*job_id*指定，則*job_name*必須省略。  
  
`[ @job_name = ] 'job_name'` 而為了回應這個警示所執行之作業的名稱。 *job_name*已**sysname**，預設值是 NULL。 如果*job_name*指定，則*job_id*必須省略。  
  
`[ @occurrence_count = ] occurrence_count` 重設警示的發生次數。 *occurrence_count*已**int**，預設值是 NULL，而且可以只設定**0**。  
  
`[ @count_reset_date = ] count_reset_date` 重設上次重設出現計數的日期。 *count_reset_date*已**int**，預設值是 NULL。  
  
`[ @count_reset_time = ] count_reset_time` 重設上次重設出現計數的時間。 *count_reset_time*已**int**，預設值是 NULL。  
  
`[ @last_occurrence_date = ] last_occurrence_date` 重設警示上次發生的日期。 *last_occurrence_date*已**int**，預設值是 NULL，而且可以只設定**0**。  
  
`[ @last_occurrence_time = ] last_occurrence_time` 重設警示上次發生的時間。 *last_occurrence_time*已**int**，預設值是 NULL，而且可以只設定**0**。  
  
`[ @last_response_date = ] last_response_date` 重設警示上次回應到 SQLServerAgent 服務的日期。 *last_response_date*已**int**，預設值是 NULL，而且可以只設定**0**。  
  
`[ @last_response_time = ] last_response_time` 重設警示上次回應到 SQLServerAgent 服務的時間。 *last_response_time*已**int**，預設值是 NULL，而且可以只設定**0**。  
  
`[ @raise_snmp_trap = ] raise_snmp_trap` 保留。  
  
`[ @performance_condition = ] 'performance_condition'` 值，以表示格式 **'***itemcomparatorvalue***'** 。 *performance_condition*已**nvarchar(512)** ，預設值是 NULL，這些元素組成。  
  
|格式元素|描述|  
|--------------------|-----------------|  
|*項目*|計數器的效能物件、效能計數器或具名執行個體|  
|*Comparator*|是下列運算子之一： **>** ， **<** ， **=**|  
|*值*|計數器的數值|  
  
`[ @category_name = ] 'category'` 警示類別目錄名稱。 *類別目錄*已**sysname**預設值是 NULL。  
  
`[ @wmi_namespace = ] 'wmi_namespace'` 進行事件查詢 WMI 命名空間。 *wmi_namespace*已**sysname**，預設值是 NULL。  
  
`[ @wmi_query = ] 'wmi_query'` 指定警示之 WMI 事件查詢。 *wmi_query*已**nvarchar(512)** ，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 只有**sysmessages**寫入至[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 應用程式記錄檔可以引發警示。  
  
 **sp_update_alert**只變更這些警示設定的參數提供值。 如果省略某個參數，就會保留目前的設定。  
  
## <a name="permissions"></a>Permissions  
 若要執行這個預存程序，使用者必須隸屬**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會將 `Test Alert` 已啟用的設定值改成 `0`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_alert  
    @name = N'Test Alert',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
