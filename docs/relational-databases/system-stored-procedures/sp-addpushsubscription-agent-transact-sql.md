---
title: sp_addpushsubscription_agent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/09/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpushsubscription_agent_TSQL
- sp_addpushsubscription_agent
helpviewer_keywords:
- sp_addpushsubscription_agent
ms.assetid: 1fdd2052-50d8-4318-8aa7-fc635d5cad18
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 42dffc53fbce2350314d773ce4cd376fae84256a
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864985"
---
# <a name="sp_addpushsubscription_agent-transact-sql"></a>sp_addpushsubscription_agent (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

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
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @subscriber = ] 'subscriber'`這是訂閱者實例的名稱，如果訂閱者資料庫是可用性群組，則為 AG 接聽程式的名稱。 *訂閱者*是**sysname**，預設值是 Null。 

> [!NOTE]
> 伺服器名稱可指定為 `<Hostname>,<PortNumber>` 。 當您使用自訂埠在 Linux 或 Windows 上部署 SQL Server，且已停用 browser 服務時，您可能需要指定連接的埠號碼。

`[ @subscriber_db = ] 'subscriber_db'`這是訂閱資料庫的名稱。 *subscriber_db*是**sysname**，預設值是 Null。 若為非 SQL Server 的訂閱者，請為*subscriber_db*指定** (預設目的地) **的值。  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`這是在同步處理時，連接到訂閱者時所要使用的安全性模式。 *subscriber_security_mode*是**int**，預設值是1。 **0**指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 **1**指定 Windows 驗證。  
  
> [!IMPORTANT]  
>  對於佇列更新訂閱，請利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來連接訂閱者，以及指定不同的連接帳戶給每個訂閱者。 對於其他所有訂閱，請使用 Windows 驗證。  
  
`[ @subscriber_login = ] 'subscriber_login'`這是在同步處理時，用來連接訂閱者的訂閱者登入。 *subscriber_login*是**sysname**，預設值是 Null。  
  
`[ @subscriber_password = ] 'subscriber_password'`這是訂閱者密碼。 如果*subscriber_security_mode*設定為**0**，則需要*subscriber_password* 。 *subscriber_password*是**sysname**，預設值是 Null。 如果使用訂閱者密碼，它會自動加密。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @job_login = ] 'job_login'`這是用來執行代理程式之帳戶的登入。 在 Azure SQL 受控執行個體使用 SQL Server 帳戶。 *job_login*是**Nvarchar (257) **，預設值是 Null。 使用 Windows 整合式驗證時，對於通往散發者的代理程式連接及通往訂閱者的連接，一律使用這個 Windows 帳戶。  
  
`[ @job_password = ] 'job_password'`這是用來執行代理程式之帳戶的密碼。 *job_password*是**sysname**，沒有預設值。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @job_name = ] 'job_name'`這是現有代理程式作業的名稱。 *job_name*是**sysname**，預設值是 Null。 只有在訂閱將利用現有的作業來同步處理，而不用新建立的作業 (預設值) 時，才指定這個參數。 如果您不是**系統管理員（sysadmin** ）固定伺服器角色的成員，則在指定*job_name*時，您必須指定*job_login*和*job_password* 。  
  
`[ @frequency_type = ] frequency_type`這是用來排程散發代理程式的頻率。 *frequency_type*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次性|  
|**2**|隨選|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64** (預設) |自動啟動|  
|**128**|重複執行|  
  
> [!NOTE]  
>  指定值**64**會導致散發代理程式以連續模式執行。 這對應于設定代理程式的 **-連續**參數。 如需詳細資訊，請參閱 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)。  
  
`[ @frequency_interval = ] frequency_interval`這是要套用至*frequency_type*所設定之頻率的值。 *frequency_interval*是**int**，預設值是1。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`這是散發代理程式的日期。 當*frequency_type*設定為**32** (每月相對) 時，會使用這個參數。 *frequency_relative_interval*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1** (預設值)|First|  
|**2**|Second|  
|**4**|Third|  
|**8**|第四個|  
|**16**|Last|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`這是*frequency_type*所使用的迴圈因數。 *frequency_recurrence_factor*是**int**，預設值是0。  
  
`[ @frequency_subday = ] frequency_subday`這是在定義的期間內重新排定的頻率。 *frequency_subday*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**2**|Second|  
|**4** (預設) |Minute|  
|**8**|小時|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`這是*frequency_subday*的間隔。 *frequency_subday_interval*是**int**，預設值是5。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`這是第一次排程散發代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*是**int**，預設值是0。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`這是排程停止散發代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是**int**，預設值是235959。  
  
`[ @active_start_date = ] active_start_date`這是第一次排程散發代理程式的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，預設值是0。  
  
`[ @active_end_date = ] active_end_date`這是排程停止散發代理程式的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，預設值是99991231。  
  
`[ @dts_package_name = ] 'dts_package_name'`指定 (DTS) 封裝之資料轉換服務的名稱。 *dts_package_name*是預設值為 Null 的**sysname** 。 例如，若要指定 `DTSPub_Package` 的封裝名稱，這個參數便是 `@dts_package_name = N'DTSPub_Package'`。  
  
`[ @dts_package_password = ] 'dts_package_password'`指定執行封裝所需的密碼。 *dts_package_password*是**sysname** ，預設值是 Null。  
  
> [!NOTE]  
>  如果指定*dts_package_name* ，您必須指定密碼。  
  
`[ @dts_package_location = ] 'dts_package_location'`指定封裝位置。 *dts_package_location*是**Nvarchar (12) **，預設值為「散發者」。 封裝的位置**可以是「** 散發者」或「**訂閱者**」。  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`這是指是否可以透過同步處理管理員來同步處理訂閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。 *enabled_for_syncmgr*是**Nvarchar (5) **，預設值是 FALSE。 如果**為 false**，則表示訂閱未向同步處理管理員註冊。 若**為 true**，則會使用同步處理管理員註冊訂閱，而且可以在不啟動的情況下進行同步處理 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
`[ @distribution_job_name = ] 'distribution_job_name'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @publisher = ] 'publisher'`這是發行者的名稱。 *publisher*是**sysname**，預設值是 Null。  
  
`[ @subscriber_provider = ] 'subscriber_provider'`這是唯一的程式設計識別碼， (PROGID) ，用於註冊非資料來源的 OLE DB 提供者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *subscriber_provider*是**sysname**，預設值是 Null。 針對散發者上所安裝的 OLE DB 提供者， *subscriber_provider*必須是唯一的。 *subscriber_provider*只有非訂閱者才支援 subscriber_provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
`[ @subscriber_datasrc = ] 'subscriber_datasrc'`這是 OLE DB 提供者所瞭解的資料來源名稱。 *subscriber_datasrc*是**Nvarchar (4000) **，預設值是 Null。 *subscriber_datasrc*會當做 DBPROP_INIT_DATASOURCE 屬性傳遞，以初始化 OLE DB 提供者。 *subscriber_datasrc*只有非訂閱者才支援 subscriber_datasrc [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
`[ @subscriber_location = ] 'subscriber_location'`這是 OLE DB 提供者所瞭解的資料庫位置。 *subscriber_location*是**Nvarchar (4000) **，預設值是 Null。 *subscriber_location*會當做 DBPROP_INIT_LOCATION 屬性傳遞，以初始化 OLE DB 提供者。 *subscriber_location*只有非訂閱者才支援 subscriber_location [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
`[ @subscriber_provider_string = ] 'subscriber_provider_string'`這是用來識別資料來源的 OLE DB 提供者特定的連接字串。 *subscriber_provider_string*是**Nvarchar (4000) **，預設值是 Null。 *subscriber_provider_string*會傳遞至 IDataInitialize 或設定為 DBPROP_INIT_PROVIDERSTRING 屬性，以初始化 OLE DB 提供者。 *subscriber_provider_string*只有非訂閱者才支援 subscriber_provider_string [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
`[ @subscriber_catalog = ] 'subscriber_catalog'`這是連接到 OLE DB 提供者時所要使用的目錄。 *subscriber_catalog*是**sysname**，預設值是 Null。 *subscriber_catalog*會當做 DBPROP_INIT_CATALOG 屬性傳遞，以初始化 OLE DB 提供者。 *subscriber_catalog*只有非訂閱者才支援 subscriber_catalog [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或**1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_addpushsubscription_agent**用於快照式複寫和異動複寫中。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addpushsubscription-a_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_addpushsubscription_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [為非 SQL Server 的訂閱者建立訂用帳戶](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [&#40;Transact-sql&#41;的複寫預存程式](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_addsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
