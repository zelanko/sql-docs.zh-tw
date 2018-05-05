---
title: sp_addpublication (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
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
- sp_addpublication_TSQL
- sp_addpublication
helpviewer_keywords:
- sp_addpublication
ms.assetid: c7167ed1-2b7e-4824-b82b-65f4667c4407
caps.latest.revision: 69
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 59fcdcebd8c8397de2669491d4ea18cb38cfc853
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spaddpublication-transact-sql"></a>sp_addpublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立一個快照式或交易式發行集。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addpublication [ @publication = ] 'publication'  
    [ , [ @taskid = ] tasked ]  
    [ , [ @restricted = ] 'restricted' ]  
    [ , [ @sync_method = ] 'sync_method' ]  
    [ , [ @repl_freq = ] 'repl_freq' ]  
    [ , [ @description = ] 'description' ]  
    [ , [ @status = ] 'status' ]  
    [ , [ @independent_agent = ] 'independent_agent' ]  
    [ , [ @immediate_sync = ] 'immediate_sync' ]  
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]  
    [ , [ @allow_push = ] 'allow_push'  
    [ , [ @allow_pull = ] 'allow_pull' ]  
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]  
    [ , [ @allow_sync_tran = ] 'allow_sync_tran' ]  
    [ , [ @autogen_sync_procs = ] 'autogen_sync_procs' ]  
    [ , [ @retention = ] retention ]  
    [ , [ @allow_queued_tran= ] 'allow_queued_updating' ]  
    [ , [ @snapshot_in_defaultfolder= ] 'snapshot_in_default_folder' ]  
    [ , [ @alt_snapshot_folder= ] 'alternate_snapshot_folder' ]  
    [ , [ @pre_snapshot_script= ] 'pre_snapshot_script' ]  
    [ , [ @post_snapshot_script= ] 'post_snapshot_script' ]  
    [ , [ @compress_snapshot= ] 'compress_snapshot' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port= ] ftp_port ]  
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @allow_dts = ] 'allow_dts' ]  
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]  
    [ , [ @conflict_policy = ] 'conflict_policy' ]  
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @queue_type = ] 'queue_type' ]  
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]  
    [ , [ @logreader_job_name = ] 'logreader_agent_name' ]  
    [ , [ @qreader_job_name = ] 'queue_reader_agent_name' ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @allow_initialize_from_backup = ] 'allow_initialize_from_backup' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @enabled_for_p2p = ] 'enabled_for_p2p' ]  
    [ , [ @publish_local_changes_only = ] 'publish_local_changes_only' ]  
    [ , [ @enabled_for_het_sub = ] 'enabled_for_het_sub' ]  
    [ , [ @p2p_conflictdetection = ] 'p2p_conflictdetection' ]  
    [ , [ @p2p_originator_id = ] p2p_originator_id  
    [ , [ @p2p_continue_onconflict = ] 'p2p_continue_onconflict'  
    [ , [ @allow_partition_switch = ] 'allow_partition_switch'  
    [ , [ @replicate_partition_switch = ]'replicate_partition_switch'  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication=**] **'***publication***'**  
 這是要建立的發行集名稱。 *發行集*是**sysname**，沒有預設值。 這個名稱在資料庫內必須是唯一的。  
  
 [  **@taskid=**] *taskid*  
 支援; 僅限回溯相容性使用[sp_addpublication_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。  
  
 [  **@restricted=**] **'***限制***'**  
 支援; 僅限回溯相容性使用*default_access*。  
  
 [  **@sync_method=**] *' sync_method * * * '**  
 這是同步處理模式。 *sync_method*是**nvarchar(13)**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**native**|產生所有資料表的原生模式大量複製程式輸出。 *不支援 Oracle 發行者*。|  
|**character**|產生所有資料表的字元模式大量複製程式輸出。 *針對 Oracle 發行者，* **字元***只適用於快照式複寫*。|  
|**並行**|產生所有資料表的原生模式大量複製程式輸出，但在快照集期間，不鎖定資料表。 只支援交易式發行集使用這個項目。 *不支援 Oracle 發行者*。|  
|**concurrent_c**|產生所有資料表的字元模式大量複製程式輸出，但在快照集期間，不鎖定資料表。 只支援交易式發行集使用這個項目。|  
|**資料庫快照集**|從資料庫快照集產生所有資料表的原生模式大量複製程式輸出。 資料庫快照集不是每個版本都可使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。|  
|**資料庫快照集的字元**|從資料庫快照集產生所有資料表的字元模式大量複製程式輸出。 資料庫快照集不是每個版本都可使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。|  
|NULL (預設值)|預設為**原生**如[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 針對非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者，預設值為**字元**時的值*repl_freq*是**快照**和**concurrent_c**在其他情況下。|  
  
 [  **@repl_freq=**] **'***repl_freq***'**  
 這是複寫頻率的類型*repl_freq*是**nvarchar （10)**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**連續**（預設值）|發行者會提供所有記錄式交易的輸出。 針對非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者， *sync_method*設**concurrent_c**。|  
|**快照集**|發行者只會產生已排程的同步處理事件。 針對非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者， *sync_method*設**字元**。|  
  
 [  **@description=**] **'***描述***'**  
 這是發行集的選擇性描述。 *描述*是**nvarchar （255)**，預設值是 NULL。  
  
 [  **@status=**] **'***狀態***'**  
 指定發行集資料是否可用。 *狀態*是**nvarchar （8)**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**使用中**|訂閱者可以立即使用發行集資料。|  
|**非作用中**（預設值）|在最初建立發行集時，訂閱者無法使用發行集資料 (它們可以訂閱，但不會處理這些訂閱)。|  
  
 *不支援 Oracle 發行者*。  
  
 [  **@independent_agent=**] **'***independent_agent***'**  
 指定這個發行集是否有獨立的散發代理程式。 *independent_agent*是**nvarchar （5)**，預設值是 FALSE。 如果**true**，沒有獨立的散發代理程式，針對這個發行集。 如果**false**、 發行集使用共用的散發代理程式，和每一組發行者資料庫/訂閱者資料庫都有單一共用代理程式。  
  
 [  **@immediate_sync=**] **'***immediate_synchronization***'**  
 指定每次執行快照集代理程式時，是否都要建立發行集的同步處理檔案。 *immediate_synchronization*是**nvarchar （5)**，預設值是 FALSE。 如果**true**，建立或重新建立每次執行快照集代理程式同步處理檔案。 如果在建立訂閱之前，快照集代理程式已經完成，訂閱者便能夠立即取得同步處理檔案。 新的訂閱會取得最近執行快照集代理程式所產生的最新同步處理檔案。 *independent_agent*必須**true**如*immediate_synchronization*是**true**。 如果**false**，只有當有新的訂閱，會建立同步處理檔案。 您必須呼叫[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)針對每個訂閱，當您以累加方式將新的發行項加入現有的發行集。 在訂閱之後，快照集代理程式啟動和完成之前，訂閱者無法接收同步處理檔案。  
  
 [  **@enabled_for_internet=**] **'***enabled_for_internet***'**  
 指定是否啟用發行集的網際網路功能，以及決定是否能夠利用檔案傳輸通訊協定 (FTP)，將快照集檔案傳送給訂閱者。 *enabled_for_internet*是**nvarchar （5)**，預設值是 FALSE。 如果**true**，發行集的同步處理檔案會放在 C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp 目錄。 使用者必須建立這個 Ftp 目錄。  
  
 [  **@allow_push=**] **'***allow_push***'**  
 指定是否能夠針對指定的發行集建立發送訂閱。 *allow_push*是**nvarchar （5)**，預設值為 TRUE，允許發送訂閱的發行集。  
  
 [  **@allow_pull=**] **'***allow_pull***'**  
 指定是否能夠針對指定的發行集建立提取訂閱。 *allow_pull*是**nvarchar （5)**，預設值是 FALSE。 如果**false**，不允許發行集的提取訂閱。  
  
 [  **@allow_anonymous=**] **'***allow_anonymous***'**  
 指定是否能夠建立指定發行集的匿名訂閱。 *allow_anonymous*是**nvarchar （5)**，預設值是 FALSE。 如果**true**， *immediate_synchronization*也必須設定為**true**。 如果**false**，發行集不允許匿名訂閱。  
  
 [  **@allow_sync_tran=**] **'***allow_sync_tran***'**  
 指定是否允許發行集使用立即更新訂閱。 *allow_sync_tran*是**nvarchar （5)**，預設值是 FALSE。 **true**是*不支援 Oracle 發行者*。  
  
 [  **@autogen_sync_procs=**] **'***autogen_sync_procs***'**  
 指定是否在發行者端產生更新訂閱的同步處理預存程序。 *autogen_sync_procs*是**nvarchar （5)**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**true**|在啟用更新訂閱時自動設定。|  
|**false**|在不啟用更新訂閱時自動設定，或針對 Oracle 發行者來自動設定。|  
|NULL (預設值)|預設為**true**時啟用更新訂閱，並**false**更新訂用帳戶未啟用時。|  
  
> [!NOTE]  
>  使用者提供值*autogen_sync_procs*取決於指定的值將會覆寫*allow_queued_tran*和*allow_sync_tran*。  
  
 [  **@retention=**]*保留*  
 這是訂閱活動的保留週期 (以小時為單位)。 *保留*是**int**，預設值為 336 小時。 如果在保留期限內，訂閱不在使用中，它便會到期，且會被移除。 這個值可以大於發行者所用的散發資料庫的最大保留期限。 如果**0**，已知發行集的訂閱永遠不會過期，過期的訂閱清除代理程式所移除。  
  
 [  **@allow_queued_tran=** ] **'***allow_queued_updating***'**  
 啟用或停用在訂閱者端將變更放入佇列中，直到可以在發行者端套用這些變更為止。 *allow_queued_updating*是**nvarchar （5)** 預設值是 FALSE。 如果**false**，「 訂閱者 」 端的變更不會排入佇列。 **true**是*不支援 Oracle 發行者*。  
  
 [  **@snapshot_in_defaultfolder=** ] **'***snapshot_in_default_folder***'**  
 指定是否將快照集檔案儲存在預設資料夾中。 *snapshot_in_default_folder*是**nvarchar （5)** 預設值是 TRUE。 如果**true**，可以在預設資料夾中找到快照集檔案。 如果**false**，快照集檔案已儲存在所指定的替代位置*alternate_snapshot_folder*。 替代位置可以在另一部伺服器、網路磁碟機或抽取式媒體 (如 CD-ROM 或抽取式磁碟) 中。 另外，您也可以將快照集檔案儲存在 FTP 站台中，供訂閱者以後擷取它們。 請注意，這個參數可以是 true，仍有位置**@alt_snapshot_folder**參數。 這個組合會指定將快照集檔案同時儲存在預設位置和替代位置中。  
  
 [  **@alt_snapshot_folder=** ] **'***alternate_snapshot_folder***'**  
 指定快照集替代資料夾的位置。 *alternate_snapshot_folder*是**nvarchar （255)** 預設值是 NULL。  
  
 [  **@pre_snapshot_script=** ] **'***pre_snapshot_script***'**  
 指定指向 **.sql**檔案位置。 *pre_snapshot_script*是**nvarchar （255)，**預設值是 NULL。 在訂閱者端套用快照集時，散發代理程式會在執行任何複寫的物件指令碼之前，先執行前快照集 (pre-snapshot) 指令碼。 這個指令碼是在連接到訂閱資料庫時，在散發代理程式所用的安全性內容中執行。  
  
 [  **@post_snapshot_script=** ] **'***post_snapshot_script***'**  
 指定指向 **.sql**檔案位置。 *post_snapshot_script*是**nvarchar （255)**，預設值是 NULL。 在初始同步處理期間，散發代理程式會先套用所有其他複寫的物件指令碼和資料，然後才執行後快照集 (post-snapshot) 指令碼。 這個指令碼是在連接到訂閱資料庫時，在散發代理程式所用的安全性內容中執行。  
  
 [  **@compress_snapshot=** ] **'***compress_snapshot***'**  
 指定可寫入快照集**@alt_snapshot_folder**位置是壓縮成[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。 *compress_snapshot*是**nvarchar （5)**，預設值是 FALSE。 **false**指定，將不壓縮快照集;**true**指定壓縮快照集。 超出 2 GB 的快照集檔案無法壓縮。 壓縮的快照集檔案是在執行散發代理程式的位置進行解壓縮；提取訂閱通常會搭配使用壓縮的快照集，因此，會在訂閱者端將檔案解壓縮。 預設資料夾中的快照集無法壓縮。  
  
 [  **@ftp_address =** ] **'***ftp_address***'**  
 這是散發者之 FTP 服務的網路位址。 *ftp_address*是**sysname**，預設值是 NULL。 指定發行集快照集檔案所在的位置，以便訂閱者的散發代理程式或合併代理程式能夠加以收取。 因為這個屬性會儲存每個發行集，每個發行集可以有不同的*ftp_address*。 發行集必須支援利用 FTP 來傳播快照集。  
  
 [  **@ftp_port=** ] *ftp_port*  
 這是散發者的 FTP 服務通訊埠編號。 *ftp_port*是**int**，預設值為 21。 指定發行集快照集檔案所在的位置，以便訂閱者的散發代理程式或合併代理程式能夠加以收取。 因為這個屬性會儲存每個發行集，每個發行集可以有它自己*ftp_port*。  
  
 [  **@ftp_subdirectory =** ] **'***ftp_subdirectory***'**  
 指定在發行集支援利用 FTP 來傳播快照集時，供訂閱者的散發代理程式或合併代理程式從中收取快照集檔案的位置。 *ftp_subdirectory*是**nvarchar （255)**，預設值是 NULL。 因為這個屬性會儲存每個發行集，每個發行集可以有它自己*ftp_subdirctory*或是選擇將以 NULL 值的任何子目錄。  
  
 [  **@ftp_login =** ] **'***ftp_login***'**  
 這是用於連接到 FTP 服務的使用者名稱。 *ftp_login*是**sysname**，預設值為 ANONYMOUS。  
  
 [  **@ftp_password =** ] **'***ftp_password***'**  
 這是用來連接到 FTP 服務的使用者密碼。 *ftp_password*是**sysname**，預設值是 NULL。  
  
 [  **@allow_dts =** ] **'***allow_dts***'**  
 指定發行集允許資料轉換。 您可以在建立訂閱時，指定一個 DTS 封裝。 *allow_transformable_subscriptions*是**nvarchar （5)** ，預設值是 FALSE，表示不允許進行 DTS 轉換。 當*allow_dts*為 true， *sync_method*必須設定為 **字元**或**concurrent_c**。  
  
 **true**是*不支援 Oracle 發行者*。  
  
 [  **@allow_subscription_copy =** ] **'***allow_subscription_copy***'**  
 啟用或停用複製訂閱這個發行集之訂閱資料庫的能力。 *allow_subscription_copy*是**nvarchar （5)**，預設值是 FALSE。  
  
 [  **@conflict_policy =** ] **'***conflict_policy***'**  
 指定使用佇列更新訂閱者選項時，所遵照的衝突解決原則。 *conflict_policy*是**nvarchar （100)** 預設值是 NULL，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**pub wins**|發行者在衝突中獲勝。|  
|**sub reinit**|重新初始化這項訂閱。|  
|**sub wins**|訂閱者在衝突中獲勝。|  
|NULL (預設值)|如果 NULL 和發行集是快照式發行集，就會變成預設原則**sub reinit**。 如果不是快照式發行集的 NULL，且發行集，預設值會變成**pub wins**。|  
  
 *不支援 Oracle 發行者*。  
  
 [  **@centralized_conflicts =** ] **'***centralized_conflicts***'**  
 指定是否將衝突記錄儲存在發行者端： *centralized_conflicts*是**nvarchar （5)**，預設值是 TRUE。 如果**true**，衝突記錄會儲存在發行者端。 如果**false**，衝突記錄會儲存在發行者端和造成衝突的訂閱者端。 *不支援 Oracle 發行者*。  
  
 [  **@conflict_retention =** ] *conflict_retention*  
 指定衝突保留週期 (以天為單位)。 這是針對點對點異動複寫和佇列更新訂閱儲存衝突中繼資料的時間週期。 *conflict_retention*是**int**，預設值為 14。 *不支援 Oracle 發行者*。  
  
 [  **@queue_type =** ] **'***類型***'**  
 指定所用的佇列類型。 *類型*是**nvarchar （10)**，預設值是 NULL，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**sql**|利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來儲存交易。|  
|NULL (預設值)|預設為**sql**，其中指定要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]來儲存交易。|  
  
> [!NOTE]  
>  已不再支援使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing。 指定的值是**msmq**會產生警告，並複寫會自動將值設為**sql**。  
  
 *不支援 Oracle 發行者*。  
  
 [  **@add_to_active_directory =** ] **' * * * 新增**_**to_active_directory * * * '**  
 這個參數已被取代，支援它的目的，只是為了與舊版的指令碼相容。 您不能再將發行集資訊加入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中。  
  
 [  **@logreader_job_name =** ] **'***logreader_agent_name***'**  
 這是現有散發代理程式作業的名稱。 *logreader_agent_name*是**sysname**，預設值是 NULL。 只有在記錄讀取器代理程式將使用現有的作業，而不建立新的作業時，才指定這個參數。  
  
 [  **@qreader_job_name =** ] **'***queue_reader_agent_name***'**  
 這是現有散發代理程式作業的名稱。 *queue_reader_agent_name*是**sysname**，預設值是 NULL。 只有在佇列讀取器代理程式將使用現有的作業，而不建立新的作業時，才指定這個參數。  
  
 [  **@publisher =** ] **'***發行者***'**  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *發行者*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應加入至發行集時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
 [  **@allow_initialize_from_backup =** ] **'***allow_initialize_from_backup***'**  
 指出訂閱者是否能夠從備份中，而不是從初始快照集中，對這個發行集的訂閱進行初始化。 *allow_initialize_from_backup*是**nvarchar （5)**，而且可以是下列值之一：  
  
|Value|Description|  
|-----------|-----------------|  
|**true**|啟用從備份進行的初始化。|  
|**false**|停用從備份進行的初始化。|  
|NULL (預設值)|預設為**true**內對等複寫拓撲的發行集和**false**所有其他發行集。|  
  
 如需詳細資訊，請參閱 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。  
  
> [!WARNING]  
>  為了避免遺漏訂閱者資料，當您使用 **sp_addpublication** 搭配 `@allow_initialize_from_backup = N'true'`時，請一律使用 `@immediate_sync = N'true'`。  
  
 [  **@replicate_ddl =** ] *replicate_ddl*  
 指出是否支援發行集的結構描述複寫。 *replicate_ddl*是**int**，預設值是**1**如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者和**0**的非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 **1**表示複寫在發行者端執行的資料定義語言 (DDL) 陳述式，和**0**表示不複寫 DDL 陳述式。 *不支援 Oracle 發行者的結構描述複寫。* 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
 *@replicate_ddl* DDL 陳述式將資料行時，會接受一個參數。 *@replicate_ddl* DDL 陳述式改變或卸除資料行，基於下列原因時，參數會被忽略。  
  
-   卸除資料行後，必須更新 sysarticlecolumns，以避免新的 DML 陳述式包括已卸除資料行而造成散發代理程式失敗。 *@replicate_ddl*參數會被忽略，因為複寫作業一定要複寫結構描述變更。  
  
-   當更改資料行時，來源資料類型或 Null 屬性可能已變更，造成 DML 陳述式包含的值可能與散發者端的資料表不相容。 這類 DML 陳述式可能會造成散發代理程式失敗。 *@replicate_ddl*參數會被忽略，因為複寫作業一定要複寫結構描述變更。  
  
-   Sysarticlecolumns DDL 陳述式加入新的資料行，不包括新的資料行。 DML 陳述式不會嘗試複寫新資料行的資料。 接受此參數是因為可接受複寫或不複寫 DDL。  
  
 [  **@enabled_for_p2p =** ] **'***enabled_for_p2p***'**  
 使點對點複寫拓撲能夠使用發行集。 *enabled_for_p2p*是**nvarchar （5)**，預設值是 FALSE。 **true**表示發行集支援端對端複寫。 設定時*enabled_for_p2p*至**true**，適用下列限制：  
  
-   *allow_anonymous*必須**false**。  
  
-   *allow_dts*必須**false**。  
  
-   *allow_initialize_from_backup*必須**true**。  
  
-   *allow_queued_tran*必須**false**。  
  
-   *allow_sync_tran*必須**false**。  
  
-   *conflict_policy*必須**false**。  
  
-   *independent_agent*必須**true**。  
  
-   *repl_freq*必須**連續**。  
  
-   *replicate_ddl*必須**1**。  
  
 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 [  **@publish_local_changes_only =** ] **'***publish_local_changes_only***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@enabled_for_het_sub=** ] **'***enabled_for_het_sub***'**  
 啟用發行集以支援非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。 *enabled_for_het_sub*是**nvarchar （5)** 預設值是 FALSE。 值為**true**表示發行集支援非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]「 訂閱者 」。 當*enabled_for_het_sub*是**true**，適用下列限制：  
  
-   *allow_initialize_from_backup*必須**false**。  
  
-   *allow_push*必須**true**。  
  
-   *allow_queued_tran*必須**false**。  
  
-   *allow_subscription_copy*必須**false**。  
  
-   *allow_sync_tran*必須**false**。  
  
-   *autogen_sync_procs*必須**false**。  
  
-   *conflict_policy*必須是 NULL。  
  
-   *enabled_for_internet*必須**false**。  
  
-   *enabled_for_p2p*必須**false**。  
  
-   *ftp_address*必須是 NULL。  
  
-   *ftp_subdirectory*必須是 NULL。  
  
-   *ftp_password*必須是 NULL。  
  
-   *pre_snapshot_script*必須是 NULL。  
  
-   *post_snapshot_script*必須是 NULL。  
  
-   *replicate_ddl*必須是 0。  
  
-   *qreader_job_name*必須是 NULL。  
  
-   *類型*必須是 NULL。  
  
-   *sync_method*不可**原生**或**並行**。  
  
 如需詳細資訊，請參閱 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。  
  
 [  **@p2p_conflictdetection=** ] **'***p2p_conflictdetection***'**  
 如果發行集啟用點對點複寫，便讓散發代理程式偵測衝突。 *p2p_conflictdetection*是**nvarchar （5)** 預設值為 true。 如需詳細資訊，請參閱 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。  
  
 [  **@p2p_originator_id=** ] *p2p_originator_id*  
 針對點對點拓撲中的節點指定識別碼。 *p2p_originator_id*是**int**，預設值是 NULL。 此識別碼用於衝突偵測，如果*p2p_conflictdetection*設為 TRUE。 請指定拓撲中從未使用過的非零正數識別碼。 對於已經使用的識別碼清單，請執行[sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md)。  
  
 [  **@p2p_continue_onconflict=** ] **'***p2p_continue_onconflict***'**  
 決定散發代理程式在偵測到衝突之後是否會繼續處理變更。 *p2p_continue_onconflict*是**nvarchar （5)** 預設值是 FALSE。  
  
> [!CAUTION]  
>  我們建議您使用預設值 FALSE。 當這個選項設定為 TRUE 時，散發代理程式會套用具有最高訂閱者識別碼之節點的衝突資料列，藉以嘗試聚合拓撲中的資料。 但是，這個方法無法保證聚合。 您應該確定在偵測到衝突之後，拓撲是一致的。 如需詳細資訊，請參閱＜ [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)＞中的「處理衝突」。  
  
 [  **@allow_partition_switch=** ] **'***allow_partition_switch***'**  
 指定 ALTER TABLE…SWITCH 陳述式是否可以針對發行的資料庫來執行。 *allow_partition_switch*是**nvarchar （5)** 預設值是 FALSE。 如需詳細資訊，請參閱[複寫資料分割資料表及索引](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。  
  
 [  **@replicate_partition_switch=** ] **'***replicate_partition_switch***'**  
 指定針對發行資料庫執行的 ALTER TABLE…SWITCH 陳述式是否應該複寫到訂閱者。 *replicate_partition_switch*是**nvarchar （5)** 預設值是 FALSE。 這個選項才有效才*allow_partition_switch*設為 TRUE。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addpublication**用於快照式複寫和異動複寫。  
  
 如果存在多個發行集的發行相同的資料庫物件，使用的發行集*replicate_ddl*值**1** ALTER TABLE、 ALTER VIEW、 ALTER PROCEDURE、 ALTER FUNCTION，將複寫和ALTER TRIGGER DDL 陳述式。 不過，所有發行已卸除之資料行的發行集都會複寫 ALTER TABLE DROP COLUMN DDL 陳述式。  
  
 啟用 DDL 複寫 (*replicate_ddl* = **1**) 是發行集，為了進行非複寫 DDL 變更發行集， [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)設定必須先執行*replicate_ddl*至**0**。 在發出非複寫 DDL 陳述式之後， [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)可以再次執行才能重新開啟 DDL 複寫。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-transa_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addpublication**。 Windows 驗證登入必須擁有代表其 Windows 使用者帳戶的資料庫使用者帳戶。 代表 Windows 群組的使用者帳戶權限不足。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addlogreader_agent &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_addpublication_snapshot &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [sp_replicationdboption &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
