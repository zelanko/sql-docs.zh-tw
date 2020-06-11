---
title: sp_addpullsubscription_agent （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/09/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpullsubscription_agent
- sp_addpullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addpullsubscription_agent
ms.assetid: b9c2eaed-6d2d-4b78-ae9b-73633133180b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f0704ff7d6764ca06c7de37d0d02bfbcb9148ce7
ms.sourcegitcommit: 1be90e93980a8e92275b5cc072b12b9e68a3bb9a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84627424"
---
# <a name="sp_addpullsubscription_agent-transact-sql"></a>sp_addpullsubscription_agent (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
 
  加入一項新排程的代理程式作業，以便用來同步處理提取訂閱與交易式發行集。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addpullsubscription_agent [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]          , [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @distributor = ] 'distributor' ]  
    [ , [ @distribution_db = ] 'distribution_db' ]  
    [ , [ @distributor_security_mode = ] distributor_security_mode ]  
    [ , [ @distributor_login = ] 'distributor_login' ]  
    [ , [ @distributor_password = ] 'distributor_password' ]  
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
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
    [ , [ @distribution_jobid = ] distribution_jobid OUTPUT ]  
    [ , [ @encrypted_distributor_password = ] encrypted_distributor_password ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port = ] ftp_port ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]  
    [ , [ @working_directory = ] 'working_directory' ]  
    [ , [ @use_ftp = ] 'use_ftp' ]  
    [ , [ @publication_type = ] publication_type ]  
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @offloadagent = ] 'remote_agent_activation' ]  
    [ , [ @offloadserver = ] 'remote_agent_server_name']  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'`這是發行者的名稱。 *publisher*是**sysname**，沒有預設值。  

> [!NOTE]
> 伺服器名稱可指定為 `<Hostname>,<PortNumber>` 。 當您使用自訂埠在 Linux 或 Windows 上部署 SQL Server，且已停用 browser 服務時，您可能需要指定連接的埠號碼。
  
`[ @publisher_db = ] 'publisher_db'_`這是發行者資料庫的名稱。 *publisher_db*是**sysname**，預設值是 Null。 Oracle 發行者會忽略*publisher_db* 。  
  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @subscriber = ] 'subscriber'`這是訂閱者實例的名稱，如果訂閱者資料庫位於可用性群組中，則為 AG 接聽程式的名稱。 *訂閱者*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。  
  
`[ @subscriber_db = ] 'subscriber_db'`這是訂閱資料庫的名稱。 *subscriber_db*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`這是在同步處理時，連接到訂閱者時所要使用的安全性模式。 *subscriber_security_mode*是**int，** 預設值是 Null。 **0**指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 **1**指定 Windows 驗證。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 散發代理程式一律是利用 Windows 驗證來連接到本機訂閱者。 如果為這個參數指定了 Null 或**1**以外的值，則會傳回警告訊息。  
  
`[ @subscriber_login = ] 'subscriber_login'`這是在同步處理時，用來連接訂閱者的訂閱者登入。*subscriber_login*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
`[ @subscriber_password = ] 'subscriber_password'`這是訂閱者密碼。 如果*subscriber_security_mode*設定為**0**，則需要*subscriber_password* 。 *subscriber_password*是**sysname**，預設值是 Null。 如果使用訂閱者密碼，它會自動加密。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
`[ @distributor = ] 'distributor'`這是散發者的名稱。 散發者是**sysname**，預設*值是**發行者*所指定的值。  
  
`[ @distribution_db = ] 'distribution_db'`這是散發資料庫的名稱。 *distribution_db*是**sysname**，預設值是 Null。  
  
`[ @distributor_security_mode = ] distributor_security_mode`這是在同步處理時，連接到散發者時所要使用的安全性模式。 *distributor_security_mode*是**int**，預設值是**1**。 **0**指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 **1**指定 Windows 驗證。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'`這是在同步處理時，用來連接到散發者的散發者登入。 如果*distributor_security_mode*設定為**0**，則需要*distributor_login* 。 *distributor_login*是**sysname**，預設值是 Null。  
  
`[ @distributor_password = ] 'distributor_password'`這是散發者密碼。 如果*distributor_security_mode*設定為**0**，則需要*distributor_password* 。 *distributor_password*是**sysname**，預設值是 Null。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @optional_command_line = ] 'optional_command_line'`這是提供給散發代理程式的選擇性命令提示字元。 例如， **-DefinitionFile** C:\Distdef.txt 或 **-CommitBatchSize** 10。 *optional_command_line*是**Nvarchar （4000）**，預設值是空字串。  
  
`[ @frequency_type = ] frequency_type`這是用來排程散發代理程式的頻率。 *frequency_type*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次性|  
|**2** (預設值)|隨選|  
|**4**|每日|  
|**8**|每週|  
|**1600**|每月|  
|**32**|每月相對|  
|**64**|自動啟動|  
|**128**|重複執行|  
  
> [!NOTE]  
>  指定值**64**會導致散發代理程式以連續模式執行。 這對應于設定代理程式的 **-連續**參數。 如需詳細資訊，請參閱 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)。  
  
`[ @frequency_interval = ] frequency_interval`這是要套用至*frequency_type*所設定之頻率的值。 *frequency_interval*是**int**，預設值是1。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`這是散發代理程式的日期。 當*frequency_type*設定為**32** （每月相對）時，會使用這個參數。 *frequency_relative_interval*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1** (預設值)|First|  
|**2**|Second|  
|**4**|第三個|  
|**8**|第四個|  
|**1600**|Last|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`這是*frequency_type*所使用的迴圈因數。 *frequency_recurrence_factor*是**int**，預設值是**1**。  
  
`[ @frequency_subday = ] frequency_subday`這是在定義的期間內重新排定的頻率。 *frequency_subday*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1** (預設值)|單次|  
|**2**|Second|  
|**4**|Minute|  
|**8**|小時|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`這是*frequency_subday*的間隔。 *frequency_subday_interval*是**int**，預設值是**1**。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`這是第一次排程散發代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*是**int**，預設值是**0**。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`這是排程停止散發代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是**int**，預設值是**0**。  
  
`[ @active_start_date = ] active_start_date`這是第一次排程散發代理程式的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，預設值是**0**。  
  
`[ @active_end_date = ] active_end_date`這是排程停止散發代理程式的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，預設值是**0**。  
  
`[ @distribution_jobid = ] _distribution_jobidOUTPUT`這是此作業的散發代理程式識別碼。 *distribution_jobid*是**binary （16）**，預設值是 Null，它是一個 OUTPUT 參數。  
  
`[ @encrypted_distributor_password = ] encrypted_distributor_password`已不再支援設定*encrypted_distributor_password* 。 嘗試將此**位**參數設定為**1**將會導致錯誤。  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`這是指是否可以透過同步處理管理員來同步處理訂閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。 *enabled_for_syncmgr*是**Nvarchar （5）**，預設值是 FALSE。 如果**為 false**，則表示訂閱未向同步處理管理員註冊。 若**為 true**，則會使用同步處理管理員註冊訂閱，而且可以在不啟動的情況下進行同步處理 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
`[ @ftp_address = ] 'ftp_address'`僅供回溯相容性之用。  
  
`[ @ftp_port = ] ftp_port`僅供回溯相容性之用。  
  
`[ @ftp_login = ] 'ftp_login'`僅供回溯相容性之用。  
  
`[ @ftp_password = ] 'ftp_password'`僅供回溯相容性之用。  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'_`指定快照集替代資料夾的位置。 *alternate_snapshot_folder*是**Nvarchar （255）**，預設值是 Null。  
  
`[ @working_directory = ] 'working_director'`這是用來儲存發行集資料和架構檔案的工作目錄名稱。 *working_directory*是**Nvarchar （255）**，預設值是 Null。 這個名稱應該用 UNC 格式來指定。  
  
`[ @use_ftp = ] 'use_ftp'`指定使用 FTP 而不是一般通訊協定來取得快照集。 *use_ftp*是**Nvarchar （5）**，預設值是 FALSE。  
  
`[ @publication_type = ] publication_type`指定發行集的複寫類型。 *publication_type*是**Tinyint** ，預設值是**0**。 如果是**0**，則發行集是交易類型。 如果是**1**，則發行集是快照集類型。 如果為**2**，則發行集是合併類型。  
  
`[ @dts_package_name = ] 'dts_package_name'`指定 DTS 封裝的名稱。 *dts_package_name*是預設值為 Null 的**sysname** 。 例如，若要指定 `DTSPub_Package` 封裝，這個參數便是 `@dts_package_name = N'DTSPub_Package'`。  
  
`[ @dts_package_password = ] 'dts_package_password'`指定封裝上的密碼（如果有的話）。 *dts_package_password*是**sysname** ，預設值是 Null，表示不在封裝上的密碼。  
  
> [!NOTE]  
>  如果指定*dts_package_name* ，您必須指定密碼。  
  
`[ @dts_package_location = ] 'dts_package_location'`指定封裝位置。 *dts_package_location*是**Nvarchar （12）**，預設值是「**訂閱者**」。 封裝的位置**可以是「** 散發者」或「**訂閱者**」。  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @offloadagent = ] 'remote_agent_activation'`
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 將*remote_agent_activation*設定為**false**以外的值將會產生錯誤。  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 將*remote_agent_server_name*設定為任何非 Null 值將會產生錯誤。  
  
`[ @job_name = ] 'job_name'`這是現有代理程式作業的名稱。 *job_name*是**sysname**，預設值是 Null。 只有在訂閱將利用現有的作業來同步處理，而不用新建立的作業 (預設值) 時，才指定這個參數。 如果您不是**系統管理員（sysadmin** ）固定伺服器角色的成員，則在指定*job_name*時，您必須指定*job_login*和*job_password* 。  
  
`[ @job_login = ] 'job_login'`這是用來執行代理程式之 Windows 帳戶的登入。 *job_login*是**Nvarchar （257）**，沒有預設值。 通往訂閱者的代理程式連接一律使用這個 Windows 帳戶。  
  
`[ @job_password = ] 'job_password'`這是執行代理程式之 Windows 帳戶的密碼。 *job_password*是**sysname**，沒有預設值。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addpullsubscription_agent**用於快照式複寫和異動複寫中。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-a_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_addpullsubscription_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
