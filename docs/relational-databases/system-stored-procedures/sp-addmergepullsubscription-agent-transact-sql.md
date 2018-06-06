---
title: sp_addmergepullsubscription_agent (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_addmergepullsubscription_agent
- sp_addmergepullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addmergepullsubscription_agent
ms.assetid: a2f4b086-078d-49b5-8971-8a1e3f6a6feb
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a728fc2fff24001355a59a9df1f9701d83bd75fb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
 [ **@name =** ] **'***name***'**  
 這是代理程式的名稱。 *名稱*是**sysname**，預設值是 NULL。  
  
 [  **@publisher =** ] **'***發行者***'**  
 這是發行者伺服器的名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [  **@publisher_db =** ] **'***publisher_db***'**  
 這是發行者資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
 [ **@publication =** ] **'***publication***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@publisher_security_mode =** ] *publisher_security_mode*  
 這是進行同步處理時，連接到發行者時使用的安全性模式。 *publisher_security_mode*是**int**，預設值是 1。 如果**0**，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 如果**1**，指定 Windows 驗證。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@publisher_login =** ] **'***publisher_login***'**  
 這是在同步處理時，用來連接發行者的登入。 *publisher_login*是**sysname**，預設值是 NULL。  
  
 [  **@publisher_password =** ] **'***publisher_password***'**  
 這是連接到發行者時所用的密碼。 *publisher_password*是**sysname**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
 [  **@publisher_encrypted_password =** ]*publisher_encrypted_password*  
 設定*publisher_encrypted_password*不再支援。 嘗試將這個**元**參數**1**會導致錯誤。  
  
 [  **@subscriber =** ] **'***訂閱者***'**  
 這是訂閱者的名稱。 *訂閱者*是**sysname**，預設值是 NULL。  
  
 [  **@subscriber_db =** ] **'***subscriber_db***'**  
 這是訂閱資料庫的名稱。 *subscriber_db*是**sysname**，預設值是 NULL。  
  
 [  **@subscriber_security_mode =** ] *subscriber_security_mode*  
 這是進行同步處理時，連接到訂閱者時使用的安全性模式。 *subscriber_security_mode*是**int**，預設值是 1。 如果**0**，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 如果**1**，指定 Windows 驗證。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 合併代理程式一律是利用 Windows 驗證來連接到本機訂閱者。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
 [  **@subscriber_login =** ] **'***subscriber_login***'**  
 這是進行同步處理時，連接到訂閱者時使用的訂閱者登入。 *subscriber_login*時需要*subscriber_security_mode*設**0**。 *subscriber_login*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
 [  **@subscriber_password =** ] **'***subscriber_password***'**  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的訂閱者密碼。 *subscriber_password*時需要*subscriber_security_mode*設**0**。 *subscriber_password*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
 [  **@distributor =** ] **'***散發者***'**  
 這是散發者的名稱。 *散發者*是**sysname**，預設值是*發行者*; 也就是說，發行者也是 「 散發者 」。  
  
 [  **@distributor_security_mode =** ] *distributor_security_mode*  
 這是進行同步處理時，連接到散發者時使用的安全性模式。 *distributor_security_mode*是**int**，預設值是 0。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 **1**指定 Windows 驗證。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@distributor_login =** ] **'***distributor_login***'**  
 這是進行同步處理時，連接到散發者時使用的散發者登入。 *distributor_login*時需要*distributor_security_mode*設**0**。 *distributor_login*是**sysname**，預設值是 NULL。  
  
 [  **@distributor_password =** ] **'***distributor_password***'**  
 這是散發者密碼。 *distributor_password*時需要*distributor_security_mode*設**0**。 *distributor_password*是**sysname**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
 [  **@encrypted_password =** ] *encrypted_password*  
 設定*encrypted_password*不再支援。 嘗試將這個**元**參數**1**會導致錯誤。  
  
 [  **@frequency_type =** ] *frequency_type*  
 這是排程合併代理程式所採用的頻率。 *frequency_type*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
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
>  指定的值是**64**會導致合併代理程式，以連續模式執行。 這會對應至設定 **-連續**代理程式的參數。 如需詳細資訊，請參閱 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
 [  **@frequency_interval =** ] *frequency_interval*  
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
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 這是合併代理程式的日期。 使用這個參數時*frequency_type*設**32** （每月相對）。 *frequency_relative_interval*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
|NULL (預設值)||  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*是**int**，預設值是 NULL。  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 這是在定義的期間內，重新排程的頻率。 *frequency_subday*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (預設值)||  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 間隔*frequency_subday*。 *frequency_subday_interval*是**int**，預設值是 NULL。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 這是第一次排程合併代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*是**int**，預設值是 NULL。  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 這是排程停止合併代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是**int**，預設值是 NULL。  
  
 [ **@active_start_date =** ] *active_start_date*  
 這是第一次排程合併代理程式的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，預設值是 NULL。  
  
 [ **@active_end_date =** ] *active_end_date*  
 這是排程停止合併代理程式的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，預設值是 NULL。  
  
 [  **@optional_command_line =** ] **'***optional_command_line***'**  
 這是提供給合併代理程式的選擇性命令提示字元。 *optional_command_line*是**nvarchar （255)**，預設值是 ' '。 它可用來提供其他參數給合併代理程式，例如以下範例將預設查詢逾時值增加到 `600` 秒：  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
 [  **@merge_jobid =** ] *merge_jobid*  
 這是作業識別碼的輸出參數。 *merge_jobid*是**binary （16)**，預設值是 NULL。  
  
 [  **@enabled_for_syncmgr =** ] **'***enabled_for_syncmgr***'**  
 指定是否能夠利用 Windows Synchronization Manager 來同步處理訂閱。 *enabled_for_syncmgr*是**nvarchar （5)**，預設值是 FALSE。 如果**false**，訂用帳戶未註冊使用 Synchronization Manager。 如果**true**，則與 Synchronization Manager 註冊的訂閱，且可以同步處理，而不啟動[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
 [  **@ftp_address =** ] **'***ftp_address***'**  
 只是為了與舊版相容。  
  
 [  **@ftp_port =** ] *ftp_port*  
 只是為了與舊版相容。  
  
 [  **@ftp_login =** ] **'***ftp_login***'**  
 只是為了與舊版相容。  
  
 [  **@ftp_password =** ] **'***ftp_password***'**  
 只是為了與舊版相容。  
  
 [  **@alt_snapshot_folder =** ] **'***alternate_snapshot_folder***'**  
 指定從中收取快照集檔案的位置。 *alternate_snapshot_folder*是**nvarchar （255)**，預設值是 NULL。 如果是 NULL，便會從發行者所指定的預設位置中，收取快照集檔案。  
  
 [  **@working_directory =** ] **'***working_directory***'**  
 這是在利用 FTP 來傳送快照集檔案時，用來暫時儲存發行集的資料檔和結構描述檔的工作目錄名稱。 *working_directory*是**nvarchar （255)**，預設值是 NULL。  
  
 [  **@use_ftp =** ] **'***use_ftp***'**  
 指定利用 FTP 而不是一般通訊協定來擷取快照集。 *use_ftp*是**nvarchar （5)**，預設值是 FALSE。  
  
 [  **@reserved =** ] **'***保留***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@use_interactive_resolver =** ] **'***use_interactive_resolver***'** ]  
 利用互動式解析程式來解決接受互動式解決之所有發行項的衝突。 *use_interactive_resolver*是**nvarchar （5)**，預設值是 FALSE。  
  
 [  **@offloadagent =** ] **'***remote_agent_activation***'**  
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 設定*remote_agent_activation*以外的值來**false**會產生錯誤。  
  
 [  **@offloadserver =** ] **'***remote_agent_server_name***'**  
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 設定*remote_agent_server_name*為任何非 NULL 值會產生錯誤。  
  
 [  **@job_name =** ] **'***job_name***'** ]  
 這是現有散發代理程式作業的名稱。 *job_name*是**sysname**，預設值是 NULL。 只有在訂閱將利用現有的作業來同步處理，而不用新建立的作業 (預設值) 時，才指定這個參數。 如果您不屬於**sysadmin**固定伺服器角色，您必須指定*job_login*和*job_password*當您指定*job_name*.  
  
 [  **@dynamic_snapshot_location =** ] **'***dynamic_snapshot_location***'** ]  
 如果將使用已篩選資料快照集，這便是要讀取的快照集檔案的資料夾路徑 *dynamic_snapshot_location*是**nvarchar （260)**，預設值是 NULL。 如需詳細資訊，請參閱 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。  
  
 [  **@use_web_sync =** ] *use_web_sync*  
 指出 Web 同步處理已啟用。 *use_web_sync*是**元**，預設值是 0。 **1**指定可以在使用 HTTP 透過網際網路同步處理提取訂閱。  
  
 [  **@internet_url =** ] **'***應***'**  
 這是複寫接聽程式 (REPLISAPI.DLL) 的 Web 同步處理位置。 *應*是**nvarchar （260)**，預設值是 NULL。 *應*是完整的 URL，格式`http://server.domain.com/directory/replisapi.dll`。 如果將伺服器設定成來接聽通訊埠 80 以外的通訊埠，就必須用 `http://server.domain.com:portnumber/directory/replisapi.dll` 格式來提供通訊埠編號，其中 `portnumber` 代表通訊埠。  
  
 [  **@internet_login =** ] **'***internet_url***'**  
 這是在利用 HTTP 基本驗證來連接到主控 Web 同步處理的 Web 伺服器時，合併代理程式所用的登入。 *internet_url*是**sysname**，預設值是 NULL。  
  
 [  **@internet_password =** ] **'***internet_login***'**  
 這是在利用 HTTP 基本驗證來連接到主控 Web 同步處理的 Web 伺服器時，合併代理程式所用的密碼。 *internet_login*是**nvarchar （524)**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [  **@internet_security_mode =** ] *internet_security_mode*  
 這是在利用 HTTPS 進行的 Web 同步處理期間，合併代理程式用來連接到 Web 伺服器的驗證方法。 *internet_security_mode*是**int**而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**0**|使用基本驗證。|  
|**1** (預設值)|使用 Windows 整合式驗證。|  
  
> [!NOTE]  
>  我們建議您搭配 Web 同步處理來使用基本驗證。 若要使用 Web 同步處理，您必須建立 Web 伺服器的 SSL 連接。 如需詳細資訊，請參閱[設定 Web 同步處理](../../relational-databases/replication/configure-web-synchronization.md)。  
  
 [  **@internet_timeout =** ] *internet_timeout*  
 這是 Web 同步處理要求到期之前的時間長度 (以秒為單位)。 *internet_timeout*是**int**，預設值是**300**秒。  
  
 [  **@hostname =** ] **'***hostname***'**  
 當在參數化篩選的 WHERE 子句中使用這個函數時，覆寫 HOST_NAME() 的值。 *主機名稱*是**sysname**，預設值是 NULL。  
  
 [  **@job_login =** ] **'***job_login***'**  
 這是用來執行代理程式之 Windows 帳戶的登入。 *job_login*是**nvarchar （257)**，沒有預設值。 代理程式連接到訂閱者時，一律使用這個 Windows 帳戶，當利用 Windows 整合式驗證來連接到散發者和發行者時，也一律使用這個 Windows 帳戶。  
  
 [  **@job_password =** ] **'***job_password***'**  
 這是用來執行代理程式之 Windows 帳戶的密碼。 *job_password*是**sysname**，沒有預設值。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 為了要有最佳的安全性，登入名稱和密碼應該在執行階段提供。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addmergepullsubscription_agent**用於合併式複寫中，並使用類似的功能[sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。  
  
 如需如何執行時，正確地指定安全性設定的範例**sp_addmergepullsubscription_agent**，請參閱[Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addmergepullsubscription_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
