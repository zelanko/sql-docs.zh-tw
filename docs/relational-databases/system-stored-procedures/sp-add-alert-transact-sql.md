---
description: sp_add_alert (Transact-SQL)
title: sp_add_alert (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: dd4c19f3cbe2525bf9b968e1d314767217f62129
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419312"
---
# <a name="sp_add_alert-transact-sql"></a>sp_add_alert (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @name = ] 'name'` 警示的名稱。 這個名稱會出現在回應警示所傳送的電子郵件或呼叫器訊息中。 它必須是唯一的，而且可以包含 percent (**%**) 字元。 *名稱* 是 **sysname**，沒有預設值。  
  
`[ @message_id = ] message_id` 定義警示的訊息錯誤號碼。  (通常會對應至 **sysmessages** 資料表中的錯誤號碼。 ) *message_id* 是 **int**，預設值是 **0**。 如果使用 *嚴重性* 來定義警示， *message_id* 必須是 **0** 或 Null。  
  
> [!NOTE]  
>  只有寫入 Microsoft Windows 應用程式記錄檔的 **sysmessages** 錯誤可能會導致傳送警示。  
  
`[ @severity = ] severity` 嚴重性層級 (從 **1** 到 **25** 個定義警示的) 。 任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 儲存在 **sysmessages** 資料表中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 且以指定嚴重性傳送至 Windows 應用程式記錄檔的訊息，都會導致傳送警示。 *嚴重性* 是 **int**，預設值是0。 如果使用 *message_id* 來定義警示， *嚴重性* 必須為 **0**。  
  
`[ @enabled = ] enabled` 指出警示的目前狀態。 *enabled* 是 **Tinyint**，預設值是 1 (已啟用) 。 如果是 **0**，則不會啟用警示，也不會引發警示。  
  
`[ @delay_between_responses = ] delay_between_responses` 警示回應之間的等待期間（以秒為單位）。 *delay_between_responses*是 **int**，預設值是 **0**，這表示每次出現警示時，不會在回應之間等待 (會產生回應) 。 回應可以採用下列兩種形式，或其中之一：  
  
-   利用電子郵件或呼叫器來傳送的一或多項通知。  
  
-   要執行的作業。  
  
 在設定這個值之後，便有可能防止在一小段時間內重複出現警示，因而傳送不想要的電子郵件訊息之類的情況。  
  
`[ @notification_message = ] 'notification_message'` 是在電子郵件、 **net send**或傳呼通知中傳送給操作員的選擇性額外訊息。 *notification_message* 是 **Nvarchar (512) **，預設值是 Null。 指定 *notification_message* 有助於新增特殊的附注，例如補救程式。  
  
`[ @include_event_description_in = ] include_event_description_in` 這是指是否應該在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通知訊息中包含錯誤的描述。 *include_event_description_in*是 **Tinyint**，預設值為 **5** (電子郵件和 **net send**) ，而且可以有一或多個這些值與 **or** 邏輯運算子結合。  
  
> [!IMPORTANT]
>  呼叫器和 **net send** 選項會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未來版本的 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請避免在新的開發工作中使用這些功能，並規劃修改目前使用這些功能的應用程式。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|None|  
|**1**|電子郵件|  
|**2**|呼叫器|  
|**4**|**net send**|  
  
`[ @database_name = ] 'database'` 必須發生錯誤才能引發警示的資料庫。 如果未提供 *資料庫*，則不論發生錯誤的位置為何，都會引發警示。 *資料庫* 為 **sysname**。 不允許以括號 ([ ]) 括住的名稱。 預設值是 NULL。  
  
`[ @event_description_keyword = ] 'event_description_keyword_pattern'` 錯誤描述所需的字元序列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] LIKE 運算式模式比對字元。 *event_description_keyword_pattern* 是 **Nvarchar (100) **，預設值是 Null。 此參數適用于篩選物件名稱 (例如 **% customer_table%**) 。  
  
`[ @job_id = ] job_id` 回應此警示所要執行之作業的作業識別碼。 *job_id* 是 **uniqueidentifier**，預設值是 Null。  
  
`[ @job_name = ] 'job_name'` 回應此警示所要執行的作業名稱。 *job_name*是 **sysname**，預設值是 Null。  
  
> [!NOTE]  
>  必須指定 *job_id* 或 *job_name* ，但不能同時指定兩者。  
  
`[ @raise_snmp_trap = ] raise_snmp_trap` 不是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本7.0 中執行。 *raise_snmp_trap* 是 **Tinyint**，預設值是0。  
  
`[ @performance_condition = ] 'performance_condition'` 這是以 '*itemcomparatorvalue*' 格式來表示的值。 *performance_condition* 是 **Nvarchar (512) ** ，預設值是 Null，且包含這些元素。  
  
|格式元素|描述|  
|--------------------|-----------------|  
|*Item*|計數器的效能物件、效能計數器或具名執行個體|  
|*比較*|下列其中一個運算子： >、< 或 =|  
|*值*|計數器的數值|  
  
`[ @category_name = ] 'category'` 警示類別目錄的名稱。 *category* 是 **sysname**，預設值是 Null。  
  
`[ @wmi_namespace = ] 'wmi_namespace'` 要查詢事件的 WMI 命名空間。 *wmi_namespace* 是 **sysname**，預設值是 Null。 只支援本機伺服器的命名空間。  
  
`[ @wmi_query = ] 'wmi_query'` 指定警示之 WMI 事件的查詢。 *wmi_query* 是 **Nvarchar (512) **，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_add_alert** 必須從 **msdb** 資料庫執行。  
  
 這些都是將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 應用程式產生的錯誤/訊息傳給 Windows 應用程式記錄檔的情況，因此，可能會產生警示：  
  
-   嚴重性19或更高的 **sys. 訊息** 錯誤  
  
-   利用 WITH LOG 語法叫用的任何 RAISERROR 陳述式  
  
-   使用**sp_altermessage**修改或建立的任何**sys. messages**錯誤  
  
-   使用**xp_logevent**記錄的任何事件  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理整個警示系統，建議您利用這個方式來設定警示基礎結構。  
  
 如果警示無法正常作，請檢查情況是否如下：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務正在執行。  
  
-   事件出現在 Windows 應用程式記錄檔中。  
  
-   已啟用警示。  
  
-   **xp_logevent** 產生的事件出現在 master 資料庫中。 因此，除非警示的 **\@database_name** 是 **'master'** 或 NULL，否則，**xp_logevent** 不會觸發警示。  
  
## <a name="permissions"></a>權限  
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
 [sp_add_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_altermessage &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_delete_alert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [sp_update_alert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
