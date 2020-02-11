---
title: sp_help_alert （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_alert
- sp_help_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_alert
ms.assetid: 850cef4e-6348-4439-8e79-fd1bca712091
author: stevestein
ms.author: sstein
ms.openlocfilehash: a4b430884a497d9a8926f16f387b3608300f037c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "72304831"
---
# <a name="sp_help_alert-transact-sql"></a>sp_help_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  報告定義給伺服器之警示的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_alert [ [ @alert_name = ] 'alert_name' ]   
     [ , [ @order_by = ] 'order_by' ]   
     [ , [ @alert_id = ] alert_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @legacy_format = ] legacy_format ]  
```  
  
## <a name="arguments"></a>引數  
`[ @alert_name = ] 'alert_name'`警示名稱。 *alert_name*為**Nvarchar （128）**。 如果未指定*alert_name* ，就會傳回所有警示的相關資訊。  
  
`[ @order_by = ] 'order_by'`要用來產生結果的排序次序。 *order_by*是**sysname**，預設值是 N '*name*'。  
  
`[ @alert_id = ] alert_id`要報告其相關資訊之警示的識別碼。 *alert_id*是**int**，預設值是 Null。  
  
`[ @category_name = ] 'category'`警示的類別目錄。 *category*是**sysname**，預設值是 Null。  
  
`[ @legacy_format = ] legacy_format`這是指是否產生舊的結果集。 *legacy_format*是**bit**，預設值是**0**。 當*legacy_format*為**1**時， **sp_help_alert**會傳回**sp_help_alert**在 Microsoft SQL Server 2000 中傳回的結果集。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 當** \@legacy_format**為**0**時， **sp_help_alert**會產生下列結果集。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**號**|**int**|系統指派的唯一整數識別碼。|  
|**name**|**sysname**|警示名稱（例如，示範：完整的**msdb**記錄檔）。|  
|**event_source**|**Nvarchar （100）**|事件的來源。 7.0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版一律會**MSSQLServer** [!INCLUDE[msCoName](../../includes/msconame-md.md)]|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|定義警示的訊息錯誤號碼。 （通常會對應至**sysmessages**資料表中的錯誤號碼）。 如果使用嚴重性來定義警示， **message_id**為**0**或 Null。|  
|**低於**|**int**|定義警示的嚴重性層級（ **9**至**25**、 **110**、 **120**、 **130**或**140**）。|  
|**後**|**tinyint**|警示目前是否已啟用（**1**）或不是（**0**）的狀態。 不會傳送未啟用的警示。|  
|**delay_between_responses**|**int**|這個警示各次回應之間的等待期間 (以秒為單位)。|  
|**last_occurrence_date**|**int**|警示上次發生的日期。|  
|**last_occurrence_time**|**int**|警示上次發生的時間。|  
|**last_response_date**|**int**|**SQLServerAgent**服務上次回應警示的日期。|  
|**last_response_time**|**int**|**SQLServerAgent**服務上次回應警示的時間。|  
|**notification_message**|**nvarchar(512)**|附加在電子郵件或呼叫器通知來傳給操作員的選擇性附加訊息。|  
|**include_event_description**|**tinyint**|這是指是否應該將 Microsoft Windows 應用程式記錄檔的 SQL Server 錯誤描述併入通知訊息中。|  
|**database_name**|**sysname**|會因發生錯誤而引發警示的資料庫。 如果資料庫名稱是 NULL，不論是在哪裡發生錯誤，都會引發警示。|  
|**event_description_keyword**|**Nvarchar （100）**|Windows 應用程式記錄檔中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤的描述，必須如同所提供的字元順序。|  
|**occurrence_count**|**int**|警示的發生次數。|  
|**count_reset_date**|**int**|上次重設**occurrence_count**的日期。|  
|**count_reset_time**|**int**|上次重設**occurrence_count**的時間。|  
|**job_id**|**uniqueidentifier**|當回應這個警示時，所執行的作業識別碼。|  
|**job_name**|**sysname**|當回應這個警示時，所執行的作業名稱。|  
|**has_notification**|**int**|如果向一或多個操作員通知這個警示，便是非零。 這個值是下列的一或多個值 (以 OR 聯結)：<br /><br /> **1**= 有電子郵件通知<br /><br /> **2**= 具有呼叫器通知<br /><br /> **4**= 具有**net send**通知。|  
|**旗幟**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**performance_condition**|**nvarchar(512)**|如果**type**是**2**，這個資料行會顯示效能條件的定義。否則，資料行為 Null。|  
|**category_name**|**sysname**|
  [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]如果是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0，便一律是 '[Uncategorized]'。|  
|**wmi_namespace**|**sysname**|如果**type**是**3**，這個資料行會顯示 WMI 事件的命名空間。|  
|**wmi_query**|**nvarchar(512)**|如果**type**是**3**，這個資料行會顯示 WMI 事件的查詢。|  
|**type**|**int**|事件類型：<br /><br /> ****  =  1[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]個事件警示<br /><br /> ****  =  2[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]效能警示<br /><br /> **3** = WMI 事件警示|  
  
 當** \@legacy_format**為**1**時， **sp_help_alert**會產生下列結果集。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**號**|**int**|系統指派的唯一整數識別碼。|  
|**name**|**sysname**|警示名稱（例如，示範：完整的**msdb**記錄檔）。|  
|**event_source**|**Nvarchar （100）**|事件的來源。 7.0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版一律會**MSSQLServer**|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|定義警示的訊息錯誤號碼。 （通常會對應至**sysmessages**資料表中的錯誤號碼）。 如果使用嚴重性來定義警示， **message_id**為**0**或 Null。|  
|**低於**|**int**|定義警示的嚴重性層級（ **9**至**25**、 **110**、 **120**、 **130**或 1**40**）。|  
|**後**|**tinyint**|警示目前是否已啟用（**1**）或不是（**0**）的狀態。 不會傳送未啟用的警示。|  
|**delay_between_responses**|**int**|這個警示各次回應之間的等待期間 (以秒為單位)。|  
|**last_occurrence_date**|**int**|警示上次發生的日期。|  
|**last_occurrence_time**|**int**|警示上次發生的時間。|  
|**last_response_date**|**int**|**SQLServerAgent**服務上次回應警示的日期。|  
|**last_response_time**|**int**|**SQLServerAgent**服務上次回應警示的時間。|  
|**notification_message**|**nvarchar(512)**|附加在電子郵件或呼叫器通知來傳給操作員的選擇性附加訊息。|  
|**include_event_description**|**tinyint**|這是指是否應該將 Windows 應用程式記錄檔的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤描述併入通知訊息中。|  
|**database_name**|**sysname**|會因發生錯誤而引發警示的資料庫。 如果資料庫名稱是 NULL，不論是在哪裡發生錯誤，都會引發警示。|  
|**event_description_keyword**|**Nvarchar （100）**|Windows 應用程式記錄檔中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤的描述，必須如同所提供的字元順序。|  
|**occurrence_count**|**int**|警示的發生次數。|  
|**count_reset_date**|**int**|上次重設**occurrence_count**的日期。|  
|**count_reset_time**|**int**|上次重設**occurrence_count**的時間。|  
|**job_id**|**uniqueidentifier**|作業識別碼。|  
|**job_name**|**sysname**|回應這個警示所需執行的作業。|  
|**has_notification**|**int**|如果向一或多個操作員通知這個警示，便是非零。 這個值是下列的一或多個值 (以 OR 聯結)：<br /><br /> **1**= 有電子郵件通知<br /><br /> **2**= 具有呼叫器通知<br /><br /> **4**= 具有**net send**通知。|  
|**旗幟**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)].|  
|**performance_condition**|**nvarchar(512)**|如果**type**是**2**，這個資料行會顯示效能條件的定義。 如果**type**是**3**，這個資料行會顯示 WMI 事件的查詢。 否則，這個資料行是 NULL。|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]7.0 的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一律會是 '**[未分類]**'。|  
|**type**|**int**|警示類型：<br /><br /> ****  =  1[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]個事件警示<br /><br /> ****  =  2[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]效能警示<br /><br /> **3** = WMI 事件警示|  
  
## <a name="remarks"></a>備註  
 **sp_help_alert**必須從**msdb**資料庫中執行。  
  
## <a name="permissions"></a>權限  
 根據預設，**系統管理員（sysadmin** ）固定伺服器角色的成員可以執行此預存程式。 其他使用者必須被授與 **msdb** 資料庫的 **SQLAgentOperatorRole** 固定資料庫角色。  
  
 如需**SQLAgentOperatorRole**的詳細資訊，請參閱[SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
## <a name="examples"></a>範例  
 下列範例會報告 `Demo: Sev. 25 Errors` 這項警示的相關資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_update_alert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
