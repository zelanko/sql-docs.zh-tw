---
title: "sp_addmergepublication (TRANSACT-SQL) |Microsoft 文件"
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
- sp_addmergepublication
- sp_addmergepublication_TSQL
helpviewer_keywords: sp_addmergepublication
ms.assetid: 28a629a1-7374-4614-9b04-279d290a942a
caps.latest.revision: "72"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b3f61d6ab3c2154020be3eb1ecf4407f57541918
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spaddmergepublication-transact-sql"></a>sp_addmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [  **@publication =** ] **'***發行集***'**  
 這是要建立之合併式發行集的名稱。 *發行集*是**sysname**，沒有預設值，而且不能是關鍵字所有。 在資料庫內，發行集名稱必須是唯一的。  
  
 [  **@description =** ] **'***描述***'**  
 這是發行集的描述。 *描述*是**nvarchar （255)**，預設值是 NULL。  
  
 [  **@retention =** ]*保留*  
 會保留期限，以保留週期單位，這是要儲存變更給定*發行集*。 *保留*是**int**，預設值是 14 個單位。 保留週期單位由定義*retention_period_unit*。 如果未在保留期限內同步處理訂閱，且散發者端的清除作業移除了它已收到的暫止變更，訂閱便會到期，必須重新初始化。 最大的允許保留期限是目前的日期到 9999 年 12 月 31 日之間的天數。  
  
> [!NOTE]  
>  合併式發行集的保留期限有 24 小時的寬限期，以便配合不同時區的訂閱者。 例如，如果您設定的保留期限是一天，實際的保留期限便是 48 小時。  
  
 [  **@sync_mode =** ] **'***sync_mode***'**  
 這是發行集訂閱者的初始同步處理模式。 *sync_mode*是**nvarchar （10)**，而且可以是下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**原生**（預設值）|產生所有資料表的原生模式大量複製程式輸出。|  
|**字元**|產生所有資料表的字元模式大量複製程式輸出。 支援所需[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssEW](../../includes/ssew-md.md)]和非-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 「 訂閱者 」。|  
  
 [  **@allow_push =** ] **'***allow_push***'**  
 指定是否能夠針對指定的發行集建立發送訂閱。 *allow_push*是**nvarchar （5)**，預設值為 TRUE，允許發送訂閱的發行集。  
  
 [  **@allow_pull =** ] **'***allow_pull***'**  
 指定是否能夠針對指定的發行集建立提取訂閱。 *allow_pull*是**nvarchar （5)**，預設值為 TRUE，允許提取訂閱的發行集上。 您必須指定 true 來支援[!INCLUDE[ssEW](../../includes/ssew-md.md)]「 訂閱者 」。  
  
 [  **@allow_anonymous =** ] **'***allow_anonymous***'**  
 指定是否能夠建立指定發行集的匿名訂閱。 *allow_anonymous*是**nvarchar （5)**，預設值為 TRUE，允許匿名訂閱發行集。 若要支援[!INCLUDE[ssEW](../../includes/ssew-md.md)]訂閱者，您必須指定**true**。  
  
 [  **@enabled_for_internet =** ] **'***enabled_for_internet***'**  
 指定是否啟用發行集的網際網路功能，以及決定是否能夠利用檔案傳輸通訊協定 (FTP)，將快照集檔案傳送給訂閱者。 *enabled_for_internet*是**nvarchar （5)**，預設值是 FALSE。 如果**true**，發行集的同步處理檔案會放在 C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp 目錄。 使用者必須建立這個 Ftp 目錄。 如果**false**，發行集未啟用的網際網路存取。  
  
 [  **@centralized_conflicts =**] **'***centralized_conflicts***'**  
 這個參數已被取代，支援它的目的，只是為了與舊版的指令碼相容。 使用*conflict_logging*來指定衝突記錄儲存的位置。  
  
 [  **@dynamic_filters =**] **'***dynamic_filters***'**  
 使合併式發行集能夠使用參數化資料列篩選器。 *dynamic_filters*是**nvarchar （5)**，預設值是 FALSE。  
  
> [!NOTE]  
>  您不應該指定這個參數，而應允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自動判斷是否正在使用參數化資料列篩選器。 如果您指定的值**true**如*dynamic_filters*，您必須定義發行項的參數化資料列篩選。 如需詳細資訊，請參閱 [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
 [  **@snapshot_in_defaultfolder =** ] **'***snapshot_in_default_folder***'**  
 指定是否將快照集檔案儲存在預設資料夾中。 *snapshot_in_default_folder*是**nvarchar （5)**，預設值是 TRUE。 如果**true**，可以在預設資料夾中找到快照集檔案。 如果**false**，快照集檔案會儲存在所指定的替代位置*alternate_snapshot_folder*。 替代位置可以在另一部伺服器、網路磁碟機或抽取式媒體 (如 CD-ROM 或抽取式磁碟) 中。 另外，您也可以將快照集檔案儲存在檔案傳輸通訊協定 (FTP) 網站中，供訂閱者以後擷取它們。 請注意，這個參數可以是 true，仍有指定的位置*alt_snapshot_folder*。 這個組合會指定將快照集檔案同時儲存在預設位置和替代位置中。  
  
 [  **@alt_snapshot_folder =** ] **'***alternate_snapshot_folder***'**  
 指定快照集替代資料夾的位置。 *alternate_snapshot_folder*是**nvarchar （255)**，預設值是 NULL。  
  
 [  **@pre_snapshot_script =** ] **'***pre_snapshot_script***'**  
 指定指向**.sql**檔案位置。 *pre_snapshot_script*是**nvarchar （255)**，預設值是 NULL。 在訂閱者端套用快照集時，合併代理程式會在任何複寫的物件指令碼之前，先執行前快照集 (Pre-snapshot) 指令碼。 這個指令碼是在連接到訂閱資料庫時，在合併代理程式所用的安全性內容中執行。 前快照集指令碼並非執行於[!INCLUDE[ssEW](../../includes/ssew-md.md)]「 訂閱者 」。  
  
 [  **@post_snapshot_script =** ] **'***post_snapshot_script***'**  
 指定指向**.sql**檔案位置。 *post_snapshot_script*是**nvarchar （255)**，預設值是 NULL。 在初始同步處理期間，合併代理程式會先套用所有其他複寫的物件指令碼和資料，然後才執行後快照集 (Post-snapshot) 指令碼。 這個指令碼是在連接到訂閱資料庫時，在合併代理程式所用的安全性內容中執行。 後快照集指令碼並非執行於[!INCLUDE[ssEW](../../includes/ssew-md.md)]「 訂閱者 」。  
  
 [  **@compress_snapshot =** ] **'***compress_snapshot***'**  
 指定可寫入快照 **@alt_snapshot_folder** 位置是壓縮成[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。 *compress_snapshot*是**nvarchar （5)**，預設值是 FALSE。 **false**指定，將不壓縮快照集;**true**指定壓縮快照集。 超出 2GB 的快照集檔案無法壓縮。 壓縮的快照集檔案是在執行合併代理程式的位置進行解壓縮；提取訂閱通常會搭配使用壓縮的快照集，因此，會在訂閱者端將檔案解壓縮。 預設資料夾中的快照集無法壓縮。 若要支援[!INCLUDE[ssEW](../../includes/ssew-md.md)]訂閱者，您必須指定**false**。  
  
 [  **@ftp_address =** ] **'***ftp_address***'**  
 這是散發者之 FTP 服務的網路位址。 *ftp_address*是**sysname**，預設值是 NULL。 指定發行集快照集檔案所在的位置，以便訂閱者的合併代理程式能夠加以收取。 因為這個屬性會儲存每個發行集，每個發行集可以有不同的*ftp_address*。 發行集必須支援利用 FTP 來傳播快照集。  
  
 [  **@ftp_port=** ] *ftp_port*  
 這是散發者的 FTP 服務通訊埠編號。 *ftp_port*是**int**，預設值為 21。 指定發行集快照集檔案所在的位置，以便訂閱者的合併代理程式能夠加以收取。 因為這個屬性會儲存每個發行集，每個發行集可以有它自己*ftp_port*。  
  
 [  **@ftp_subdirectory =** ] **'***ftp_subdirectory***'**  
 指定如果發行集支援利用 FTP 來傳播快照集，訂閱者的合併代理程式可收取快照集檔案的位置。 *ftp_subdirectory*是**nvarchar （255)**，預設值是 NULL。 因為這個屬性會儲存每個發行集，每個發行集可以有它自己*ftp_subdirctory*或是選擇將以 NULL 值的任何子目錄。  
  
 當利用參數化篩選來預先產生快照集時，每個訂閱者分割區的資料快照集都必須在它自己的資料夾中。 利用 FTP 預先產生快照集，其目錄結構必須遵照下列結構：  
  
 *alternate_snapshot_folder*\ftp\\*publisher_publicationDB_publication*\\*partitionID*。  
  
> [!NOTE]  
>  上述斜體值會隨著發行集和訂閱者分割區的細節而不同。  
  
 [  **@ftp_login =** ] **'***ftp_login***'**  
 這是用於連接到 FTP 服務的使用者名稱。 *ftp_login*是**sysname**，預設值為 'anonymous'。  
  
 [  **@ftp_password =** ] **'***ftp_password***'**  
 這是用來連接到 FTP 服務的使用者密碼。 *ftp_password*是**sysname**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。  
  
 [  **@conflict_retention =** ] *conflict_retention*  
 指定衝突的保留期限 (以天為單位)。 *conflict_retention*是**int**，預設值是 14 天之後衝突資料列會從衝突資料表清除。  
  
 [  **@keep_partition_changes =** ] **'***keep_partition_changes***'**  
 指定在無法使用預先計算的分割區時，是否啟用分割區變更最佳化。 *keep_partition_changes*是**nvarchar （5)**，預設值是 TRUE。 **false**表示資料分割變更沒有最佳化，而且資料分割中的資料變更時，不使用預先計算資料分割時，會驗證傳送給所有訂閱者的分割區。 **true**表示資料分割變更最佳化，而且只有中訂閱者資料列已變更的資料分割會受到影響。 預先計算資料分割時，設定*use_partition_groups*至**true**並設定*keep_partition_changes*至**false**。 如需詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
> [!NOTE]  
>  如果您指定的值**true**如*keep_partition_changes*，指定其值為**1**快照集代理程式參數**-MaxNetworkOptimization**. 如需有關此參數的詳細資訊，請參閱[複寫快照集代理程式](../../relational-databases/replication/agents/replication-snapshot-agent.md)。 如需如何指定代理程式參數資訊，請參閱[複寫代理程式管理](../../relational-databases/replication/agents/replication-agent-administration.md)。  
  
 與[!INCLUDE[ssEW](../../includes/ssew-md.md)]訂閱者， *keep_partition_changes*必須設定為 true，以確保正確傳播刪除。 設為 false 時，訂閱者所擁有的資料列可能比預期多。  
  
 [  **@allow_subscription_copy=** ] **'***allow_subscription_copy***'**  
 啟用或停用複製訂閱這個發行集之訂閱資料庫的能力。 *allow_subscription_copy*是**nvarchar （5)**，預設值是 FALSE。 所複製的訂閱資料庫大小必須小於 2 GB。  
  
 [  **@allow_synctoalternate =** ] **'***allow_synctoalternate***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@validate_subscriber_info =** ] **'***validate_subscriber_info***'**  
 列出使用參數化資料列篩選器時，用來定義已發行資料之訂閱者分割區的函數。 *validate_subscriber_info*是**nvarchar （500)**，預設值是 NULL。 合併代理程式利用這項資訊來驗證訂閱者的分割區。 例如，如果[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)會使用參數化資料列篩選器，則參數應該是`@validate_subscriber_info=N'SUSER_SNAME()'`。  
  
> [!NOTE]  
>  您不應該指定這個參數，而應允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自動判斷篩選準則。  
  
 [  **@add_to_active_directory =** ] **'***add_to_active_directory***'**  
 這個參數已被取代，支援它的目的，只是為了與舊版的指令碼相容。 您不能再將發行集資訊加入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中。  
  
 [  **@max_concurrent_merge =** ] *maximum_concurrent_merge*  
 並行合併處理序的最大數目。 *maximum_concurrent_merge*是**int**預設值是 0。 值為**0**的這個屬性表示是在任何給定時間執行的並行合併處理序數目沒有限制。 這個屬性會設定能夠針對合併式發行集來同時執行的並行合併處理序的數目限制。 如果排程同時執行的合併處理序數目超出允許執行的值，超出的作業便會放在佇列中，等到目前在執行中的合併處理序完成為止。  
  
 [  **@max_concurrent_dynamic_snapshots =**] *max_concurrent_dynamic_snapshots*  
 可同時執行以便產生訂閱者分割區之篩選資料快照集的最大快照集代理程式工作階段數目。 *maximum_concurrent_dynamic_snapshots*是**int**預設值是 0。 如果**0**，數字的快照集工作階段沒有限制。 如果排程同時執行的快照集處理序數目超出允許執行的值，超出的作業便會放在佇列中，等到目前在執行中的快照集處理序完成為止。  
  
 [  **@use_partition_groups =** ] **'***use_partition_groups***'**  
 指定應該利用預先計算的分割區來最佳化同步處理。 *use_partition_groups*是**nvarchar （5)**，而且可以是下列值之一：  
  
|值|Description|  
|-----------|-----------------|  
|**true**|發行集使用預先計算的資料分割。|  
|**false**|發行集不使用預先計算的資料分割。|  
|NULL(default)|系統決定資料分割策略。|  
  
 依預設，會使用預先計算的分割區。 若要避免使用預先計算的資料分割， *use_partition_groups*必須設為**false**。 當設為 NULL 時，系統會決定能不能使用預先計算的分割區。 如果預先計算的資料分割，將無法使用，則這個值會實際改成**false**不會產生任何錯誤。 在這種情況下， *keep_partition_changes*可設為**true**來提供部分最佳化。 如需詳細資訊，請參閱[Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)和[Optimize Parameterized Filter Performance with Precomputed](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
 [  **@publication_compatibility_level =** ] *backward_comp_level*  
 指出發行集的回溯相容性。 *backward_comp_level*是**nvarchar(6)**，而且可以是下列值之一：  
  
|值|Version|  
|-----------|-------------|  
|**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
  
 [  **@replicate_ddl =** ] *replicate_ddl*  
 指出是否支援發行集的結構描述複寫。 *replicate_ddl*是**int**，預設值是 1。 **1**表示複寫在發行者端執行的資料定義語言 (DDL) 陳述式，和**0**表示不複寫 DDL 陳述式。 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
 *@replicate_ddl*  DDL 陳述式將資料行時，會接受一個參數。 *@replicate_ddl*  DDL 陳述式改變或卸除資料行，基於下列原因時，參數會被忽略。  
  
-   卸除資料行後，必須更新 sysarticlecolumns，以避免新的 DML 陳述式包括已卸除資料行而造成散發代理程式失敗。 *@replicate_ddl* 參數會被忽略，因為複寫作業一定要複寫結構描述變更。  
  
-   當更改資料行時，來源資料類型或 Null 屬性可能已變更，造成 DML 陳述式包含的值可能與散發者端的資料表不相容。 這類 DML 陳述式可能會造成散發代理程式失敗。 *@replicate_ddl* 參數會被忽略，因為複寫作業一定要複寫結構描述變更。  
  
-   Sysarticlecolumns DDL 陳述式加入新的資料行，不包括新的資料行。 DML 陳述式不會嘗試複寫新資料行的資料。 接受此參數是因為可接受複寫或不複寫 DDL。  
  
 [  **@allow_subscriber_initiated_snapshot =** ] **'***allow_subscriber_initiated_snapshot***'**  
 指出這個發行集的訂閱者是否能起始快照集處理序來產生資料分割區的篩選快照集。 *allow_subscriber_initiated_snapshot*是**nvarchar （5)**，預設值是 FALSE。 **true**指出訂閱者可以起始快照集處理序。  
  
 [  **@allow_web_synchronization =** ] **'***allow_web_synchronization***'**  
 指定是否啟用發行集的 Web 同步處理。 *allow_web_synchronization*是**nvarchar （5)**，預設值是 FALSE。 **true**指定這個發行集的訂閱可以透過 HTTPS 同步處理。 如需詳細資訊，請參閱＜ [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)＞。 若要支援[!INCLUDE[ssEW](../../includes/ssew-md.md)]訂閱者，您必須指定**true**。  
  
 [  **@web_synchronization_url=** ] **'***web_synchronization_url***'**  
 指定 Web 同步處理所用的網際網路 URL 預設值。 *web_synchronization_url 我*s **nvarchar （500)**，預設值是 NULL。 如果其中一個時不會明確地設定定義預設網際網路 URL [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)執行。  
  
 [  **@allow_partition_realignment =** ] **'***allow_partition_realignment***'**  
 決定當修改發行者的資料列造成分割區的變更時，是否要將刪除動作傳給訂閱者。 *allow_partition_realignment*是**nvarchar （5)**，預設值是 TRUE。 **true**將刪除動作傳送至 「 訂閱者 」，以反映資料分割變更的結果來移除不再是一部分的訂閱者資料分割的資料。 **false**會資料從舊的資料分割保留在 「 訂閱者 」，其中這項資料在 「 發行者 」 上所做的變更將不會複寫到這個訂閱者，但在 「 訂閱者 」 上所做的變更會複寫到 「 發行者 」 上。 設定*allow_partition_realignment*至**false**用來保留從舊的分割區的訂用帳戶中的資料，當資料必須能夠存取做為歷程記錄。  
  
> [!NOTE]  
>  在 「 訂閱者 」，因而導致保留的資料， *allow_partition_realignment*至**false**應該處理方式，如同它是唯讀; 不過，這不會強制執行複寫系統。  
  
 [  **@retention_period_unit =** ] **'***retention_period_unit***'**  
 指定期間所設定之保留的單位*保留*。 *retention_period_unit*是**nvarchar （10)**，而且可以是下列值之一。  
  
|值|Version|  
|-----------|-------------|  
|**天**（預設值）|以天為保留週期的指定單位。|  
|**週**|以星期為保留週期的指定單位。|  
|**月份**|以月為保留週期的指定單位。|  
|**年份**|以年為保留週期的指定單位。|  
  
 [  **@generation_leveling_threshold=** ] *generation_leveling_threshold*  
 指定某個層代中包含的變更數目。 層代是指傳遞給發行者或訂閱者的變更集合。 *generation_leveling_threshold*是**int**，預設值是 1000年。  
  
 [  **@automatic_reinitialization_policy =** ] *automatic_reinitialization_policy*  
 指定是否從訂閱者的值，所需的變更發行集，在自動重新初始化之前上傳變更**1**指定 **@force_reinit_subscription** 。 *automatic_reinitialization_policy* bit，預設值為 0。 **1**表示自動重新初始化之前，會從訂閱者上載變更。  
  
> [!IMPORTANT]  
>  如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
 [  **@conflict_logging =** ] **'***conflict_logging***'**  
 指定衝突記錄的儲存位置。 *conflict_logging*是**nvarchar （15)**，而且可以是下列值之一：  
  
|值|Description|  
|-----------|-----------------|  
|**發行者**|衝突記錄會儲存在發行者端。|  
|**訂閱者**|衝突記錄會儲存在造成衝突的訂閱者端。 不支援 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者。|  
|**兩者**|衝突記錄會儲存在發行者端和訂閱者端。|  
|NULL (預設值)|複寫會自動將*conflict_logging*至**兩者**時值*backward_comp_level*是**90RTM**以及**發行者**在所有其他情況下。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addmergepublication**用於合併式複寫中。  
  
 清單的發行集物件到 Active Directory 使用 **@add_to_active_directory** 參數，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必須已在 Active Directory 中建立物件。  
  
 如果存在多個發行集的發行相同的資料庫物件，使用的發行集*replicate_ddl*值**1** ALTER TABLE、 ALTER VIEW、 ALTER PROCEDURE、 ALTER FUNCTION，將複寫和ALTER TRIGGER DDL 陳述式。 不過，所有發行已卸除之資料行的發行集都會複寫 ALTER TABLE DROP COLUMN DDL 陳述式。  
  
 如[!INCLUDE[ssEW](../../includes/ssew-md.md)]「 訂閱者 」 的值*alternate_snapshot_folder*時，才使用的值*snapshot_in_default_folder*是**false**。  
  
 啟用 DDL 複寫 (*replicate_ddl***= 1**) 是發行集，為了進行非複寫 DDL 變更發行集， [sp_changemergepublication &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)設定必須先執行*replicate_ddl*至**0**。 在發出非複寫 DDL 陳述式之後， **sp_changemergepublication**可以再次執行才能重新開啟 DDL 複寫。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddMergePub](../../relational-databases/replication/codesnippet/tsql/sp-addmergepublication-t_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addmergepublication**。  
  
## <a name="see-also"></a>請參閱＜  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
