---
title: sp_addmergepullsubscription_agent(轉算 SQL) |微軟文件
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
ms.openlocfilehash: 07cc514d615c86a90dcf37fbd4748c3ab1776f06
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528972"
---
# <a name="sp_addmergepullsubscription_agent-transact-sql"></a>sp_addmergepullsubscription_agent (Transact-SQL)

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @name = ] 'name'`是代理的名稱。 *名稱*是**sysname,** 預設值為 NULL。  
  
`[ @publisher = ] 'publisher'`是發佈伺服器的名稱。 *發行者*是**sysname,** 沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'`是發佈者資料庫的名稱。 *publisher_db*是**系統名稱**,沒有預設值。  
  
`[ @publication = ] 'publication'`是發佈的名稱。 *發佈*是**sysname,** 沒有預設值。  
  
`[ @publisher_security_mode = ] publisher_security_mode`是同步時連接到發佈伺服器時使用的安全模式。 *publisher_security_mode*為**int,** 預設值為 1。 如果**為** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 0 ,則指定身份驗證。 如果**為 1**,則指定 Windows 身份驗證。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`是同步時連接到發佈伺服器時使用的登錄名。 *publisher_login*是**系統名稱**,預設值為 NULL。  
  
`[ @publisher_password = ] 'publisher_password'`是連接到發佈伺服器時使用的密碼。 *publisher_password*是**系統名稱**,預設值為 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @publisher_encrypted_password = ]publisher_encrypted_password`不再支援設置*publisher_encrypted_password。* 嘗試將此**位**參數設置為**1**將導致錯誤。  
  
`[ @subscriber = ] 'subscriber'`是訂閱者的名稱。 *訂戶*是**sysname,** 預設值為 NULL。  
  
`[ @subscriber_db = ] 'subscriber_db'`是訂閱資料庫的名稱。 *subscriber_db*是**系統名稱**,預設值為 NULL。  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`是同步時連接到訂閱伺服器時使用的安全模式。 *subscriber_security_mode* **為 int,** 預設值為 1。 如果**為** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 0 ,則指定身份驗證。 如果**為 1**,則指定 Windows 身份驗證。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 合併代理程式一律是利用 Windows 驗證來連接到本機訂閱者。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
`[ @subscriber_login = ] 'subscriber_login'`在同步時連接到訂閱伺服器時使用的訂閱伺服器登錄名是。 如果subscriber_security_mode設置為**0,** 則需要*subscriber_login。* *subscriber_security_mode* *subscriber_login*是**系統名稱**,預設值為 NULL。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
`[ @subscriber_password = ] 'subscriber_password'`是身份驗證的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者密碼。 如果subscriber_security_mode設置為**0,** 則需要*subscriber_password。* *subscriber_security_mode* *subscriber_password*是**sysname,** 預設值為 NULL。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
`[ @distributor = ] 'distributor'`是分發伺服器的名稱。 *分發伺服器*是**sysname,** 預設為*發佈者*;也就是說,發佈者也是分發伺服器。  
  
`[ @distributor_security_mode = ] distributor_security_mode`是同步時連接到分發伺服器時使用的安全模式。 *distributor_security_mode* **為 int,** 預設值為 0。 **0**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定身份驗證。 **1**指定 Windows 身份驗證。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'`在同步時連接到分發伺服器時使用的分發伺服器登錄名是。 如果*distributor_security_mode*設置為**0,** 則需要*distributor_login。* *distributor_login*是**系統名稱**,預設值為 NULL。  
  
`[ @distributor_password = ] 'distributor_password'`是分發伺服器密碼。 如果*distributor_security_mode*設置為**0,** 則需要*distributor_password。* *distributor_password*是**系統名稱**,預設值為 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @encrypted_password = ] encrypted_password`不再支援設置*encrypted_password。* 嘗試將此**位**參數設置為**1**將導致錯誤。  
  
`[ @frequency_type = ] frequency_type`是計劃合併代理的頻率。 *frequency_type*是**int,** 可以是以下值之一。  
  
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
>  指定值**64**會導致合併代理在連續模式下運行。 這對應於為代理設置 **-連續**參數。 如需詳細資訊，請參閱 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
`[ @frequency_interval = ] frequency_interval`合併代理運行的天數。 *frequency_interval*是**int,** 可以是這些值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|星期日|  
|**2**|星期一|  
|**3**|Tuesday|  
|**4**|星期三|  
|**5**|Thursday|  
|**6**|星期五|  
|**7**|星期六|  
|**8**|Day|  
|**9**|工作日|  
|**10**|週末|  
|NULL (預設值)||  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`是合併代理的日期。 當*frequency_type*設置為**32(** 每月相對)時,使用此參數。 *frequency_relative_interval*是**int,** 可以是這些值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|First|  
|**2**|Second|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|Last|  
|NULL (預設值)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`是*frequency_type*使用的復發係數。 *frequency_recurrence_factor*為**int,** 預設值為 NULL。  
  
`[ @frequency_subday = ] frequency_subday`是在定義的時間段內重新計劃的頻率。 *frequency_subday* **是 int,** 可以是這些值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (預設值)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`是*frequency_subday*的間隔。 *frequency_subday_interval* **為 int,** 預設值為 NULL。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`是首次計劃合併代理(格式化為 HHMMSS)的一天中的時間。 *active_start_time_of_day* **為 int,** 預設值為 NULL。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`是合併代理停止計畫的時間,格式化為 HHMMSS。 *active_end_time_of_day* **為 int,** 預設值為 NULL。  
  
`[ @active_start_date = ] active_start_date`是首次計劃合併代理的日期,格式化為 YYYYMMD。 *active_start_date* **為 int,** 預設值為 NULL。  
  
`[ @active_end_date = ] active_end_date`是合併代理停止計畫的日期,格式化為 YYYYMMDD。 *active_end_date***為 int,** 預設值為 NULL。  
  
`[ @optional_command_line = ] 'optional_command_line'`是提供給合併代理的可選命令提示符。 *optional_command_line*是**nvarchar(255),** 預設值為''。 它可用來提供其他參數給合併代理程式，例如以下範例將預設查詢逾時值增加到 `600` 秒：  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
`[ @merge_jobid = ] merge_jobid`是作業ID的輸出參數。 *merge_jobid*是**二進位 (16),** 預設值為 NULL。  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`指定是否可以通過 Windows 同步管理器同步訂閱。 *enabled_for_syncmgr*是**nvarchar(5),** 預設值為 FALSE。 如果**為 false,** 則訂閱不會註冊到同步管理員。 如果**為 true,** 則訂閱在同步管理器中註冊[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)],無需啟動 即可同步。  
  
`[ @ftp_address = ] 'ftp_address'`僅適用於向後相容性。  
  
`[ @ftp_port = ] ftp_port`僅適用於向後相容性。  
  
`[ @ftp_login = ] 'ftp_login'`僅適用於向後相容性。  
  
`[ @ftp_password = ] 'ftp_password'`僅適用於向後相容性。  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'`指定從中拾取快照檔的位置。 *alternate_snapshot_folder*是**nvarchar (255),** 預設值為 NULL。 如果是 NULL，便會從發行者所指定的預設位置中，收取快照集檔案。  
  
`[ @working_directory = ] 'working_directory'`是用於在 FTP 傳輸快照檔時臨時存儲發佈數據和架構檔的工作目錄的名稱。 *working_directory*是**nvarchar (255),** 預設值為 NULL。  
  
`[ @use_ftp = ] 'use_ftp'`指定使用 FTP 而不是典型的協議來檢索快照。 *use_ftp*是**nvarchar(5),** 預設值為 FALSE。  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @use_interactive_resolver = ] 'use_interactive_resolver' ]`使用互動式解析器解決所有允許互動式解析的文章的衝突。 *use_interactive_resolver*是**nvarchar(5),** 預設值為 FALSE。  
  
`[ @offloadagent = ] 'remote_agent_activation'`
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 將*remote_agent_activation*設定為**false**以外的值將生成錯誤。  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 將*remote_agent_server_name*設定為任何非 NULL 值都會產生錯誤。  
  
`[ @job_name = ] 'job_name' ]`是現有代理作業的名稱。 *job_name*是**sysname,** 預設值為 NULL。 只有在訂閱將利用現有的作業來同步處理，而不用新建立的作業 (預設值) 時，才指定這個參數。 如果您不是**sysadmin**固定伺服器角色的成員,則必須在指定*job_name*時指定*job_login*和*job_password。*  
  
`[ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]`如果要使用篩選的數據快照,則從其中讀取快照檔的資料夾的路徑。 *dynamic_snapshot_location*是**nvarchar (260),** 預設值為 NULL。 如需詳細資訊，請參閱＜ [參數化資料列篩選器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
`[ @use_web_sync = ] use_web_sync`指示啟用了 Web 同步。 *use_web_sync***位,** 預設值為 0。 **1**指定拉取訂閱可以使用 HTTP 在網路上同步。  
  
`[ @internet_url = ] 'internet_url'`是複製偵聽器的位置 (REPLISAPI)。用於 Web 同步的 DLL)。 *internet_url*是**nvarchar(260),** 預設值為 NULL。 *internet_url*是一個完全合格的網址`http://server.domain.com/directory/replisapi.dll`,格式為 。 如果將伺服器設定成來接聽通訊埠 80 以外的通訊埠，就必須用 `http://server.domain.com:portnumber/directory/replisapi.dll` 格式來提供通訊埠編號，其中 `portnumber` 代表通訊埠。  
  
`[ @internet_login = ] 'internet_login'`是合併代理使用 HTTP 基本身份驗證連接到承載 Web 同步的 Web 伺服器時使用的登錄名。 *internet_login*是**系統名稱**,預設值為 NULL。  
  
`[ @internet_password = ] 'internet_password'`是合併代理使用 HTTP 基本身份驗證連接到承載 Web 同步的 Web 伺服器時使用的密碼。 *internet_password*是**nvarchar (524),** 預設值為 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
`[ @internet_security_mode = ] internet_security_mode`是合併代理在使用 HTTPS 在 Web 同步期間連接到 Web 伺服器時使用的身份驗證方法。 *internet_security_mode*是**int,** 可以是這些值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|使用基本驗證。|  
|**1** (預設值)|使用 Windows 整合式驗證。|  
  
> [!NOTE]  
>  我們建議您搭配 Web 同步處理來使用基本驗證。 要使用 Web 同步,必須與 Web 伺服器建立 TLS 連接。 如需詳細資訊，請參閱 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)。  
  
`[ @internet_timeout = ] internet_timeout`是 Web 同步請求過期之前的時間長度(以秒為單位)。 *internet_timeout***是 int,** 預設為**300**秒。  
  
`[ @hostname = ] 'hostname'`在參數化篩選器的 WHERE 子句中使用此功能時,將覆蓋HOST_NAME()的值。 *主機名稱*是**系統名稱**,預設值為 NULL。  
  
`[ @job_login = ] 'job_login'`是代理運行的 Windows 帳戶的登錄名。 *job_login*是**nvarchar(257),** 沒有預設值。 代理程式連接到訂閱者時，一律使用這個 Windows 帳戶，當利用 Windows 整合式驗證來連接到散發者和發行者時，也一律使用這個 Windows 帳戶。  
  
`[ @job_password = ] 'job_password'`是代理運行的 Windows 帳戶的密碼。 *job_password*是**系統名稱**,沒有預設值。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 為了要有最佳的安全性，登入名稱和密碼應該在執行階段提供。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addmergepullsubscription_agent**用於合併複製,並使用類似於[sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)的功能。  
  
 有關如何在執行**sp_addmergepullsubscription_agent**時正確指定安全設定的範例,請參閱[建立拉取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**sysadmin**固定伺服器角色的成員或**db_owner**固定資料庫角色才能**執行sp_addmergepullsubscription_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [建立拉取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)   
 [訂閱出版物](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription&#40;交易-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription&#40;交易-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription&#40;轉算-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription&#40;交易-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
