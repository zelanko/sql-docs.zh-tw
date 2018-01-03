---
title: "sp_addpullsubscription_agent (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_addpullsubscription_agent
- sp_addpullsubscription_agent_TSQL
helpviewer_keywords: sp_addpullsubscription_agent
ms.assetid: b9c2eaed-6d2d-4b78-ae9b-73633133180b
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01f7e3cdecd4c0a95c9d91104e2feee39f00252b
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="spaddpullsubscriptionagent-transact-sql"></a>sp_addpullsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
 
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
 [  **@publisher=**] **'***發行者***'**  
 這是發行者的名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [  **@publisher_db=**] **'***publisher_db'*  
 這是發行者資料庫的名稱。 *publisher_db*是**sysname**，預設值是 NULL。 *publisher_db* Oracle 發行者會忽略。  
  
 [  **@publication=**] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@subscriber=**] **'***訂閱者***'**  
 這是訂閱者的名稱。 *訂閱者*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。  
  
 [  **@subscriber_db=**] **'***subscriber_db***'**  
 這是訂閱資料庫的名稱。 *subscriber_db*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。  
  
 [  **@subscriber_security_mode=**] *subscriber_security_mode*  
 這是進行同步處理時，連接到訂閱者時使用的安全性模式。 *subscriber_security_mode*是**int、**預設值是 NULL。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 **1**指定 Windows 驗證。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 散發代理程式一律是利用 Windows 驗證來連接到本機訂閱者。 如果 NULL 以外的值或**1**指定這個參數，就會傳回一則警告訊息。  
  
 [  **@subscriber_login =**] **'***subscriber_login***'**  
 是同步處理時至訂閱者連接時使用的訂閱者登入。*subscriber_login*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
 [  **@subscriber_password=**] **'***subscriber_password***'**  
 這是訂閱者密碼。 *subscriber_password*時需要*subscriber_security_mode*設**0**。 *subscriber_password*是**sysname**，預設值是 NULL。 如果使用訂閱者密碼，它會自動加密。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果指定了這個參數值，便會傳回警告訊息，但會忽略這個值。  
  
 [  **@distributor=**] **'***散發者***'**  
 這是散發者的名稱。 *散發者*是**sysname**，預設值是所指定的值*發行者*。  
  
 [  **@distribution_db=**] **'***distribution_db***'**  
 這是散發資料庫的名稱。 *distribution_db*是**sysname**，預設值是 NULL。  
  
 [  **@distributor_security_mode=**] *distributor_security_mode*  
 這是進行同步處理時，連接到散發者時使用的安全性模式。 *distributor_security_mode*是**int**，預設值是**1**。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 **1**指定 Windows 驗證。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@distributor_login=**] **'***distributor_login***'**  
 這是進行同步處理時，連接到散發者時使用的散發者登入。 *distributor_login*時需要*distributor_security_mode*設**0**。 *distributor_login*是**sysname**，預設值是 NULL。  
  
 [  **@distributor_password =**] **'***distributor_password***'**  
 這是散發者密碼。 *distributor_password*時需要*distributor_security_mode*設**0**。 *distributor_password*是**sysname**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
 [  **@optional_command_line=**] **'***optional_command_line***'**  
 這是提供給散發代理程式的選擇性命令提示字元。 例如， **-DefinitionFile** C:\Distdef.txt 或**-CommitBatchSize** 10。 *optional_command_line*是**nvarchar （4000)**，預設值為空字串。  
  
 [  **@frequency_type=**] *frequency_type*  
 這是排程散發代理程式所採用的頻率。 *frequency_type*是**int**，而且可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2** (預設值)|視需要|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64**|自動啟動|  
|**128**|重複執行|  
  
> [!NOTE]  
>  指定的值是**64**會導致散發代理程式以連續模式執行。 這會對應至設定**-連續**代理程式的參數。 如需詳細資訊，請參閱 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)。  
  
 [  **@frequency_interval=**] *frequency_interval*  
 若要設定的頻率所套用的值*frequency_type*。 *frequency_interval*是**int**，預設值是 1。  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 這是散發代理程式的日期。 使用這個參數時*frequency_type*設**32** （每月相對）。 *frequency_relative_interval*是**int**，而且可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**1** (預設值)|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*是**int**，預設值是**1**。  
  
 [  **@frequency_subday=**] *frequency_subday*  
 這是在定義的期間內，重新排程的頻率。 *frequency_subday*是**int**，而且可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**1** (預設值)|一次|  
|**2**|第二個|  
|**4**|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 間隔*frequency_subday*。 *frequency_subday_interval*是**int**，預設值是**1**。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 這是第一次排程散發代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*是**int**，預設值是**0**。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 這是排程停止散發代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是**int**，預設值是**0**。  
  
 [  **@active_start_date=**] *active_start_date*  
 這是第一次排程散發代理程式的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，預設值是**0**。  
  
 [  **@active_end_date=**] *active_end_date*  
 這是排程停止散發代理程式的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，預設值是**0**。  
  
 [  **@distribution_jobid =**] *distribution_jobid***輸出**  
 這是這項作業之散發代理程式的識別碼。 *distribution_jobid*是**binary （16)**，預設值是 NULL，它是一個 OUTPUT 參數。  
  
 [  **@encrypted_distributor_password=**] *encrypted_distributor_password*  
 設定*encrypted_distributor_password*不再支援。 嘗試將這個**元**參數**1**會導致錯誤。  
  
 [  **@enabled_for_syncmgr=**] **'***enabled_for_syncmgr***'**  
 為訂用帳戶是否可以透過同步[!INCLUDE[msCoName](../../includes/msconame-md.md)]Synchronization Manager。 *enabled_for_syncmgr*是**nvarchar （5)**，預設值是 FALSE。 如果**false**，訂用帳戶未註冊使用 Synchronization Manager。 如果**true**，則與 Synchronization Manager 註冊的訂閱，且可以同步處理，而不啟動[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
 [  **@ftp_address=**] **'***ftp_address***'**  
 只是為了與舊版相容。  
  
 [  **@ftp_port=**] *ftp_port*  
 只是為了與舊版相容。  
  
 [  **@ftp_login=**] **'***ftp_login***'**  
 只是為了與舊版相容。  
  
 [  **@ftp_password=**] **'***ftp_password***'**  
 只是為了與舊版相容。  
  
 [  **@alt_snapshot_folder=** ] **'***alternate_snapshot_folder'*  
 指定快照集替代資料夾的位置。 *alternate_snapshot_folder*是**nvarchar （255)**，預設值是 NULL。  
  
 [  **@working_directory** =] **'***working_director***'**  
 這是用來儲存發行集資料和結構描述檔案的工作目錄名稱。 *working_directory*是**nvarchar （255)**，預設值是 NULL。 這個名稱應該用 UNC 格式來指定。  
  
 [  **@use_ftp** =] **'***use_ftp***'**  
 指定利用 FTP 而不是一般通訊協定來擷取快照集。 *use_ftp*是**nvarchar （5)**，預設值是 FALSE。  
  
 [  **@publication_type** =] *publication_type*  
 指定發行集的複寫類型。 *publication_type*是**tinyint**預設值是**0**。 如果**0**，發行集是交易類型。 如果**1**，發行集是快照集類型。 如果**2**，發行集是合併類型。  
  
 [  **@dts_package_name** =] **'***dts_package_name***'**  
 指定 DTS 封裝的名稱。 *dts_package_name*是**sysname**預設值是 NULL。 例如，若要指定 `DTSPub_Package` 封裝，這個參數便是 `@dts_package_name = N'DTSPub_Package'`。  
  
 [  **@dts_package_password** =] **'***dts_package_password***'**  
 指定封裝的密碼 (如果有的話)。 *dts_package_password*是**sysname**預設值是 NULL，這表示密碼不是在封裝上。  
  
> [!NOTE]  
>  如果您必須指定密碼*dts_package_name*指定。  
  
 [  **@dts_package_location** =] **'***dts_package_location***'**  
 指定封裝的位置。 *dts_package_location*是**nvarchar （12)**，預設值是**訂閱者**。 封裝位置可以是**散發者**或**訂閱者**。  
  
 [  **@reserved** =] **'***保留***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@offloadagent** =] '*remote_agent_activation*'  
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 設定*remote_agent_activation*以外的值來**false**會產生錯誤。  
  
 [  **@offloadserver** =] '*remote_agent_server_name*'  
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 設定*remote_agent_server_name*為任何非 NULL 值會產生錯誤。  
  
 [  **@job_name** =] '*job_name*'  
 這是現有散發代理程式作業的名稱。 *job_name*是**sysname**，預設值是 NULL。 只有在訂閱將利用現有的作業來同步處理，而不用新建立的作業 (預設值) 時，才指定這個參數。 如果您不屬於**sysadmin**固定伺服器角色，您必須指定*job_login*和*job_password*當您指定*job_name*.  
  
 [  **@job_login** =] **'***job_login***'**  
 這是用來執行代理程式之 Windows 帳戶的登入。 *job_login*是**nvarchar （257)**，沒有預設值。 通往訂閱者的代理程式連接一律使用這個 Windows 帳戶。  
  
 [  **@job_password** =] **'***job_password***'**  
 這是用來執行代理程式之 Windows 帳戶的密碼。 *job_password*是**sysname**，沒有預設值。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addpullsubscription_agent**用於快照式複寫和異動複寫。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-a_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addpullsubscription_agent**。  
  
## <a name="see-also"></a>請參閱  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
