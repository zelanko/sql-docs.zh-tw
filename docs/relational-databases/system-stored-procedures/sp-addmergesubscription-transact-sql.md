---
title: sp_addmergesubscription （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergesubscription_TSQL
- sp_addmergesubscription
helpviewer_keywords:
- sp_addmergesubscription
ms.assetid: a191d817-0132-49ff-93ca-76f13e609b38
author: stevestein
ms.author: sstein
ms.openlocfilehash: b501a2c06a6d9e8e3573ef5d5814c3318c4e623b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68769129"
---
# <a name="sp_addmergesubscription-transact-sql"></a>sp_addmergesubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。 發行集必須已存在。  
  
`[ @subscriber = ] 'subscriber'`這是訂閱者的名稱。 *訂閱者*是**sysname**，預設值是 Null。  
  
`[ @subscriber_db = ] 'subscriber_db'`這是訂閱資料庫的名稱。 *subscriber_db*是**sysname**，預設值是 Null。  
  
`[ @subscription_type = ] 'subscription_type'`這是訂用帳戶的類型。 *subscription_type*是**Nvarchar （15）**，預設值是 PUSH。 如果**推送**，則會加入發送訂閱，並在散發者端加入合併代理程式。 如果是**pull**，則會加入提取訂閱，而不會在散發者端加入合併代理程式。  
  
> [!NOTE]  
>  匿名訂閱不需要使用這個預存程序。  
  
`[ @subscriber_type = ] 'subscriber_type'`這是訂閱者的類型。 *subscriber_type*是**Nvarchar （15）**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**本機**（預設值）|只有發行者知道的訂閱者。|  
|**全域性**|所有伺服器都知道的訂閱者。|  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本中，本機訂閱稱為客訂閱，而全域訂閱稱為主訂閱  
  
`[ @subscription_priority = ] subscription_priority`這是表示訂閱優先權的數位。 *subscription_priority*是**real**，預設值是 Null。 如果是本機和匿名訂閱，優先權就是 0.0。 如果是全域訂閱，優先權必須小於 100.0。  
  
`[ @sync_type = ] 'sync_type'`這是訂閱同步處理類型。 *sync_type*是**Nvarchar （15）**，預設值是**automatic**。 可以是 [**自動**] 或 [**無**]。 如果是**自動**，則會先將已發行資料表的架構和初始資料傳送給訂閱者。 如果**沒有**，則假設訂閱者已有發行資料表的架構和初始資料。 一律會傳送系統資料表和資料。  
  
> [!NOTE]  
>  我們建議您不要將值指定為**none**。  
  
`[ @frequency_type = ] frequency_type`這是一個值，表示何時會執行合併代理程式。 *frequency_type*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**4**|每天|  
|**8**|每週|  
|**十大**|每月|  
|**20**|每月，相對於頻率間隔|  
|**40**|當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 啟動時|  
|NULL (預設值)||  
  
`[ @frequency_interval = ] frequency_interval`合併代理程式執行的日期或天數。 *frequency_interval*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|星期日|  
|**2**|星期一|  
|**第**|Tuesday|  
|**4**|Wednesday|  
|**第**|Thursday|  
|**6**|星期五|  
|**utf-7**|星期六|  
|**8**|Day|  
|**9**|工作日|  
|**十大**|週末|  
|NULL (預設值)||  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`這是每個月中排程的頻率間隔合併出現次數。 *frequency_relative_interval*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|第一頁|  
|**2**|秒|  
|**4**|第三個|  
|**8**|第四個|  
|**1600**|最後一頁|  
|NULL (預設值)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`這是*frequency_type*所使用的迴圈因數。 *frequency_recurrence_factor*是**int**，預設值是 Null。  
  
`[ @frequency_subday = ] frequency_subday`這是*frequency_subday_interval*的單位。 *frequency_subday*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**2**|秒|  
|**4**|分鐘|  
|**8**|小時|  
|NULL (預設值)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`這是每次合併之間*frequency_subday*發生的頻率。 *frequency_subday_interval*是**int**，預設值是 Null。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`這是第一次排程合併代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*是**int**，預設值是 Null。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`這是排程停止合併代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是**int**，預設值是 Null。  
  
`[ @active_start_date = ] active_start_date`這是第一次排程合併代理程式的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，預設值是 Null。  
  
`[ @active_end_date = ] active_end_date`這是排程停止合併代理程式的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，預設值是 Null。  
  
`[ @optional_command_line = ] 'optional_command_line'`這是要執行的選擇性命令提示字元。 *optional_command_line*是**Nvarchar （4000）**，預設值是 Null。 這個參數用來新增擷取輸出以及將輸出儲存在檔案中的命令，或指定組態檔或屬性。  
  
`[ @description = ] 'description'`這是此合併訂閱的簡要描述。 *description*是**Nvarchar （255）**，預設值是 Null。 複寫監視器會在 [**易記名稱**] 資料行中顯示這個值，這可以用來排序受監視發行集的訂閱。  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`指定是否可以透過[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 同步處理管理員來同步處理訂閱。 *enabled_for_syncmgr*是**Nvarchar （5）**，預設值是 FALSE。 如果**為 false**，則表示訂閱未向同步處理管理員註冊。 若**為 true**，則會使用同步處理管理員註冊訂閱，而且可以在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]不啟動的情況下進行同步處理。  
  
`[ @offloadagent = ] remote_agent_activation`指定可以從遠端啟用代理程式。 *remote_agent_activation*是**bit** ，預設值是**0**。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。  
  
`[ @offloadserver = ] 'remote_agent_server_name'`指定要用於遠端代理程式啟用的伺服器網路名稱。 *remote_agent_server_name*是**sysname**，預設值是 Null。  
  
`[ @use_interactive_resolver = ] 'use_interactive_resolver'`允許針對允許互動式解決的所有發行項，以互動方式解決衝突。 *use_interactive_resolver*是**Nvarchar （5）**，預設值是 FALSE。  
  
`[ @merge_job_name = ] 'merge_job_name'`Merge_job_name 參數已被取代，無法設定。 * \@ * *merge_job_name*是**sysname**，預設值是 Null。  
  
`[ @hostname = ] 'hostname'`當在參數化篩選的 WHERE 子句中使用這個函數時，覆寫[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)所傳回的值。 *Hostname*是**sysname**，預設值是 Null。  
  
> [!IMPORTANT]  
>  基於效能的考量，我們建議您不要在參數化資料列篩選器子句中，將函數套用至資料行名稱上，如 `LEFT([MyColumn]) = SUSER_SNAME()`。 如果您在篩選子句中使用[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) ，並覆寫 HOST_NAME 值，則可能需要使用[convert](../../t-sql/functions/cast-and-convert-transact-sql.md)來轉換資料類型。 如需有關此案例之最佳做法的詳細資訊，請參閱主題＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞中的「覆寫 HOST_NAME() 值」一節。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addmergesubscription**用於合併式複寫中。  
  
 當**sp_addmergesubscription**由**系統管理員（sysadmin** ）固定伺服器角色的成員執行時，若要建立發送訂閱，合併代理程式作業會以隱含方式建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並在 Agent 服務帳戶之下執行。 我們建議您執行[sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) ，並指定不同的代理程式特定 Windows 帳戶的認證，以供** \@job_login**和** \@job_password**。 如需詳細資訊，請參閱 [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergesubscription-_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_addmergesubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [互動式衝突解決方法](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_changemergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
