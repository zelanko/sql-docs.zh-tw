---
title: sp_addmergepullsubscription_agent & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8bfa9ff0683f67a1d38aeb17bccd0cfc1443d6d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117962"
---
# <a name="spaddmergepullsubscriptionagent-transact-sql"></a>sp_addmergepullsubscription_agent (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
`[ @name = ] 'name'` 是代理程式的名稱。 *名稱*已**sysname**，預設值是 NULL。  
  
`[ @publisher = ] 'publisher'` 是發行者伺服器的名稱。 *發行者*已**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'` 是發行者資料庫的名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'` 是發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @publisher_security_mode = ] publisher_security_mode` 是同步處理時，連接到發行者時所要使用的安全性模式。 *publisher_security_mode*已**int**，預設值是 1。 如果**0**，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 如果**1**，指定 Windows 驗證。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'` 是同步處理時，連接到發行者時所要使用的登入。 *publisher_login*已**sysname**，預設值是 NULL。  
  
`[ @publisher_password = ] 'publisher_password'` 這是連接到 「 發行者 」 時用的密碼。 *publisher_password*已**sysname**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @publisher_encrypted_password = ]publisher_encrypted_password` 設定*publisher_encrypted_password*不受支援。 嘗試將這個**位元**參數來**1**會導致錯誤。  
  
`[ @subscriber = ] 'subscriber'` 是訂閱者的名稱。 *訂閱者*已**sysname**，預設值是 NULL。  
  
`[ @subscriber_db = ] 'subscriber_db'` 是訂閱資料庫的名稱。 *subscriber_db*已**sysname**，預設值是 NULL。  
  
`[ @subscriber_security_mode = ] subscriber_security_mode` 是同步處理時，連接到訂閱者時要使用的安全性模式。 *subscriber_security_mode*已**int**，預設值是 1。 如果**0**，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 如果**1**，指定 Windows 驗證。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 合併代理程式一律是利用 Windows 驗證來連接到本機訂閱者。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
`[ @subscriber_login = ] 'subscriber_login'` 這是訂閱者登入同步處理時，連接到訂閱者時使用。 *subscriber_login* ，便須*subscriber_security_mode*設定為**0**。 *subscriber_login*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
`[ @subscriber_password = ] 'subscriber_password'` 訂閱者密碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 *subscriber_password* ，便須*subscriber_security_mode*設定為**0**。 *subscriber_password*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
`[ @distributor = ] 'distributor'` 是散發者的名稱。 *散發者*已**sysname**，預設值是*發行者*; 也就是說，發行者也是 「 散發者 」。  
  
`[ @distributor_security_mode = ] distributor_security_mode` 是，連接到散發者時同步處理時所要使用的安全性模式。 *distributor_security_mode*已**int**，預設值是 0。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 **1**指定 Windows 驗證。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'` 是，連接到散發者時同步處理時所要使用的散發者登入。 *distributor_login* ，便須*distributor_security_mode*設定為**0**。 *distributor_login*已**sysname**，預設值是 NULL。  
  
`[ @distributor_password = ] 'distributor_password'` 這是散發者密碼。 *distributor_password* ，便須*distributor_security_mode*設定為**0**。 *distributor_password*已**sysname**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @encrypted_password = ] encrypted_password` 設定*encrypted_password*不受支援。 嘗試將這個**位元**參數來**1**會導致錯誤。  
  
`[ @frequency_type = ] frequency_type` 是用來排程合併代理程式的頻率。 *frequency_type*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|視需要|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64**|自動啟動|  
|**128**|重複執行|  
|NULL (預設值)||  
  
> [!NOTE]  
>  指定的值是**64**會導致合併代理程式以連續模式執行。 這對應於設定 **-連續**代理程式參數。 如需詳細資訊，請參閱 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
`[ @frequency_interval = ] frequency_interval` 執行合併代理程式的日期或天數。 *frequency_interval*已**int**，而且可以是下列值之一。  
  
|值|描述|  
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
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 這是合併代理程式的日期。 使用這個參數時*frequency_type*設為**32** （每月相對）。 *frequency_relative_interval*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
|NULL (預設值)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*已**int**，預設值是 NULL。  
  
`[ @frequency_subday = ] frequency_subday` 已定義的期間重新排程的頻率。 *frequency_subday*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (預設值)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 間隔*frequency_subday*。 *frequency_subday_interval*已**int**，預設值是 NULL。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 「 合併代理程式時第一天的排程時間，格式為 HHMMSS。 *active_start_time_of_day*已**int**，預設值是 NULL。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 是 「 合併代理程式停止的當日時間排程，格式為 HHMMSS。 *active_end_time_of_day*已**int**，預設值是 NULL。  
  
`[ @active_start_date = ] active_start_date` 排程的日期時第一個 「 合併代理程式，格式為 YYYYMMDD。 *active_start_date*已**int**，預設值是 NULL。  
  
`[ @active_end_date = ] active_end_date` 是 「 合併代理程式停止的日期排程，格式為 YYYYMMDD。 *active_end_date*已**int**，預設值是 NULL。  
  
`[ @optional_command_line = ] 'optional_command_line'` 是選擇性的命令提示字元提供給合併代理程式。 *optional_command_line*已**nvarchar(255)** ，預設值是 ' '。 它可用來提供其他參數給合併代理程式，例如以下範例將預設查詢逾時值增加到 `600` 秒：  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
`[ @merge_jobid = ] merge_jobid` 輸出參數為工作識別碼。 *merge_jobid*已**二進位 （16)** ，預設值是 NULL。  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'` 指定是否訂用帳戶可以同步處理到 Windows Synchronization Manager。 *enabled_for_syncmgr*已**nvarchar(5)** ，預設值是 FALSE。 如果**false**，訂用帳戶未註冊使用 Synchronization Manager。 如果**真**，訂用帳戶使用 Synchronization Manager 註冊，並可以同步處理，而不啟動[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
`[ @ftp_address = ] 'ftp_address'` 基於回溯相容性。  
  
`[ @ftp_port = ] ftp_port` 基於回溯相容性。  
  
`[ @ftp_login = ] 'ftp_login'` 基於回溯相容性。  
  
`[ @ftp_password = ] 'ftp_password'` 基於回溯相容性。  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'` 指定要從中收取快照集檔案的位置。 *alternate_snapshot_folder*已**nvarchar(255)** ，預設值是 NULL。 如果是 NULL，便會從發行者所指定的預設位置中，收取快照集檔案。  
  
`[ @working_directory = ] 'working_directory'` 是用來暫時儲存發行集的資料和結構描述檔案，當利用 FTP 來傳送快照集檔案的工作目錄的名稱。 *working_directory*已**nvarchar(255)** ，預設值是 NULL。  
  
`[ @use_ftp = ] 'use_ftp'` 指定利用 FTP 而不是一般通訊協定來擷取快照集。 *use_ftp*已**nvarchar(5)** ，預設值是 FALSE。  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @use_interactive_resolver = ] 'use_interactive_resolver' ]` 利用互動式解析程式來解決接受互動式解決之所有發行項的衝突。 *use_interactive_resolver*已**nvarchar(5)** ，預設值是 FALSE。  
  
`[ @offloadagent = ] 'remote_agent_activation'`
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 設定*remote_agent_activation&lt*以外的值來**false**會產生錯誤。  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 設定*remote_agent_server_name*為任何非 NULL 值會產生錯誤。  
  
`[ @job_name = ] 'job_name' ]` 是現有的代理程式作業名稱。 *job_name*已**sysname**，預設值是 NULL。 只有在訂閱將利用現有的作業來同步處理，而不用新建立的作業 (預設值) 時，才指定這個參數。 如果您不屬於**sysadmin**固定伺服器角色，您必須指定*job_login*並*job_password*當您指定*job_name*.  
  
`[ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]` 用為位置的快照集檔案會從讀取如果篩選的資料快照集資料夾的路徑。 *dynamic_snapshot_location*已**nvarchar(260)** ，預設值是 NULL。 如需詳細資訊，請參閱＜ [參數化資料列篩選器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
`[ @use_web_sync = ] use_web_sync` 指出已啟用 Web 同步處理。 *use_web_sync&lt*已**元**，預設值是 0。 **1**指定可以在使用 HTTP 透過網際網路同步處理提取訂閱。  
  
`[ @internet_url = ] 'internet_url'` 是複寫接聽程式 (REPLISAPI 位置。DLL) 的 Web 同步處理。 *應*已**nvarchar(260)** ，預設值是 NULL。 *應*是完整的 URL，格式`http://server.domain.com/directory/replisapi.dll`。 如果將伺服器設定成來接聽通訊埠 80 以外的通訊埠，就必須用 `http://server.domain.com:portnumber/directory/replisapi.dll` 格式來提供通訊埠編號，其中 `portnumber` 代表通訊埠。  
  
`[ @internet_login = ] 'internet_login'` 利用 HTTP 基本驗證連接到主控 Web 同步處理的 Web 伺服器時，會使用 「 合併代理程式的登入。 *internet_url*已**sysname**，預設值是 NULL。  
  
`[ @internet_password = ] 'internet_password'` 「 合併代理程式在連接到主控 Web 同步處理的 Web 伺服器時所用的密碼使用 HTTP 基本驗證。 *internet_login*已**nvarchar(524)** ，預設值是 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
`[ @internet_security_mode = ] internet_security_mode` Web 同步處理期間連接到 Web 伺服器時，合併代理程式所使用的驗證方法使用 HTTPS。 *internet_security_mode*已**int**而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|使用基本驗證。|  
|**1** (預設值)|使用 Windows 整合式驗證。|  
  
> [!NOTE]  
>  我們建議您搭配 Web 同步處理來使用基本驗證。 若要使用 Web 同步處理，您必須建立 Web 伺服器的 SSL 連接。 如需詳細資訊，請參閱 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)。  
  
`[ @internet_timeout = ] internet_timeout` 是以秒為單位，在 Web 同步處理要求到期之前長度。 *internet_timeout*已**int**，預設值是**300**秒。  
  
`[ @hostname = ] 'hostname'` 參數化篩選的 WHERE 子句中使用此函式時，會覆寫 host_name （） 的值。 *主機名稱*已**sysname**，預設值是 NULL。  
  
`[ @job_login = ] 'job_login'` 是執行代理程式的 Windows 帳戶的登入。 *job_login*已**nvarchar(257)** ，沒有預設值。 代理程式連接到訂閱者時，一律使用這個 Windows 帳戶，當利用 Windows 整合式驗證來連接到散發者和發行者時，也一律使用這個 Windows 帳戶。  
  
`[ @job_password = ] 'job_password'` 這是代理程式所執行的 Windows 帳戶的密碼。 *job_password*已**sysname**，沒有預設值。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 為了要有最佳的安全性，登入名稱和密碼應該在執行階段提供。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addmergepullsubscription_agent**用於合併式複寫中，並使用類似的功能[sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。  
  
 如需如何正確執行時，指定安全性設定的範例**sp_addmergepullsubscription_agent**，請參閱[建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addmergepullsubscription_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription &#40;-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
