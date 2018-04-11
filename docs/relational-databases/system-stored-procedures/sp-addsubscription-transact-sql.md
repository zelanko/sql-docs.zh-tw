---
title: p (TRANSACT-SQL) |Microsoft 文件
ms.date: 10/28/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addsubscription
- sp_addsubscription_TSQL
helpviewer_keywords:
- sp_addsubscription
ms.assetid: 61ddf287-1fa0-4c1a-8657-ced50cebf0e0
caps.latest.revision: 53
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 860f2f99457344167af9035d0a9ccc21eebc2577
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/10/2018
---
# <a name="spaddsubscription-transact-sql"></a>sp_addsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將訂閱加入發行集中，以及設定訂閱者狀態。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addsubscription [ @publication = ] 'publication'  
    [ , [ @article = ] 'article']  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @destination_db = ] 'destination_db' ]  
        [ , [ @sync_type = ] 'sync_type' ]  
    [ , [ @status = ] 'status'  
        [ , [ @subscription_type = ] 'subscription_type' ]  
    [ , [ @update_mode = ] 'update_mode' ]  
    [ , [ @loopback_detection = ] 'loopback_detection' ]  
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
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @enabled_for_syncmgr= ] 'enabled_for_syncmgr' ]  
    [ , [ @offloadagent= ] remote_agent_activation]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] 'dts_package_location' ]  
    [ , [ @distribution_job_name= ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @backupdevicetype = ] 'backupdevicetype' ]  
    [ , [ @backupdevicename = ] 'backupdevicename' ]  
    [ , [ @mediapassword = ] 'mediapassword' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @fileidhint = ] fileidhint ]  
    [ , [ @unload = ] unload ]  
    [ , [ @subscriptionlsn = ] subscriptionlsn ]  
    [ , [ @subscriptionstreams = ] subscriptionstreams ]  
    [ , [ @subscriber_type = ] subscriber_type ]  
    [ , [ @memory_optimized = ] memory_optimized ]  
```  
  
## <a name="arguments"></a>引數  
 [ @publication=] '*publication*'  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [ @article=] '*article*'  
 這是發行集訂閱的發行項。 *發行項*是**sysname**，所有的預設值。 如果是 all，就會將訂閱加入該發行集的所有發行項中。 只有 all 或 NULL 值支援 Oracle 發行者。  
  
 [ @subscriber=] '*subscriber*'  
 這是訂閱者的名稱。 *訂閱者*是**sysname**，預設值是 NULL。  
  
 [ @destination_db=] '*destination_db*'  
 這是放置複寫資料之目的地資料庫的名稱。 *destination_db*是**sysname**，預設值是 NULL。 為 null， *destination_db*會設為發行集資料庫的名稱。 Oracle 發行者， *destination_db*必須指定。 針對非 SQL Server 訂閱者，指定的值 （預設目的地） 的*destination_db*。  
  
 [ @sync_type=] '*sync_type*'  
 這是訂閱同步處理類型。 *sync_type*是**nvarchar （255)**，而且可以是下列值之一：  
  
|Value|Description|  
|-----------|-----------------|  
|無|訂閱者已有發行資料表的結構描述和初始資料。<br /><br /> 注意： 此選項已被取代。 請改用 replication support only。|  
|automatic (預設值)|先將發行資料表的結構描述和初始資料傳送給訂閱者。|  
|replication support only|提供在訂閱者自動產生支援更新訂閱之發行項自訂預存程序和觸發程序的功能 (如果適用)。 假設訂閱者已有發行資料表的結構描述和初始資料。 當設定點對點異動複寫拓撲時，請確定拓撲中所有節點的資料都相同。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。<br /><br /> *不支援非 SQL Server 發行集的訂閱。*|  
|initialize with backup|從發行集資料庫的備份中，取得發行資料表的結構描述和初始資料。 假設訂閱者有權存取發行集資料庫的備份。 備份的備份和媒體類型的位置由*backupdevicename*和*backupdevicetype*。 當使用這個選項時，不需要在設定組態期間，默認點對點異動複寫拓撲。<br /><br /> *不支援非 SQL Server 發行集的訂閱。*|  
|initialize from lsn|當您要將節點加入至點對點異動複寫拓撲時使用。 搭配 @subscriptionlsn 使用可確保所有相關的交易都會複寫至新的節點。 假設訂閱者已有發行資料表的結構描述和初始資料。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。|  
  
> [!NOTE]  
>  一律會傳送系統資料表和資料。  
  
 [ @status=] '*status*'  
 這是訂閱狀態。 *狀態*是**sysname**，預設值是 NULL。 如果未明確設定這個參數，複寫會自動將它設定為這些值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|active|訂閱已初始化且已做好接受變更的準備。 此選項時，會設定的值*sync_type*是 none、 initialize with backup 或僅支援複寫。|  
|subscribed|訂閱需要初始化。 此選項時，會設定的值*sync_type*為自動。|  
  
 [ @subscription_type=] '*subscription_type*'  
 這是訂閱的類型。 *subscription_type*是**nvarchar （4)**，預設值是 push。 它可以是 push 或 pull。 發送訂閱的 「 散發代理程式位於散發者上，並提取訂閱的 「 散發代理程式位於訂閱者端。 *subscription_type*可以是 pull，以便建立發行者已知的具名的提取訂閱。 如需詳細資訊，請參閱[訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)。  
  
> [!NOTE]  
>  匿名訂閱不需要使用這個預存程序。  
  
 [ @update_mode=] '*update_mode*'  
 已更新的型別。*update_mode*是**nvarchar （30)**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|read only (預設值)|訂閱是唯讀的。 在訂閱者端的變更不會傳給發行者。|  
|sync tran|啟用立即更新訂閱的支援。 不支援 Oracle 發行者使用這個值。|  
|queued tran|啟用佇列更新的訂閱。 資料修改可以在訂閱者端進行、儲存在佇列中，再傳播給發行者。 不支援 Oracle 發行者使用這個值。|  
|failover|啟用立即更新的訂閱，且利用佇列更新來做為容錯移轉。 資料修改可以在訂閱者端進行，再立即傳播給發行者。 如果發行者和訂閱者並未連接，便可以變更更新模式，以便將在訂閱者端進行的資料修改儲存在佇列中，直到發行者和訂閱者重新連接為止。 不支援 Oracle 發行者使用這個值。|  
|queued failover|將訂閱啟用成能夠改成立即更新模式的佇列更新訂閱。 資料修改可以在訂閱者端進行，儲存在佇列中，直到重建訂閱者和發行者之間的連接為止。 當建立連續連接時，更新模式可以改成立即更新。 不支援 Oracle 發行者使用這個值。|  
  
 請注意，值 synctran 和 queued 的 tran 不允許如果訂閱的發行集允許 DTS。  
  
 [ @loopback_detection=] '*loopback_detection*'  
 指定散發代理程式是否會將起源於訂閱者端的交易傳回給訂閱者。 *loopback_detection*是**nvarchar （5)**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|true|散發代理程式不將起源於訂閱者端的交易傳回給訂閱者。 搭配雙向異動複寫來使用。 如需詳細資訊，請參閱[雙向異動複寫](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md)。|  
|false|散發代理程式將起源於訂閱者端的交易傳回給訂閱者。|  
|NULL (預設值)|針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者，會自動設定為 true，而針對非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者，則會自動設定為 false。|  
  
 [ @frequency_type=] *frequency_type*  
 這是散發工作的排程頻率。 *frequency_type*是 int，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|1|一次|  
|2|視需要|  
|4|每日|  
|8|每週|  
|16|每月|  
|32|每月相對|  
|64 （預設值）|自動啟動|  
|128|重複執行|  
  
 [ @frequency_interval=] *frequency_interval*  
 若要設定的頻率所套用的值*frequency_type*。 *frequency_interval*是**int**，預設值是 NULL。  
  
 [ @frequency_relative_interval=] *frequency_relative_interval*  
 這是散發代理程式的日期。 使用這個參數時*frequency_type*設為 32 （每月相對）。 *frequency_relative_interval*是**int**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|1|第一個|  
|2|第二個|  
|4|第三個|  
|8|第四個|  
|16|最後一個|  
|NULL (預設值)||  
  
 [ @frequency_recurrence_factor=] *frequency_recurrence_factor*  
 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*是**int**，預設值是 NULL。  
  
 [ @frequency_subday=] *frequency_subday*  
 這是在定義的期間內，重新排程的頻率 (以分鐘為單位)。 *frequency_subday*是**int**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|1|一次|  
|2|第二個|  
|4|Minute|  
|8|Hour|  
|NULL||  
  
 [ @frequency_subday_interval=] *frequency_subday_interval*  
 間隔*frequency_subday*。 *frequency_subday_interval*是**int**，預設值是 NULL。  
  
 [ @active_start_time_of_day=] *active_start_time_of_day*  
 這是第一次排程散發代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*是**int**，預設值是 NULL。  
  
 [ @active_end_time_of_day=] *active_end_time_of_day*  
 這是排程停止散發代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是**int**，預設值是 NULL。  
  
 [ @active_start_date=] *active_start_date*  
 這是第一次排程散發代理程式的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，預設值是 NULL。  
  
 [ @active_end_date=] *active_end_date*  
 這是排程停止散發代理程式的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，預設值是 NULL。  
  
 [ @optional_command_line=] '*optional_command_line*'  
 這是要執行的選擇性命令提示字元。 *optional_command_line*是**nvarchar （4000)**，預設值是 NULL。  
  
 [ @reserved=] '*reserved*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @enabled_for_syncmgr=] '*enabled_for_syncmgr*'  
 為訂用帳戶是否可以透過同步[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows Synchronization Manager。 *enabled_for_syncmgr*是**nvarchar （5)**，預設值是 FALSE。 如果是 false，便不用 Windows Synchronization Manager 來註冊訂閱。 如果是 true，便用 Windows Synchronization Manager 來註冊訂閱，而且不需要啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，就可以同步處理。 不支援 Oracle 發行者使用這個值。  
  
 [ @offloadagent= ] '*remote_agent_activation*'  
 指定是否能從遠端啟動代理程式。 *remote_agent_activation*是**元**預設值是 0。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。  
  
 [ @offloadserver= ] '*remote_agent_server_name*'  
 指定將用來遠端啟用之伺服器的網路名稱。 *remote_agent_server_name*是**sysname**，預設值是 NULL。  
  
 [ @dts_package_name= ] '*dts_package_name*'  
 指定 Data Transformation Services (DTS) 封裝的名稱。 *dts_package_name*是**sysname**預設值是 NULL。 例如，若要指定 DTSPub_Package 封裝，這個參數便是 `@dts_package_name = N'DTSPub_Package'`。 發送訂閱可以使用這個參數。 若要將 DTS 封裝資訊加入提取訂閱中，請使用 sp_addpullsubscription_agent。  
  
 [ @dts_package_password= ] '*dts_package_password*'  
 指定封裝的密碼 (如果有的話)。 *dts_package_password*是**sysname**預設值是 NULL。  
  
> [!NOTE]  
>  如果您必須指定密碼*dts_package_name*指定。  
  
 [ @dts_package_location= ] '*dts_package_location*'  
 指定封裝的位置。 *dts_package_location*是**nvarchar （12)**，預設值是 「 散發者 」。 封裝位置可以是散發者或訂閱者。  
  
 [ @distribution_job_name= ] '*distribution_job_name*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @publisher= ] '*publisher*'  
 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應指定為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
 [ @backupdevicetype= ] '*backupdevicetype*'  
 指定從備份中初始化訂閱者時所用的備份裝置類型。 *backupdevicetype*是**nvarchar （20)**，而且可以是下列值之一：  
  
|Value|Description|  
|-----------|-----------------|  
|logical (預設值)|備份裝置是邏輯裝置。|  
|disk|備份裝置是硬碟。|  
|tape|備份裝置是磁帶機。|  
  
 *backupdevicetype*時，才使用*sync_method*設定為 initialize_with_backup 時。  
  
 [ @backupdevicename= ] '*backupdevicename*'  
 指定從備份中初始化訂閱者時所用的裝置名稱。 *backupdevicename*是**nvarchar （1000)**，預設值是 NULL。  
  
 [ @mediapassword= ] '*mediapassword*'  
 如果媒體格式化時設定了密碼，便指定媒體集的密碼。 *mediapassword*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 [ @password= ] '*password*'  
 如果建立備份時設定了密碼，便指定備份的密碼。 *密碼*是**sysname**，預設值是 NULL。  
  
 [ @fileidhint= ] *fileidhint*  
 識別要還原之備份組的序數值。 *fileidhint*是**int**，預設值是 NULL。  
  
 [ @unload= ] *unload*  
 指定在從備份初始化完成之後，是否應該卸載磁帶備份裝置。 *卸載*是**元**，預設值是 1。 1 指定應該卸載磁帶。 *卸載*時，才使用*backupdevicetype*的磁帶。  
  
 [ @subscriptionlsn= ] *subscriptionlsn*  
 指定記錄序號 (LSN)，而且訂閱應該從這個序號開始傳遞變更至點對點異動複寫拓撲中的節點。 搭配@sync_typeinitialize from lsn，若要確保所有相關的交易都會複寫到新的節點值。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 [ @subscriptionstreams= ] *subscriptionstreams*  
 這是在維護許多使用單一執行緒時所提供的交易式特性時，每個散發代理程式可用來將變更批次並行套用在訂閱者上的連接數目。 *subscriptionstreams*是**tinyint**，預設值是 NULL。 支援的值範圍是 1-64。 不支援非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者、Oracle 發行者或點對點訂閱使用這個參數。 每當使用訂閱資料流時，msreplication_subscriptions 資料表就會加入其他資料列 (每個資料流 1 個資料列) 並將 agent_id 設定為 NULL。  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)]Subscriptionstreams 不適用於設定為傳遞  的發行項。 若要使用 subscriptionstreams，請改將發行項設定為傳遞預存程序呼叫。  
  
 [ @subscriber_type=] *subscriber_type*  
 這是訂閱者的類型。 *subscriber_type*是**tinyint**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|0 (預設值)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者|  
|1|ODBC 資料來源伺服器|  
|2|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet 資料庫|  
|3|OLE DB 提供者|  
  
 [ @memory_optimized=] *memory_optimized*  
 指出訂用帳戶支援記憶體最佳化的資料表。 *memory_optimized*是**元**，其中 1 等於 true （訂用帳戶支援記憶體最佳化資料表）。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 sp_addsubscription 用於快照式複寫和異動複寫中。  
  
 當系統管理員 (sysadmin) 固定伺服器角色的成員執行 sp_addsubscription 來建立發送訂閱時，系統會隱含地建立散發代理程式作業，而且會利用 SQL Server Agent 服務帳戶來執行這項作業。 我們建議您執行[sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) ，並指定不同代理程式專用 Windows 帳戶認證@job_login和@job_password。 如需詳細資訊，請參閱 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
 sp_addsubscription 可防止 ODBC 和 OLE DB 訂閱者存取符合下列狀況的發行集：  
  
-   建立具有原生*sync_method*呼叫[sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。  
  
-   包含加入至與發行集的發行項[sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)預存程序具有*pre_creation_cmd*參數值是 3 （截斷）。  
  
-   嘗試設定*update_mode*設為 sync tran。  
  
-   有設定成使用參數化陳述式的發行項。  
  
 此外，如果發行集有*allow_queued_tran*選項設定為 true (啟用佇列的 「 訂閱者 」 端的變更之前將它們套用在發行者端），發行項中的時間戳記資料行便會編寫成**時間戳記**，並在該資料行的變更會傳送至 「 訂閱者 」。 訂閱者會產生和更新時間戳記資料行值。 對於 ODBC 或 OLE DB 訂閱者，sp_addsubscription 失敗如果嘗試訂閱的發行集具有*allow_queued_tran*設為 true 及含有時間戳記資料行的發行項。  
  
 如果訂用帳戶不使用 DTS 封裝，它便無法訂閱發行集設為*allow_transformable_subscriptions*。 如果發行集的資料表必須複寫到 DTS 訂閱和非 DTS 訂閱，則必須建立兩個個別的發行集，每個訂閱類型各一個發行集。  
  
 選取 **sync_type** 選項 *replication support only*、 *initialize with backup*或 *initialize from lsn*時，記錄讀取器代理程式必須在執行 **sp_addsubscription**之後執行，讓設定指令碼寫入至散發資料庫。 記錄讀取器代理程式必須在屬於 **系統管理員 (sysadmin)** 固定伺服器角色成員的 Windows 帳戶底下執行。 當 **sync_type** 選項設為 *Automatic*時，不需要任何特殊的記錄讀取器代理程式動作。  
  
## <a name="permissions"></a>Permissions  
 只有系統管理員 (sysadmin) 固定伺服器角色或 db_owner 固定資料庫角色的成員，才能夠執行 sp_addsubscription。 如果是提取訂閱，使用者只要有發行集存取清單中的登入，便能夠執行 sp_addsubscription。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addsubscription-trans_1.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [為非 SQL Server 訂閱者建立訂閱](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [sp_changesubstatus &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
