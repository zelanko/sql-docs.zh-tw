---
description: sp_update_alert (Transact-SQL)
title: sp_update_alert (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 368e5694231f52c9c7c73835308cd6a3d5fe5b81
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547255"
---
# <a name="sp_update_alert-transact-sql"></a>sp_update_alert (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @name = ] 'name'` 要更新的警示名稱。 *名稱* 是 **sysname**，沒有預設值。  
  
`[ @new_name = ] 'new_name'` 警示的新名稱。 名稱必須是唯一的。 *new_name* 是 **sysname**，預設值是 Null。  
  
`[ @enabled = ] enabled` 指定是否啟用警示 (**1**) 或未啟用 (**0**) 。 *enabled* 是 **Tinyint**，預設值是 Null。 您必須啟用警示，才能引發警示。  
  
`[ @message_id = ] message_id` 警示定義的新訊息或錯誤號碼。 一般來說， *message_id* 會對應到 **sysmessages** 資料表中的錯誤號碼。 *message_id* 是 **int**，預設值是 Null。 只有當警示的嚴重性層級設定為 **0**時，才能使用訊息識別碼。  
  
`[ @severity = ] severity` 警示定義的新嚴重性層級 (從 **1** 到 **25**) 。 任何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳送至 Windows 應用程式記錄檔且具有指定嚴重性的訊息都會啟動警示。 *嚴重性* 是 **int**，預設值是 Null。 只有當警示的訊息識別碼設定為 **0**時，才能使用嚴重性層級。  
  
`[ @delay_between_responses = ] delay_between_responses` 警示回應之間的新等候期間（以秒為單位）。 *delay_between_responses* 是 **int**，預設值是 Null。  
  
`[ @notification_message = ] 'notification_message'` 以電子郵件、 **net send**或傳呼通知的一部分傳送給操作員的額外訊息的修訂文字。 *notification_message* 是 **Nvarchar (512) **，預設值是 Null。  
  
`[ @include_event_description_in = ] include_event_description_in` 指定是否 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 應該將 Windows 應用程式記錄檔中的錯誤描述包含在通知訊息中。 *include_event_description_in* 是 **Tinyint**，預設值是 Null，而且可以是下列其中一個或多個值。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|無|  
|**1**|電子郵件|  
|**2**|呼叫器|  
|**4**|**net send**|  
|**7**|全部|  
  
`[ @database_name = ] 'database'` 必須發生錯誤才能引發警示的資料庫名稱。 *資料庫* 為 **sysname。** 不允許以括號 ([ ]) 括住的名稱。 預設值是 NULL。  
  
`[ @event_description_keyword = ] 'event_description_keyword'` 在錯誤訊息記錄檔中的錯誤描述中必須找到的字元序列。 您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] LIKE 運算式模式比對字元。 *event_description_keyword* 是 **Nvarchar (100) **，預設值是 Null。 此參數適用于篩選物件名稱 (例如 **% customer_table%**) 。  
  
`[ @job_id = ] job_id` 作業識別碼。 *job_id* 是 **uniqueidentifier**，預設值是 Null。 如果指定 *job_id* ，就必須省略 *job_name* 。  
  
`[ @job_name = ] 'job_name'` 回應此警示所執行的作業名稱。 *job_name* 是 **sysname**，預設值是 Null。 如果指定 *job_name* ，就必須省略 *job_id* 。  
  
`[ @occurrence_count = ] occurrence_count` 重設警示的發生次數。 *occurrence_count* 是 **int**，預設值是 Null，而且只能設定為 **0**。  
  
`[ @count_reset_date = ] count_reset_date` 重設前次重設出現計數的日期。 *count_reset_date* 是 **int**，預設值是 Null。  
  
`[ @count_reset_time = ] count_reset_time` 重設前次重設出現計數的時間。 *count_reset_time* 是 **int**，預設值是 Null。  
  
`[ @last_occurrence_date = ] last_occurrence_date` 重設警示上次發生的日期。 *last_occurrence_date* 是 **int**，預設值是 Null，而且只能設定為 **0**。  
  
`[ @last_occurrence_time = ] last_occurrence_time` 重設上次發生警示的時間。 *last_occurrence_time* 是 **int**，預設值是 Null，而且只能設定為 **0**。  
  
`[ @last_response_date = ] last_response_date` 重設 SQLServerAgent 服務上次回應警示的日期。 *last_response_date* 是 **int**，預設值是 Null，而且只能設定為 **0**。  
  
`[ @last_response_time = ] last_response_time` 重設 SQLServerAgent 服務上次回應警示的時間。 *last_response_time* 是 **int**，預設值是 Null，而且只能設定為 **0**。  
  
`[ @raise_snmp_trap = ] raise_snmp_trap` 保留。  
  
`[ @performance_condition = ] 'performance_condition'` 以 **'**_itemcomparatorvalue_**'** 格式表示的值。 *performance_condition* 是 **Nvarchar (512) **，預設值是 Null，且包含這些元素。  
  
|格式元素|描述|  
|--------------------|-----------------|  
|*Item*|計數器的效能物件、效能計數器或具名執行個體|  
|*比較*|下列其中一個運算子： **>** 、 **<** 、 **=**|  
|*值*|計數器的數值|  
  
`[ @category_name = ] 'category'` 警示類別目錄的名稱。 *category* 是 **sysname** ，預設值是 Null。  
  
`[ @wmi_namespace = ] 'wmi_namespace'` 要查詢事件的 WMI 命名空間。 *wmi_namespace* 是 **sysname**，預設值是 Null。  
  
`[ @wmi_query = ] 'wmi_query'` 指定警示之 WMI 事件的查詢。 *wmi_query* 是 **Nvarchar (512) **，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 只有**sysmessages**寫入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式記錄檔的 sysmessages 才會引發警示。  
  
 **sp_update_alert** 只會變更提供參數值的警示設定。 如果省略某個參數，就會保留目前的設定。  
  
## <a name="permissions"></a>權限  
 若要執行這個預存程式，使用者必須是 **系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
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
 [sp_help_alert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
