---
title: sp_add_alert (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_alert
- sp_add_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_alert
ms.assetid: d9b41853-e22d-4813-a79f-57efb4511f09
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4193e073f4ad4c52d6b2c7f6b82c6246107e85a1
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127068"
---
# <a name="spaddalert-transact-sql"></a>sp_add_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立警示。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_alert [ @name = ] 'name'   
     [ , [ @message_id = ] message_id ]   
     [ , [ @severity = ] severity ]   
     [ , [ @enabled = ] enabled ]  
     [ , [ @delay_between_responses = ] delay_between_responses ]   
     [ , [ @notification_message = ] 'notification_message' ]   
     [ , [ @include_event_description_in = ] include_event_description_in ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @event_description_keyword = ] 'event_description_keyword_pattern' ]   
     [ , { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ]   
     [ , [ @raise_snmp_trap = ] raise_snmp_trap ]   
     [ , [ @performance_condition = ] 'performance_condition' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@name =** ] **'**_名稱_**'**  
 警示的名稱。 這個名稱會出現在回應警示所傳送的電子郵件或呼叫器訊息中。 它必須是唯一的且可以包含百分比 (**%**) 字元。 *名稱*已**sysname**，沒有預設值。  
  
 [ **@message_id =** ] *message_id*  
 定義警示的訊息錯誤號碼。 (它通常對應於中的錯誤號碼**sysmessages**資料表。)*message_id*是**int**，預設值是**0**。 如果*嚴重性*用來定義警示*message_id*必須是**0**或 NULL。  
  
> [!NOTE]  
>  只有**sysmessages**寫入 Microsoft Windows 應用程式記錄的錯誤可能會導致傳送警示。  
  
 [  **@severity =** ]*嚴重性*  
 嚴重性層級 (從**1**透過**25**) 定義警示。 任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訊息會儲存在**sysmessages**傳送給資料表[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 應用程式記錄檔具有指定的嚴重性導致傳送警示。 *嚴重性*已**int**，預設值是 0。 如果*message_id*用來定義警示*嚴重性*必須是**0**。  
  
 [  **@enabled =** ]*啟用*  
 指出警示目前的狀態。 *已啟用*已**tinyint**，預設值是 1 （已啟用）。 如果**0**，未啟用，而且不會引發警示。  
  
 [ **@delay_between_responses =** ] *delay_between_responses*  
 這個警示各次回應之間的等待期間 (以秒為單位)。 *delay_between_responses*已**int**，預設值是**0**，這表示不等待 （每個出現的警示會產生回應） 的回應之間。 回應可以採用下列兩種形式，或其中之一：  
  
-   利用電子郵件或呼叫器來傳送的一或多項通知。  
  
-   要執行的作業。  
  
 在設定這個值之後，便有可能防止在一小段時間內重複出現警示，因而傳送不想要的電子郵件訊息之類的情況。  
  
 [  **@notification_message =** ] **'**_notification_message_**'**  
 這是選擇性的附加訊息的電子郵件傳送給操作員**網路傳送**，或呼叫器通知。 *notification_message*已**nvarchar(512)**，預設值是 NULL。 指定*notification_message*適合用來加入矯正程序之類的特殊附註。  
  
 [ **@include_event_description_in =** ] *include_event_description_in*  
 這是指通知訊息是否應該包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤的描述。 *include_event_description_in*已**tinyint**，預設值是**5** (電子郵件和**網路傳送**)，並可以有一個或多個這些值結合**或**邏輯運算子。  
  
> [!IMPORTANT]
>  呼叫器和 **net send** 選項會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未來版本的 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請避免在新的開發工作中使用這些功能，並規劃修改目前使用這些功能的應用程式。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|None|  
|**1**|電子郵件|  
|**2**|呼叫器|  
|**4**|**net send**|  
  
 [  **@database_name =** ] **'**_資料庫_**'**  
 會因發生錯誤而引發警示的資料庫。 如果*資料庫*未提供，不論是在發生錯誤，都會引發警示。 *資料庫*已**sysname**。 不允許以括號 ([ ]) 括住的名稱。 預設值是 NULL。  
  
 [  **@event_description_keyword =** ] **'**_event_description_keyword_pattern_**'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤的描述必須符合的字元序列。 您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] LIKE 運算式模式比對字元。 *event_description_keyword_pattern*已**nvarchar(100)**，預設值是 NULL。 此參數可用於篩選的物件名稱 (例如 **%customer_table%**)。  
  
 [ **@job_id =** ] *job_id*  
 當回應這個警示時，所執行之作業的作業識別碼。 *job_id*已**uniqueidentifier**，預設值是 NULL。  
  
 [  **@job_name =** ] **'**_job_name_**'**  
 當回應這個警示時，所執行的作業名稱。 *job_name*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  任一*job_id*或是*job_name*必須指定，但不可同時指定兩者。  
  
 [ **@raise_snmp_trap =** ] *raise_snmp_trap*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 版沒有這項實作。 *raise_snmp_trap*已**tinyint**，預設值是 0。  
  
 [  **@performance_condition =** ] **'**_performance_condition_**'**  
 表示格式的值 '*itemcomparatorvalue*'。 *performance_condition*已**nvarchar(512)** 預設值是 NULL，這些元素組成。  
  
|格式元素|描述|  
|--------------------|-----------------|  
|*項目*|計數器的效能物件、效能計數器或具名執行個體|  
|*Comparator*|它是下列運算子之一：>、< 或 =|  
|*值*|計數器的數值|  
  
 [  **@category_name =** ] **'**_分類_**'**  
 警示類別目錄的名稱。 *類別目錄*已**sysname**，預設值是 NULL。  
  
 [ **@wmi_namespace** =] **'**_wmi_namespace_**'**  
 要查詢事件的 WMI 命名空間。 *wmi_namespace*已**sysname**，預設值是 NULL。 只支援本機伺服器的命名空間。  
  
 [ **@wmi_query** =] **'**_wmi_query_**'**  
 指定警示之 WMI 事件的查詢。 *wmi_query*已**nvarchar(512)**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_add_alert**必須從執行**msdb**資料庫。  
  
 這些都是將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 應用程式產生的錯誤/訊息傳給 Windows 應用程式記錄檔的情況，因此，可能會產生警示：  
  
-   嚴重性 19 或更高**sys.messages**錯誤  
  
-   利用 WITH LOG 語法叫用的任何 RAISERROR 陳述式  
  
-   任何**sys.messages**錯誤修改或建立使用**sp_altermessage**  
  
-   使用記錄任何事件**xp_logevent**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理整個警示系統，建議您利用這個方式來設定警示基礎結構。  
  
 如果警示無法正常作，請檢查情況是否如下：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務正在執行。  
  
-   事件出現在 Windows 應用程式記錄檔中。  
  
-   已啟用警示。  
  
-   **xp_logevent** 產生的事件出現在 master 資料庫中。 因此，除非警示的 **xp_logevent** 是 **@database_name** 或 NULL，否則， **xp_logevent** 不會觸發警示。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行 **sp_add_alert**。  
  
## <a name="examples"></a>範例  
 下列範例會在引發時加入執行 `Back up the AdventureWorks2012 Database` 作業的警示 (Test Alert)。  
  
> [!NOTE]  
>  這個範例假設訊息 55001 和 `Back up the AdventureWorks2012 Database` 作業已經存在。 這個範例只供說明。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_alert  
    @name = N'Test Alert',  
    @message_id = 55001,   
   @severity = 0,   
   @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
   @job_name = N'Back up the AdventureWorks2012 Database' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_notification &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_altermessage &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_delete_alert &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [sp_update_alert &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
