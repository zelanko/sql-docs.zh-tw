---
title: sp_addmergepublication （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepublication
- sp_addmergepublication_TSQL
helpviewer_keywords:
- sp_addmergepublication
ms.assetid: 28a629a1-7374-4614-9b04-279d290a942a
author: stevestein
ms.author: sstein
ms.openlocfilehash: a296f5b4cb20768d5aa244646e584bede110d26a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "72278357"
---
# <a name="sp_addmergepublication-transact-sql"></a>sp_addmergepublication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  建立新的合併式發行集。 這個預存程序執行於所發行之資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addmergepublication [ @publication = ] 'publication'   
    [ , [ @description = ] 'description'   
    [ , [ @retention = ] retention ]   
    [ , [ @sync_mode = ] 'sync_mode' ]   
    [ , [ @allow_push = ] 'allow_push' ]   
    [ , [ @allow_pull = ] 'allow_pull' ]   
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]   
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]   
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @dynamic_filters = ] 'dynamic_filters' ]   
    [ , [ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder' ]   
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @pre_snapshot_script = ] 'pre_snapshot_script' ]   
    [ , [ @post_snapshot_script = ] 'post_snapshot_script' ]   
    [ , [ @compress_snapshot = ] 'compress_snapshot' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]   
    [ , [ @conflict_retention = ] conflict_retention ]   
    [ , [ @keep_partition_changes = ] 'keep_partition_changes' ]   
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]   
    [ , [ @allow_synctoalternate = ] 'allow_synctoalternate' ]   
    [ , [ @validate_subscriber_info = ] 'validate_subscriber_info' ]   
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]   
    [ , [ @max_concurrent_merge = ] maximum_concurrent_merge ]   
    [ , [ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots ]  
    [ , [ @use_partition_groups = ] 'use_partition_groups' ]  
    [ , [ @publication_compatibility_level = ] 'backward_comp_level' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot' ]   
    [ , [ @allow_web_synchronization = ] 'allow_web_synchronization' ]   
    [ , [ @web_synchronization_url = ] 'web_synchronization_url' ]  
    [ , [ @allow_partition_realignment = ] 'allow_partition_realignment' ]  
    [ , [ @retention_period_unit = ] 'retention_period_unit' ]  
    [ , [ @generation_leveling_threshold = ] generation_leveling_threshold ]  
    [ , [ @automatic_reinitialization_policy = ] automatic_reinitialization_policy ]  
    [ , [ @conflict_logging = ] 'conflict_logging' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是要建立的合併式發行集名稱。 *發行*集是**sysname**，沒有預設值，而且不能是關鍵字 ALL。 在資料庫內，發行集名稱必須是唯一的。  
  
`[ @description = ] 'description'`這是發行集的描述。 *description*是**Nvarchar （255）**，預設值是 Null。  
  
`[ @retention = ] retention`這是要儲存給定*發行*集之變更的保留週期（以保留週期單位表示）。 *保留*是**int**，預設值是14個單位。 保留週期單位是由*retention_period_unit*所定義。 如果未在保留期限內同步處理訂閱，且散發者端的清除作業移除了它已收到的暫止變更，訂閱便會到期，必須重新初始化。 最大的允許保留期限是目前的日期到 9999 年 12 月 31 日之間的天數。  
  
> [!NOTE]  
>  合併式發行集的保留期限有 24 小時的寬限期，以便配合不同時區的訂閱者。 例如，如果您設定的保留期限是一天，實際的保留期限便是 48 小時。  
  
`[ @sync_mode = ] 'sync_mode'`這是發行集訂閱者的初始同步處理模式。 *sync_mode*是**Nvarchar （10）**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**native** （預設值）|產生所有資料表的原生模式大量複製程式輸出。|  
|**字母**|產生所有資料表的字元模式大量複製程式輸出。 支援[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]和非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者所需。|  
  
`[ @allow_push = ] 'allow_push'`指定是否可以針對指定的發行集建立發送訂閱。 *allow_push*是**Nvarchar （5）**，預設值為 TRUE，允許發行集的發送訂閱。  
  
`[ @allow_pull = ] 'allow_pull'`指定是否可以針對指定的發行集建立提取訂閱。 *allow_pull*是**Nvarchar （5）**，預設值為 TRUE，允許發行集的提取訂閱。 您必須指定 true 才能支援[!INCLUDE[ssEW](../../includes/ssew-md.md)]訂閱者。  
  
`[ @allow_anonymous = ] 'allow_anonymous'`指定是否可以針對指定的發行集建立匿名訂閱。 *allow_anonymous*是**Nvarchar （5）**，預設值為 TRUE，允許發行集的匿名訂閱。 若要[!INCLUDE[ssEW](../../includes/ssew-md.md)]支援訂閱者，您必須指定**true**。  
  
`[ @enabled_for_internet = ] 'enabled_for_internet'`指定是否為網際網路啟用發行集，並決定是否可以使用檔案傳輸協定（FTP）將快照集檔案傳送至訂閱者。 *enabled_for_internet*是**Nvarchar （5）**，預設值是 FALSE。 如果**為 true**，則發行集的同步處理檔案會放在 C:\PROGRAM Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp 目錄中。 使用者必須建立這個 Ftp 目錄。 如果為**false**，則表示發行集未啟用網際網路存取。  
  
`[ @centralized_conflicts = ] 'centralized_conflicts'`這個參數已被取代，而且僅支援腳本的回溯相容性。 使用*conflict_logging*來指定儲存衝突記錄的位置。  
  
`[ @dynamic_filters = ] 'dynamic_filters'`讓合併式發行集使用參數化資料列篩選器。 *dynamic_filters*是**Nvarchar （5）**，預設值是 FALSE。  
  
> [!NOTE]  
>  您不應該指定這個參數，而應允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自動判斷是否正在使用參數化資料列篩選器。 如果您針對*dynamic_filters*指定**true**的值，則必須為發行項定義參數化資料列篩選器。 如需詳細資訊，請參閱 [針對合併發行項定義及修改參數化資料列篩選](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
`[ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder'`指定是否將快照集檔案儲存在預設資料夾中。 *snapshot_in_default_folder*是**Nvarchar （5）**，預設值是 TRUE。 若**為 true**，則可以在預設資料夾中找到快照集檔案。 如果**為 false**，則快照集檔案會儲存在*alternate_snapshot_folder*所指定的替代位置中。 替代位置可以在另一部伺服器、網路磁碟機或抽取式媒體 (如 CD-ROM 或抽取式磁碟) 中。 另外，您也可以將快照集檔案儲存在檔案傳輸通訊協定 (FTP) 網站中，供訂閱者以後擷取它們。 請注意，這個參數可以是 true，而且仍然具有*alt_snapshot_folder*所指定的位置。 這個組合會指定將快照集檔案同時儲存在預設位置和替代位置中。  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'`指定快照集替代資料夾的位置。 *alternate_snapshot_folder*是**Nvarchar （255）**，預設值是 Null。  
  
`[ @pre_snapshot_script = ] 'pre_snapshot_script'`指定 **.sql**檔案位置的指標。 *pre_snapshot_script*是**Nvarchar （255）**，預設值是 Null。 在訂閱者端套用快照集時，合併代理程式會在任何複寫的物件指令碼之前，先執行前快照集 (Pre-snapshot) 指令碼。 這個指令碼是在連接到訂閱資料庫時，在合併代理程式所用的安全性內容中執行。 預先快照集腳本不會在訂閱[!INCLUDE[ssEW](../../includes/ssew-md.md)]者上執行。  
  
`[ @post_snapshot_script = ] 'post_snapshot_script'`指定 **.sql**檔案位置的指標。 *post_snapshot_script*是**Nvarchar （255）**，預設值是 Null。 在初始同步處理期間，合併代理程式會先套用所有其他複寫的物件指令碼和資料，然後才執行後快照集 (Post-snapshot) 指令碼。 這個指令碼是在連接到訂閱資料庫時，在合併代理程式所用的安全性內容中執行。 後快照集腳本不會在訂閱[!INCLUDE[ssEW](../../includes/ssew-md.md)]者上執行。  
  
`[ @compress_snapshot = ] 'compress_snapshot'`指定要將寫入** \@alt_snapshot_folder**位置的快照集壓縮成[!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 格式。 *compress_snapshot*是**Nvarchar （5）**，預設值是 FALSE。 **false**指定不壓縮快照集;**true**指定要壓縮快照集。 超出 2GB 的快照集檔案無法壓縮。 壓縮的快照集檔案是在執行合併代理程式的位置進行解壓縮；提取訂閱通常會搭配使用壓縮的快照集，因此，會在訂閱者端將檔案解壓縮。 預設資料夾中的快照集無法壓縮。 若要[!INCLUDE[ssEW](../../includes/ssew-md.md)]支援訂閱者，您必須指定**false**。  
  
`[ @ftp_address = ] 'ftp_address'`這是散發者之 FTP 服務的網路位址。 *ftp_address*是**sysname**，預設值是 Null。 指定發行集快照集檔案所在的位置，以便訂閱者的合併代理程式能夠加以收取。 由於每個發行集都會儲存這個屬性，因此每個發行集都可以有不同的*ftp_address*。 發行集必須支援利用 FTP 來傳播快照集。  
  
`[ @ftp_port = ] ftp_port`這是散發者之 FTP 服務的通訊埠編號。 *ftp_port*是**int**，預設值是21。 指定發行集快照集檔案所在的位置，以便訂閱者的合併代理程式能夠加以收取。 因為每個發行集都會儲存這個屬性，所以每個發行集都可以有自己的*ftp_port*。  
  
`[ @ftp_subdirectory = ] 'ftp_subdirectory'`指定在發行集支援使用 FTP 來傳播快照集時，訂閱者的合併代理程式可以挑選快照集檔案的位置。 *ftp_subdirectory*是**Nvarchar （255）**，預設值是 Null。 由於每個發行集都會儲存這個屬性，因此，每個發行集都可以有自己的*ftp_subdirctory*或選擇沒有任何子目錄，並以 Null 值表示。  
  
 當利用參數化篩選來預先產生快照集時，每個訂閱者分割區的資料快照集都必須在它自己的資料夾中。 利用 FTP 預先產生快照集，其目錄結構必須遵照下列結構：  
  
 *alternate_snapshot_folder*\ftp\\*publisher_publicationDB_publication*\\*partitionID*。  
  
> [!NOTE]  
>  上述斜體值會隨著發行集和訂閱者分割區的細節而不同。  
  
`[ @ftp_login = ] 'ftp_login'`這是用來連接到 FTP 服務的使用者名稱。 *ftp_login*是**sysname**，預設值為 ' anonymous '。  
  
`[ @ftp_password = ] 'ftp_password'`這是用來連接到 FTP 服務的使用者密碼。 *ftp_password*是**sysname**，預設值是 Null。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。  
  
`[ @conflict_retention = ] conflict_retention`指定保留衝突的保留期限（以天為單位）。 *conflict_retention*是**int**，預設值是14天，然後才會從衝突資料表中清除衝突資料列。  
  
`[ @keep_partition_changes = ] 'keep_partition_changes'`指定當無法使用預先計算的分割區時，是否要啟用資料分割變更優化。 *keep_partition_changes*是**Nvarchar （5）**，預設值是 TRUE。 **false**表示不會優化分割區變更，而且不使用預先計算的資料分割時，傳送至所有訂閱者的分割區會在資料分割中變更時進行驗證。 **true**表示資料分割變更已優化，而且只有在已變更之分割區中具有資料列的訂閱者會受到影響。 使用預先計算的資料分割時，請將*use_partition_groups*設定為**true** ，並將*keep_partition_changes*設定為**false**。 如需詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
> [!NOTE]  
>  如果您為*keep_partition_changes*指定**true**的值，請為快照集代理程式參數指定**1**的值 **-MaxNetworkOptimization**。 如需此參數的詳細資訊，請參閱[Replication 快照集代理程式](../../relational-databases/replication/agents/replication-snapshot-agent.md)。 如需如何指定代理程式參數的詳細資訊，請參閱複寫[代理程式管理](../../relational-databases/replication/agents/replication-agent-administration.md)。  
  
 若[!INCLUDE[ssEW](../../includes/ssew-md.md)]為訂閱者， *keep_partition_changes*必須設定為 true，才能確保正確傳播刪除。 設為 false 時，訂閱者所擁有的資料列可能比預期多。  
  
`[ @allow_subscription_copy = ] 'allow_subscription_copy'`啟用或停用複製訂閱這個發行集之訂閱資料庫的能力。 *allow_subscription_copy*是**Nvarchar （5）**，預設值是 FALSE。 所複製的訂閱資料庫大小必須小於 2 GB。  
  
`[ @allow_synctoalternate = ] 'allow_synctoalternate'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @validate_subscriber_info = ] 'validate_subscriber_info'`列出使用參數化資料列篩選器時，用來定義已發行資料之訂閱者資料分割的函數。 *validate_subscriber_info*是**Nvarchar （500）**，預設值是 Null。 合併代理程式利用這項資訊來驗證訂閱者的分割區。 例如，如果在參數化資料列篩選器中使用[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) ，則參數應`@validate_subscriber_info=N'SUSER_SNAME()'`為。  
  
> [!NOTE]  
>  您不應該指定這個參數，而應允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自動判斷篩選準則。  
  
`[ @add_to_active_directory = ] 'add_to_active_directory'`這個參數已被取代，而且僅支援腳本的回溯相容性。 您不能再將發行集資訊加入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中。  
  
`[ @max_concurrent_merge = ] maximum_concurrent_merge`並行合併進程的最大數目。 *maximum_concurrent_merge*是**int** ，預設值是0。 這個屬性的值為**0**時，表示在任何給定時間執行的並行合併進程數目沒有限制。 這個屬性會設定能夠針對合併式發行集來同時執行的並行合併處理序的數目限制。 如果排程同時執行的合併處理序數目超出允許執行的值，超出的作業便會放在佇列中，等到目前在執行中的合併處理序完成為止。  
  
`[ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots`可以同時執行的快照集代理程式會話數目上限，以產生訂閱者分割區的已篩選資料快照集。 *maximum_concurrent_dynamic_snapshots*是**int** ，預設值是0。 如果是**0**，表示快照集會話數目沒有限制。 如果排程同時執行的快照集處理序數目超出允許執行的值，超出的作業便會放在佇列中，等到目前在執行中的快照集處理序完成為止。  
  
`[ @use_partition_groups = ] 'use_partition_groups'`指定應該使用預先計算的資料分割來優化同步處理常式。 *use_partition_groups*是**Nvarchar （5）**，它可以是下列其中一個值：  
  
|值|描述|  
|-----------|-----------------|  
|**true**|發行集使用預先計算的資料分割。|  
|**false**|發行集不使用預先計算的資料分割。|  
|Null （預設值）|系統決定資料分割策略。|  
  
 依預設，會使用預先計算的分割區。 若要避免使用預先計算的資料分割， *use_partition_groups*必須設定為**false**。 當設為 NULL 時，系統會決定能不能使用預先計算的分割區。 如果無法使用預先計算的資料分割，則這個值實際上會變成**false** ，而不會產生任何錯誤。 在這種情況下， *keep_partition_changes*可以設定為**true** ，以提供一些優化。 如需詳細資訊，請參閱[參數化資料列篩選器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)和[使用預先計算的資料分割優化參數化篩選效能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
`[ @publication_compatibility_level = ] backward_comp_level`指出發行集的回溯相容性。 *backward_comp_level*是**Nvarchar （6）**，而且可以是下列其中一個值：  
  
|值|版本|  
|-----------|-------------|  
|**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
  
`[ @replicate_ddl = ] replicate_ddl`指出是否支援發行集的架構複寫。 *replicate_ddl*是**int**，預設值是1。 **1**表示複寫在發行者端執行的資料定義語言（ddl）語句， **0**表示不復寫 DDL 語句。 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
 當* \@ * ddl 語句加入資料行時，就會接受 replicate_ddl 參數。 當* \@ * ddl 語句因下列原因而改變或卸載資料行時，會忽略 replicate_ddl 參數。  
  
-   當卸除資料行時必須更新 sysarticlecolumns，以免新的 DML 陳述式包含造成散發代理程式失敗的已卸除資料行。 因為複寫必須一律複寫架構變更，所以會忽略* \@replicate_ddl*參數。  
  
-   當更改資料行時，來源資料類型或 Null 屬性可能已變更，造成 DML 陳述式包含的值可能與散發者端的資料表不相容。 這類 DML 陳述式可能會造成散發代理程式失敗。 因為複寫必須一律複寫架構變更，所以會忽略* \@replicate_ddl*參數。  
  
-   當 DDL 陳述式加入新的資料行時，sysarticlecolumns 不包括新的資料行。 DML 陳述式不會嘗試複寫新資料行的資料。 接受此參數是因為可接受複寫或不複寫 DDL。  
  
`[ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot'`指出此發行集的訂閱者是否可以起始快照集進程，為其資料分割產生篩選的快照集。 *allow_subscriber_initiated_snapshot*是**Nvarchar （5）**，預設值是 FALSE。 **true**表示訂閱者可以起始快照集進程。  
  
`[ @allow_web_synchronization = ] 'allow_web_synchronization'`指定發行集是否已啟用 Web 同步處理。 *allow_web_synchronization*是**Nvarchar （5）**，預設值是 FALSE。 **true**指定可以透過 HTTPS 來同步處理這個發行集的訂閱。 如需詳細資訊，請參閱＜ [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)＞。 若要[!INCLUDE[ssEW](../../includes/ssew-md.md)]支援訂閱者，您必須指定**true**。  
  
`[ @web_synchronization_url = ] 'web_synchronization_url'`指定 Web 同步處理所用的網際網路 URL 預設值。 *web_synchronization_url i*s **Nvarchar （500）**，預設值是 Null。 定義預設的網際網路 URL （如果未在執行[sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)時明確設定的話）。  
  
`[ @allow_partition_realignment = ] 'allow_partition_realignment'`決定當修改發行者上的資料列使其變更其資料分割時，是否要將刪除傳送至訂閱者。 *allow_partition_realignment*是**Nvarchar （5）**，預設值是 TRUE。 **true**會將刪除動作傳送至訂閱者，藉由移除不再屬於訂閱者分割區的資料，來反映分割區變更的結果。 **false**會將舊分割區的資料保留在訂閱者端，而在發行者端對此資料所做的變更將不會複寫到這個訂閱者，但在訂閱者上所做的變更將會複寫到發行者。 將*allow_partition_realignment*設定為**false** ，會在資料需要可供歷程記錄之用時，用來將資料保留在舊分割區的訂用帳戶中。  
  
> [!NOTE]  
>  將*allow_partition_realignment*設定為**false**時，保留在訂閱者端的資料應該視為唯讀;不過，複寫系統並不會強制執行這項工作。  
  
`[ @retention_period_unit = ] 'retention_period_unit'`指定*保留*期間所設定之保留期限的單位。 *retention_period_unit*是**Nvarchar （10）**，而且可以是下列其中一個值。  
  
|值|版本|  
|-----------|-------------|  
|**day** （預設值）|以天為保留週期的指定單位。|  
|**week**|以星期為保留週期的指定單位。|  
|**month**|以月為保留週期的指定單位。|  
|**year**|以年為保留週期的指定單位。|  
  
`[ @generation_leveling_threshold = ] generation_leveling_threshold`指定層代中包含的變更數目。 層代是指傳遞給發行者或訂閱者的變更集合。 *generation_leveling_threshold*是**int**，預設值是1000。  
  
`[ @automatic_reinitialization_policy = ] automatic_reinitialization_policy`指定在變更發行集之前，是否從訂閱者上傳變更，其中已針對** \@force_reinit_subscription**指定**1**的值。 *automatic_reinitialization_policy*是 bit，預設值是0。 **1**表示在自動重新初始化之前，會從訂閱者上傳變更。  
  
> [!IMPORTANT]  
>  如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
`[ @conflict_logging = ] 'conflict_logging'`指定衝突記錄的儲存位置。 *conflict_logging*是**Nvarchar （15）**，而且可以是下列其中一個值：  
  
|值|描述|  
|-----------|-----------------|  
|**發行者**|衝突記錄會儲存在發行者端。|  
|**預訂**|衝突記錄會儲存在造成衝突的訂閱者端。 不支援 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者。|  
|**既**|衝突記錄會儲存在發行者端和訂閱者端。|  
|NULL (預設值)|當值*backward_comp_level*為**90rtm**時，複寫會自動將*conflict_logging*設定為，而在所有其他情況下則會**設為「** **發行者**」。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addmergepublication**用於合併式複寫中。  
  
 若要使用** \@add_to_active_directory**參數列出 Active Directory 中的發行集物件， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件必須已在 Active Directory 中建立。  
  
 如果有多個發行集發行相同的資料庫物件，只有*replicate_ddl*值為**1**的發行集，才會複寫 ALTER TABLE、ALTER VIEW、ALTER PROCEDURE、ALTER FUNCTION 和 ALTER TRIGGER ddl 語句。 不過，所有發行已卸除之資料行的發行集都會複寫 ALTER TABLE DROP COLUMN DDL 陳述式。  
  
 對於[!INCLUDE[ssEW](../../includes/ssew-md.md)]訂閱者而言，只有在*snapshot_in_default_folder*的值為**false**時，才會使用*alternate_snapshot_folder*的值。  
  
 在啟用發行集的 DDL 複寫（_replicate_ddl_**= 1**）時，為了進行發行集的非複寫 ddl 變更，必須先執行[sp_changemergepublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) ，將*replicate_ddl*設定為**0**。 在發出非複寫 DDL 語句之後，您可以再次執行**sp_changemergepublication**來重新開啟 DDL 複寫。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddMergePub](../../relational-databases/replication/codesnippet/tsql/sp-addmergepublication-t_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_addmergepublication**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [sp_changemergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
