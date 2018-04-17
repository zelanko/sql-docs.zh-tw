---
title: sp_addmergesubscription (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addmergesubscription_TSQL
- sp_addmergesubscription
helpviewer_keywords:
- sp_addmergesubscription
ms.assetid: a191d817-0132-49ff-93ca-76f13e609b38
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc7b47a0253b47e9c8e1a75131ae3003fce2ac33
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spaddmergesubscription-transact-sql"></a>sp_addmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立發送或提取合併訂閱。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addmergesubscription [ @publication= ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @subscription_type= ] 'subscription_type' ]  
    [ , [ @subscriber_type= ] 'subscriber_type' ]  
    [ , [ @subscription_priority= ] subscription_priority ]  
    [ , [ @sync_type= ] 'sync_type' ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @optional_command_line= ] 'optional_command_line' ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @enabled_for_syncmgr= ] 'enabled_for_syncmgr' ]  
    [ , [ @offloadagent= ] remote_agent_activation]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @use_interactive_resolver= ] 'use_interactive_resolver' ]  
    [ , [ @merge_job_name= ] 'merge_job_name' ]  
    [ , [ @hostname = ] 'hostname'  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication=**] **'***publication***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。 發行集必須已存在。  
  
 [  **@subscriber =**] **'***訂閱者***'**  
 這是訂閱者的名稱。 *訂閱者*是**sysname**，預設值是 NULL。  
  
 [  **@subscriber_db=**] **'***subscriber_db***'**  
 這是訂閱資料庫的名稱。 *subscriber_db*是**sysname**，預設值是 NULL。  
  
 [  **@subscription_type=**] **'***subscription_type***'**  
 這是訂閱的類型。 *subscription_type*是**nvarchar （15)**，預設值是 PUSH。 如果**發送**，加入發送訂閱，以及在散發者端新增合併代理程式。 如果**提取**，會新增提取訂閱，不會在散發者端新增合併代理程式。  
  
> [!NOTE]  
>  匿名訂閱不需要使用這個預存程序。  
  
 [  **@subscriber_type=**] **'***subscriber_type***'**  
 這是訂閱者的類型。 *subscriber_type*是**nvarchar （15)**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**本機**（預設值）|只有發行者知道的訂閱者。|  
|**全域**|所有伺服器都知道的訂閱者。|  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本中，本機訂閱稱為客訂閱，而全域訂閱稱為主訂閱  
  
 [  **@subscription_priority=**] *subscription_priority*  
 這是表示訂閱優先權的數字。 *subscription_priority*是**真實**，預設值是 NULL。 如果是本機和匿名訂閱，優先權就是 0.0。 如果是全域訂閱，優先權必須小於 100.0。  
  
 [  **@sync_type=**] **'***sync_type***'**  
 這是訂閱同步處理類型。 *sync_type*是**nvarchar （15)**，預設值是**自動**。 可以是**自動**或**無**。 如果**自動**，結構描述和發行資料表的初始資料傳送給 「 訂閱者 」 第一次。 如果**無**，便假設訂閱者端已有結構描述和初始資料已發行資料表。 一律會傳送系統資料表和資料。  
  
> [!NOTE]  
>  我們建議您不要指定值為**無**。  
  
 [  **@frequency_type=**] *frequency_type*  
 這是指出合併代理程式執行時間的值。 *frequency_type*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**4**|每日|  
|**8**|每週|  
|**10**|每月|  
|**20**|每月，相對於頻率間隔|  
|**40**|當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 啟動時|  
|NULL (預設值)||  
  
 [  **@frequency_interval=**] *frequency_interval*  
 合併代理程式的執行日期。 *frequency_interval*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|星期日|  
|**2**|星期一|  
|**3**|星期二|  
|**4**|星期三|  
|**5**|星期四|  
|**6**|星期五|  
|**7**|星期六|  
|**8**|Day|  
|**9**|工作日|  
|**10**|週末|  
|NULL (預設值)||  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 這是每月排程的頻率間隔合併出現項目。 *frequency_relative_interval*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
|NULL (預設值)||  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*是**int**，預設值是 NULL。  
  
 [  **@frequency_subday=**] *frequency_subday*  
 單位是*frequency_subday_interval*。 *frequency_subday*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (預設值)||  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 是的頻率*frequency_subday*每次合併之間發生。 *frequency_subday_interval*是**int**，預設值是 NULL。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 這是第一次排程合併代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*是**int**，預設值是 NULL。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 這是排程停止合併代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是**int**，預設值是 NULL。  
  
 [  **@active_start_date=**] *active_start_date*  
 這是第一次排程合併代理程式的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，預設值是 NULL。  
  
 [  **@active_end_date=**] *active_end_date*  
 這是排程停止合併代理程式的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，預設值是 NULL。  
  
 [  **@optional_command_line=**] **'***optional_command_line***'**  
 這是要執行的選擇性命令提示字元。 *optional_command_line*是**nvarchar （4000)**，預設值是 NULL。 這個參數用來新增擷取輸出以及將輸出儲存在檔案中的命令，或指定組態檔或屬性。  
  
 [  **@description=**] **'***描述***'**  
 這是此項合併訂閱的簡要描述。 *描述*是**nvarchar （255)**，預設值是 NULL。 這個值會顯示在複寫監視器**易記名稱**資料行，可以用來排序受監視發行集的訂閱。  
  
 [  **@enabled_for_syncmgr=**] **'***enabled_for_syncmgr***'**  
 指定是否能夠利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Synchronization Manager 來同步處理訂閱。 *enabled_for_syncmgr*是**nvarchar （5)**，預設值是 FALSE。 如果**false**，訂用帳戶未註冊使用 Synchronization Manager。 如果**true**，則與 Synchronization Manager 註冊的訂閱，且可以同步處理，而不啟動[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
 [  **@offloadagent=** ] *remote_agent_activation*  
 指定是否能從遠端啟動代理程式。 *remote_agent_activation*是**元**預設值是**0**。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。  
  
 [  **@offloadserver=** ] **'***remote_agent_server_name***'**  
 指定將用來啟用遠端代理程式之伺服器的網路名稱。 *remote_agent_server_name*是**sysname**，預設值是 NULL。  
  
 [  **@use_interactive_resolver=** ] **'***use_interactive_resolver***'**  
 可讓您以互動方式來解決接受互動式解決之所有發行項的衝突。 *use_interactive_resolver*是**nvarchar （5)**，預設值是 FALSE。  
  
 [  **@merge_job_name=** ] **'***merge_job_name***'**  
 *@merge_job_name*參數已被取代，無法設定。 *merge_job_name*是**sysname**，預設值是 NULL。  
  
 [ **@hostname**=] **'***hostname***'**  
 所傳回的值會覆寫[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)參數化篩選的 WHERE 子句中使用此函式時。 *主機名稱*是**sysname**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  基於效能的考量，我們建議您不要在參數化資料列篩選器子句中，將函數套用至資料行名稱上，如 `LEFT([MyColumn]) = SUSER_SNAME()`。 如果您使用[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)在篩選子句和覆寫了 HOST_NAME 值，它可能需要將使用的資料類型轉換[轉換](../../t-sql/functions/cast-and-convert-transact-sql.md)。 如需有關此案例之最佳做法的詳細資訊，請參閱主題＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞中的「覆寫 HOST_NAME() 值」一節。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addmergesubscription**用於合併式複寫中。  
  
 當**sp_addmergesubscription**的成員所執行**sysadmin**固定伺服器角色建立發送訂閱，合併代理程式 」 工作會隱含地建立及執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式服務帳戶。 我們建議您執行[sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) ，並指定不同代理程式專用 Windows 帳戶認證**@job_login**和 **@job_password**. 如需詳細資訊，請參閱 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergesubscription-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addmergesubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)   
 [互動式衝突解決方法](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_changemergesubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
