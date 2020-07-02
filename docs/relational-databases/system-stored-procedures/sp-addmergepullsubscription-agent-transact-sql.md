---
title: sp_addmergepullsubscription_agent （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_agent
- sp_addmergepullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addmergepullsubscription_agent
ms.assetid: a2f4b086-078d-49b5-8971-8a1e3f6a6feb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b9af4f3564c5834b856632db70bd6b12368a22c7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786236"
---
# <a name="sp_addmergepullsubscription_agent-transact-sql"></a>sp_addmergepullsubscription_agent (Transact-SQL)

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  新增一項新的代理程式作業，以便用來排程合併式發行集提取訂閱的同步處理。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addmergepullsubscription_agent [ [ @name = ] 'name' ]   
        , [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication =] 'publication'   
    [ , [ @publisher_security_mod e= ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher_encrypted_password = ] publisher_encrypted_password ]   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password= ] 'subscriber_password' ]   
    [ , [ @distributor = ] 'distributor' ]   
    [ , [ @distributor_security_mode = ] distributor_security_mode ]   
    [ , [ @distributor_login = ] 'distributor_login' ]   
    [ , [ @distributor_password = ] 'distributor_password' ]   
    [ , [ @encrypted_password = ] encrypted_password ]   
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @optional_command_line = ] 'optional_command_line' ]   
    [ , [ @merge_jobid = ] merge_jobid ]   
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]    
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @working_directory = ] 'working_directory' ]   
    [ , [ @use_ftp = ] 'use_ftp' ]   
    [ , [ @reserved = ] 'reserved' ]   
    [ , [ @use_interactive_resolver = ] 'use_interactive_resolver' ]   
    [ , [ @offloadagent = ] 'remote_agent_activation' ]   
    [ , [ @offloadserver = ] 'remote_agent_server_name']   
    [ , [ @job_name = ] 'job_name' ]   
    [ , [ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]  
    [ , [ @use_web_sync = ] use_web_sync ]  
        [ , [ @internet_url = ] 'internet_url' ]  
    [ , [ @internet_login = ] 'internet_login' ]  
        [ , [ @internet_password = ] 'internet_password' ]  
    [ , [ @internet_security_mode = ] internet_security_mode ]  
        [ , [ @internet_timeout = ] internet_timeout ]  
    [ , [ @hostname = ] 'hostname' ]  
        [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @name = ] 'name'`這是代理程式的名稱。 *name*是**sysname**，預設值是 Null。  
  
`[ @publisher = ] 'publisher'`這是發行者伺服器的名稱。 *publisher*是**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'`這是發行者資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @publisher_security_mode = ] publisher_security_mode`這是在同步處理時，連接到發行者時所使用的安全性模式。 *publisher_security_mode*是**int**，預設值是1。 如果為**0**，則指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 如果是**1**，則指定 Windows 驗證。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`這是在同步處理時，用來連接到發行者的登入。 *publisher_login*是**sysname**，預設值是 Null。  
  
`[ @publisher_password = ] 'publisher_password'`這是連接到發行者時所使用的密碼。 *publisher_password*是**sysname**，預設值是 Null。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @publisher_encrypted_password = ]publisher_encrypted_password`已不再支援設定*publisher_encrypted_password* 。 嘗試將此**位**參數設定為**1**將會導致錯誤。  
  
`[ @subscriber = ] 'subscriber'`這是訂閱者的名稱。 *訂閱者*是**sysname**，預設值是 Null。  
  
`[ @subscriber_db = ] 'subscriber_db'`這是訂閱資料庫的名稱。 *subscriber_db*是**sysname**，預設值是 Null。  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`這是在同步處理時，連接到訂閱者時所要使用的安全性模式。 *subscriber_security_mode*是**int**，預設值是1。 如果為**0**，則指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 如果是**1**，則指定 Windows 驗證。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 合併代理程式一律是利用 Windows 驗證來連接到本機訂閱者。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
`[ @subscriber_login = ] 'subscriber_login'`這是在同步處理時，用來連接訂閱者的訂閱者登入。 如果*subscriber_security_mode*設定為**0**，則需要*subscriber_login* 。 *subscriber_login*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
`[ @subscriber_password = ] 'subscriber_password'`這是驗證的訂閱者密碼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果*subscriber_security_mode*設定為**0**，則需要*subscriber_password* 。 *subscriber_password*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
`[ @distributor = ] 'distributor'`這是散發者的名稱。 散發者是**sysname**，預設*值是* *publisher*;也就是說，「發行者」也是「散發者」。  
  
`[ @distributor_security_mode = ] distributor_security_mode`這是在同步處理時，連接到散發者時所要使用的安全性模式。 *distributor_security_mode*是**int**，預設值是0。 **0**指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 **1**指定 Windows 驗證。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'`這是在同步處理時，用來連接到散發者的散發者登入。 如果*distributor_security_mode*設定為**0**，則需要*distributor_login* 。 *distributor_login*是**sysname**，預設值是 Null。  
  
`[ @distributor_password = ] 'distributor_password'`這是散發者密碼。 如果*distributor_security_mode*設定為**0**，則需要*distributor_password* 。 *distributor_password*是**sysname**，預設值是 Null。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @encrypted_password = ] encrypted_password`已不再支援設定*encrypted_password* 。 嘗試將此**位**參數設定為**1**將會導致錯誤。  
  
`[ @frequency_type = ] frequency_type`這是用來排程合併代理程式的頻率。 *frequency_type*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次性|  
|**2**|隨選|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64**|自動啟動|  
|**128**|重複執行|  
|NULL (預設值)||  
  
> [!NOTE]  
>  指定值**64**會導致合併代理程式以連續模式執行。 這對應于設定代理程式的 **-連續**參數。 如需詳細資訊，請參閱 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
`[ @frequency_interval = ] frequency_interval`合併代理程式執行的日期或天數。 *frequency_interval*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|星期日|  
|**2**|星期一|  
|**3**|Tuesday|  
|**4**|星期三|  
|**5**|Thursday|  
|**6**|星期五|  
|**7**|星期六|  
|**8**|天|  
|**9**|工作日|  
|**10**|週末|  
|NULL (預設值)||  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`這是合併代理程式的日期。 當*frequency_type*設定為**32** （每月相對）時，會使用這個參數。 *frequency_relative_interval*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|First|  
|**2**|Second|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|Last|  
|NULL (預設值)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`這是*frequency_type*所使用的迴圈因數。 *frequency_recurrence_factor*是**int**，預設值是 Null。  
  
`[ @frequency_subday = ] frequency_subday`這是在定義的期間內重新排定的頻率。 *frequency_subday*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**2**|Second|  
|**4**|Minute|  
|**8**|小時|  
|NULL (預設值)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`這是*frequency_subday*的間隔。 *frequency_subday_interval*是**int**，預設值是 Null。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`這是第一次排程合併代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*是**int**，預設值是 Null。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`這是排程停止合併代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是**int**，預設值是 Null。  
  
`[ @active_start_date = ] active_start_date`這是第一次排程合併代理程式的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，預設值是 Null。  
  
`[ @active_end_date = ] active_end_date`這是排程停止合併代理程式的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，預設值是 Null。  
  
`[ @optional_command_line = ] 'optional_command_line'`是提供給合併代理程式的選擇性命令提示字元。 *optional_command_line*是**Nvarchar （255）**，預設值是 ' '。 它可用來提供其他參數給合併代理程式，例如以下範例將預設查詢逾時值增加到 `600` 秒：  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
`[ @merge_jobid = ] merge_jobid`這是作業識別碼的輸出參數。 *merge_jobid*是**binary （16）**，預設值是 Null。  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`指定是否可以透過 Windows 同步處理管理員來同步處理訂閱。 *enabled_for_syncmgr*是**Nvarchar （5）**，預設值是 FALSE。 如果**為 false**，則表示訂閱未向同步處理管理員註冊。 若**為 true**，則會使用同步處理管理員註冊訂閱，而且可以在不啟動的情況下進行同步處理 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
`[ @ftp_address = ] 'ftp_address'`僅供回溯相容性之用。  
  
`[ @ftp_port = ] ftp_port`僅供回溯相容性之用。  
  
`[ @ftp_login = ] 'ftp_login'`僅供回溯相容性之用。  
  
`[ @ftp_password = ] 'ftp_password'`僅供回溯相容性之用。  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'`指定要從中挑選快照集檔案的位置。 *alternate_snapshot_folder*是**Nvarchar （255）**，預設值是 Null。 如果是 NULL，便會從發行者所指定的預設位置中，收取快照集檔案。  
  
`[ @working_directory = ] 'working_directory'`這是使用 FTP 來傳送快照集檔案時，用來暫時儲存發行集資料和架構檔案的工作目錄名稱。 *working_directory*是**Nvarchar （255）**，預設值是 Null。  
  
`[ @use_ftp = ] 'use_ftp'`指定使用 FTP 而不是一般通訊協定來抓取快照集。 *use_ftp*是**Nvarchar （5）**，預設值是 FALSE。  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @use_interactive_resolver = ] 'use_interactive_resolver' ]`使用互動式解析程式來解決允許互動式解決之所有發行項的衝突。 *use_interactive_resolver*是**Nvarchar （5）**，預設值是 FALSE。  
  
`[ @offloadagent = ] 'remote_agent_activation'`
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 將*remote_agent_activation*設定為**false**以外的值將會產生錯誤。  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 將*remote_agent_server_name*設定為任何非 Null 值將會產生錯誤。  
  
`[ @job_name = ] 'job_name' ]`這是現有代理程式作業的名稱。 *job_name*是**sysname**，預設值是 Null。 只有在訂閱將利用現有的作業來同步處理，而不用新建立的作業 (預設值) 時，才指定這個參數。 如果您不是**系統管理員（sysadmin** ）固定伺服器角色的成員，則在指定*job_name*時，您必須指定*job_login*和*job_password* 。  
  
`[ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]`如果要使用已篩選的資料快照集，將從中讀取快照集檔案的資料夾路徑。 *dynamic_snapshot_location*是**Nvarchar （260）**，預設值是 Null。 如需詳細資訊，請參閱＜ [參數化資料列篩選器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
`[ @use_web_sync = ] use_web_sync`表示已啟用 Web 同步處理。 *use_web_sync*是**bit**，預設值是0。 **1**指定可使用 HTTP 透過網際網路同步處理提取訂閱。  
  
`[ @internet_url = ] 'internet_url'`這是 Web 同步處理的複寫接聽程式（REPLISAPI.DLL）位置。 *internet_url*是**Nvarchar （260）**，預設值是 Null。 *internet_url*是完整的 url，格式為 `http://server.domain.com/directory/replisapi.dll` 。 如果將伺服器設定成來接聽通訊埠 80 以外的通訊埠，就必須用 `http://server.domain.com:portnumber/directory/replisapi.dll` 格式來提供通訊埠編號，其中 `portnumber` 代表通訊埠。  
  
`[ @internet_login = ] 'internet_login'`這是當使用 HTTP 基本驗證來連接到主控 Web 同步處理的 Web 服務器時，合併代理程式所使用的登入。 *internet_login*是**sysname**，預設值是 Null。  
  
`[ @internet_password = ] 'internet_password'`這是當使用 HTTP 基本驗證來連接到主控 Web 同步處理的 Web 服務器時，合併代理程式所使用的密碼。 *internet_password*是**Nvarchar （524）**，預設值是 Null。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
`[ @internet_security_mode = ] internet_security_mode`這是合併代理程式在使用 HTTPS 進行 Web 同步處理期間連接到 Web 服務器時所使用的驗證方法。 *internet_security_mode*是**int** ，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|使用基本驗證。|  
|**1** (預設值)|使用 Windows 整合式驗證。|  
  
> [!NOTE]  
>  我們建議您搭配 Web 同步處理來使用基本驗證。 若要使用 Web 同步處理，您必須建立與 Web 服務器的 TLS 連接。 如需詳細資訊，請參閱 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)。  
  
`[ @internet_timeout = ] internet_timeout`這是 Web 同步處理要求到期之前的時間長度（以秒為單位）。 *internet_timeout*是**int**，預設值是**300**秒。  
  
`[ @hostname = ] 'hostname'`當在參數化篩選的 WHERE 子句中使用這個函數時，會覆寫 HOST_NAME （）的值。 *hostname*是**sysname**，預設值是 Null。  
  
`[ @job_login = ] 'job_login'`這是用來執行代理程式之 Windows 帳戶的登入。 *job_login*是**Nvarchar （257）**，沒有預設值。 代理程式連接到訂閱者時，一律使用這個 Windows 帳戶，當利用 Windows 整合式驗證來連接到散發者和發行者時，也一律使用這個 Windows 帳戶。  
  
`[ @job_password = ] 'job_password'`這是執行代理程式之 Windows 帳戶的密碼。 *job_password*是**sysname**，沒有預設值。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 為了要有最佳的安全性，登入名稱和密碼應該在執行階段提供。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addmergepullsubscription_agent**用於合併式複寫中，並使用類似于[sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)的功能。  
  
 如需如何在執行**sp_addmergepullsubscription_agent**時正確指定安全性設定的範例，請參閱[建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_addmergepullsubscription_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
