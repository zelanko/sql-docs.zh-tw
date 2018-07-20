---
title: sp_addpushsubscription_agent & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
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
- sp_addpushsubscription_agent_TSQL
- sp_addpushsubscription_agent
helpviewer_keywords:
- sp_addpushsubscription_agent
ms.assetid: 1fdd2052-50d8-4318-8aa7-fc635d5cad18
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 65e24090d009a33f221abc0ba4bf2502418fd377
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39083570"
---
# <a name="spaddpushsubscriptionagent-transact-sql"></a>sp_addpushsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  加入一項新排程的代理程式作業，以便用來同步處理發送訂閱與交易式發行集。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!IMPORTANT]  
>  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addpushsubscription_agent [ @publication= ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @job_name = ] 'job_name' ]   
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
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @distribution_job_name = ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @subscriber_provider = ] 'subscriber_provider' ]   
    [ , [ @subscriber_datasrc = ] 'subscriber_datasrc' ]   
    [ , [ @subscriber_location = ] 'subscriber_location' ]  
    [ , [ @subscriber_provider_string = ] 'subscriber_provider_string' ]   
    [ , [ @subscriber_catalog = ] 'subscriber_catalog' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication =**] **'***發行集***'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@subscriber =**] **'***訂閱者***'**  
 這是訂閱者的名稱。 *訂閱者*已**sysname**，預設值是 NULL。  
  
 [  **@subscriber_db =**] **'***subscriber_db***'**  
 這是訂閱資料庫的名稱。 *subscriber_db*已**sysname**，預設值是 NULL。 針對非 SQL Server 訂閱者，指定其值為 **（預設目的地）** for *subscriber_db*。  
  
 [  **@subscriber_security_mode =**] *subscriber_security_mode*  
 這是進行同步處理時，連接到訂閱者時使用的安全性模式。 *subscriber_security_mode*已**int**，預設值是 1。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 **1**指定 Windows 驗證。  
  
> [!IMPORTANT]  
>  對於佇列更新訂閱，請利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來連接訂閱者，以及指定不同的連接帳戶給每個訂閱者。 對於其他所有訂閱，請使用 Windows 驗證。  
  
 [  **@subscriber_login =**] **'***subscriber_login***'**  
 這是進行同步處理時，連接到訂閱者時使用的訂閱者登入。 *subscriber_login*已**sysname**，預設值是 NULL。  
  
 [  **@subscriber_password =**] **'***subscriber_password***'**  
 這是訂閱者密碼。 *subscriber_password* ，便須*subscriber_security_mode*設定為**0**。 *subscriber_password*已**sysname**，預設值是 NULL。 如果使用訂閱者密碼，它會自動加密。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
 [  **@job_login =** ] **'***job_login***'**  
 是執行代理程式帳戶的登入。 在 Azure SQL Database 受控執行個體上使用 SQL Server 帳戶。 *job_login*已**nvarchar(257)**，預設值是 NULL。 使用 Windows 整合式驗證時，對於通往散發者的代理程式連接及通往訂閱者的連接，一律使用這個 Windows 帳戶。  
  
 [  **@job_password =** ] **'***job_password***'**  
 是執行代理程式帳戶的密碼。 *job_password*已**sysname**，沒有預設值。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
 [ **@job_name =** ] **'***job_name***'**  
 這是現有散發代理程式作業的名稱。 *job_name*已**sysname**，預設值是 NULL。 只有在訂閱將利用現有的作業來同步處理，而不用新建立的作業 (預設值) 時，才指定這個參數。 如果您不屬於**sysadmin**固定伺服器角色，您必須指定*job_login*並*job_password*當您指定*job_name*.  
  
 [  **@frequency_type =** ] *frequency_type*  
 這是排程散發代理程式所採用的頻率。 *frequency_type*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|視需要|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64** （預設值）|自動啟動|  
|**128**|重複執行|  
  
> [!NOTE]  
>  指定的值是**64**會導致散發代理程式以連續模式執行。 這對應於設定 **-連續**代理程式參數。 如需詳細資訊，請參閱 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)。  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 要套用至所設定之頻率的值*frequency_type*。 *frequency_interval*已**int**，預設值是 1。  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 這是散發代理程式的日期。 使用這個參數時*frequency_type*設為**32** （每月相對）。 *frequency_relative_interval*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1** (預設值)|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor&lt*  
 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*已**int**，預設值是 0。  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 這是在定義的期間內，重新排程的頻率。 *frequency_subday*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4** （預設值）|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 間隔*frequency_subday*。 *frequency_subday_interval*已**int**，預設值是 5。  
  
 [  **@active_start_time_of_day =** ] *active_start_time_of_day*  
 這是第一次排程散發代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*已**int**，預設值是 0。  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 這是排程停止散發代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*已**int**，預設值是 235959。  
  
 [ **@active_start_date =** ] *active_start_date*  
 這是第一次排程散發代理程式的日期，格式為 YYYYMMDD。 *active_start_date*已**int**，預設值是 0。  
  
 [ **@active_end_date =** ] *active_end_date*  
 這是排程停止散發代理程式的日期，格式為 YYYYMMDD。 *active_end_date*已**int**，預設值是 99991231。  
  
 [  **@dts_package_name =** ] **'***dts_package_name***'**  
 指定 Data Transformation Services (DTS) 封裝的名稱。 *dts_package_name*已**sysname**預設值是 NULL。 例如，若要指定 `DTSPub_Package` 的封裝名稱，這個參數便是 `@dts_package_name = N'DTSPub_Package'`。  
  
 [  **@dts_package_password =** ] **'***dts_package_password***'**  
 指定執行封裝所需的密碼。 *dts_package_password*已**sysname**預設值是 NULL。  
  
> [!NOTE]  
>  您必須指定密碼，如果*dts_package_name*指定。  
  
 [  **@dts_package_location =** ] **'***dts_package_location***'**  
 指定封裝的位置。 *dts_package_location*已**nvarchar(12)**，預設值是 「 散發者 」。 封裝位置可以是**散發者端**或是**訂閱者**。  
  
 [  **@enabled_for_syncmgr =** ] **'***enabled_for_syncmgr***'**  
 為訂用帳戶是否可以透過同步[!INCLUDE[msCoName](../../includes/msconame-md.md)]Synchronization Manager。 *enabled_for_syncmgr*已**nvarchar(5)**，預設值是 FALSE。 如果**false**，訂用帳戶未註冊使用 Synchronization Manager。 如果**真**，訂用帳戶使用 Synchronization Manager 註冊，並可以同步處理，而不啟動[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
 [  **@distribution_job_name =** ] **'***distribution_job_name***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@publisher =** ] **'***發行者***'**  
 這是發行者的名稱。 *發行者*已**sysname**，預設值是 NULL。  
  
 [  **@subscriber_provider=** ] **'***subscriber_provider***'**  
 這是用來登錄非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源之 OLE DB 提供者的唯一程式化識別碼 (PROGID)。 *subscriber_provider*已**sysname**，預設值是 NULL。 *subscriber_provider*必須是唯一的 「 散發者 」 上安裝 OLE DB 提供者。 *subscriber_provider*僅支援非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者。  
  
 [  **@subscriber_datasrc=** ] **'***subscriber_datasrc***'**  
 這是 OLE DB 提供者所了解的資料來源名稱。 *subscriber_datasrc*已**nvarchar(4000)**，預設值是 NULL。 *subscriber_datasrc*被當做 DBPROP_INIT_DATASOURCE 屬性傳入來初始化 OLE DB 提供者。 *subscriber_datasrc*僅支援非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者。  
  
 [  **@subscriber_location=** ] **'***subscriber_location***'**  
 這是 OLE DB 提供者所了解的資料庫位置 *subscriber_location*已**nvarchar(4000)**，預設值是 NULL。 *subscriber_location*被當做 DDBPROP_INIT_LOCATION 屬性來初始化 OLE DB 提供者。 *subscriber_location*僅支援非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者。  
  
 [  **@subscriber_provider_string=** ] **'***subscriber_provider_string***'**  
 這是 OLE DB 提供者特定的連接字串，用來識別資料來源。 *subscriber_provider_string*已**nvarchar(4000)**，預設值是 NULL。 *subscriber_provider_string*是傳遞至 IDataInitialize 或設定為 DBPROP_INIT_PROVIDERSTRING 屬性以初始化 OLE DB 提供者。 *subscriber_provider_string*僅支援非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者。  
  
 [  **@subscriber_catalog=** ] **'***subscriber_catalog***'**  
 這是建立 OLE DB 提供者連接時所用的目錄。 *subscriber_catalog*已**sysname**，預設值是 NULL。 *subscriber_catalog*被當做 DBPROP_INIT_CATALOG 屬性傳入來初始化 OLE DB 提供者。 *subscriber_catalog*僅支援非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addpushsubscription_agent**用於快照式複寫和異動複寫。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addpushsubscription-a_1.sql)]  
  
## <a name="permissions"></a>[權限]  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addpushsubscription_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [為非 SQL Server 訂閱者建立訂閱](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_addsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)   
 [sp_dropsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
