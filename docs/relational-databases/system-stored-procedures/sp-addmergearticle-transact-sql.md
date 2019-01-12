---
title: sp_addmergearticle & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergearticle
- sp_addmergearticle_TSQL
helpviewer_keywords:
- sp_addmergearticle
ms.assetid: 0df654ea-24e2-4c61-a75a-ecaa7a140a6c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4bcf5b0163156fe078c3bd3382efb193ec417399
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129406"
---
# <a name="spaddmergearticle-transact-sql"></a>sp_addmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將發行項加入現有的合併式發行集中。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addmergearticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @source_object = ] 'source_object'   
    [ , [ @type = ] 'type' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @column_tracking = ] 'column_tracking' ]   
    [ , [ @status = ] 'status' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @subset_filterclause = ] 'subset_filterclause' ]   
    [ , [ @article_resolver = ] 'article_resolver' ]   
    [ , [ @resolver_info = ] 'resolver_info' ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @verify_resolver_signature = ] verify_resolver_signature ]   
    [ , [ @destination_object = ] 'destination_object' ]   
    [ , [ @allow_interactive_resolver = ] 'allow_interactive_resolver' ]   
    [ , [ @fast_multicol_updateproc = ] 'fast_multicol_updateproc' ]   
    [ , [ @check_permissions = ] check_permissions ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @published_in_tran_pub = ] 'published_in_tran_pub' ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @logical_record_level_conflict_detection = ] 'logical_record_level_conflict_detection' ]  
    [ , [ @logical_record_level_conflict_resolution = ] 'logical_record_level_conflict_resolution' ]  
    [ , [ @partition_options = ] partition_options ]  
    [ , [ @processing_order = ] processing_order ]  
    [ , [ @subscriber_upload_options = ] subscriber_upload_options ]  
    [ , [ @identityrangemanagementoption = ] 'identityrangemanagementoption' ]  
    [ , [ @delete_tracking = ] delete_tracking ]  
    [ , [ @compensate_for_errors = ] 'compensate_for_errors' ]   
    [ , [ @stream_blob_columns = ] 'stream_blob_columns' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication=** ] **'**_發行集_**'**  
 這是發行項所在的發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@article=** ] **'**_文章_**'**  
 這是發行項的名稱。 這個名稱在發行集內必須是唯一的。 *發行項*已**sysname**，沒有預設值。 *發行項*必須是執行的本機電腦上[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而且必須符合識別碼的規則。  
  
 [  **@source_object=** ] **'**_source_object_**'**  
 這是要發佈的資料庫物件。 *source_object*已**sysname**，沒有預設值。 如需可以使用合併式複寫發行之物件的類型的詳細資訊，請參閱[發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
 [  **@type=** ] **'**_型別_**'**  
 這是發行項的類型。 *型別*已**sysname**，預設值是**表格**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**資料表**（預設值）|含結構描述和資料的資料表。 複寫會監視資料表來判斷要複寫的資料。|  
|**僅限 func 結構描述**|只含結構描述的函數。|  
|**索引檢視表****僅限結構描述**|只含結構描述的索引檢視。|  
|**僅限程序結構描述**|僅限結構描述的預存程序。|  
|**僅限同義字結構描述**|僅限結構描述的同義字。|  
|**僅限檢視結構描述**|只含結構描述的檢視。|  
  
 [  **@description=** ] **'**_描述_**'**  
 這是發行項的描述。 *描述*已**nvarchar(255)**，預設值是 NULL。  
  
 [  **@column_tracking=** ] **'**_column_tracking_**'**  
 這是資料行層級追蹤的設定。 *column_tracking*已**nvarchar(10**，預設值是 FALSE。 **true**開啟的資料行追蹤。 **false**會關閉資料行追蹤，並將衝突偵測保留在資料列層級。 如果資料表已發行在其他合併式發行集中，您必須使用依據這份資料表之現有發行項所使用的相同資料行追蹤值。 這個參數只適用於資料表發行項。  
  
> [!NOTE]  
>  如果使用資料列追蹤執行衝突偵測 (預設值)，基底資料表最多可以包含 1,024 個資料行，但必須從發行項篩選資料行，以便發行最多 246 個資料行。 如果使用資料行追蹤，則基底資料表可包括的資料行數上限為 246。  
  
 [  **@status=** ] **'**_狀態_**'**  
 這是發行項的狀態。 *狀態*已**nvarchar(10**，預設值是**unsynced**。 如果**active**，執行發行資料表的初始處理指令碼。 如果**unsynced**，發行資料表的初始處理指令碼會在下次執行快照集代理程式執行。  
  
 [  **@pre_creation_cmd=** ] **'**_pre_creation_cmd_**'**  
 指定在套用快照集時，如果資料表存在於訂閱者，系統要採取什麼動作。 *pre_creation_cmd*已**nvarchar(10**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**None**|如果訂閱者端已有資料表，就不會採取任何動作。|  
|**delete**|根據子集篩選中的 WHERE 子句來發出一項刪除。|  
|**卸除**（預設值）|在重新建立資料表之前，先卸除資料表。 支援所需[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssEW](../../includes/ssew-md.md)]訂閱者。|  
|**truncate**|截斷目的地資料表。|  
  
 [  **@creation_script=** ] **'**_creation_script_**'**  
 在訂閱資料庫中，這是用來建立發行項的選擇性發行項結構描述指令碼的路徑和名稱。 *creation_script*已**nvarchar(255)**，預設值是 NULL。  
  
> [!NOTE]  
>  建立指令碼並非執行於 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者。  
  
 [  **@schema_option=** ] *schema_option*  
 這是給定發行項的結構描述產生選項點陣圖。 *schema_option*已**binary(8**，而且可以是[|(位元 OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md)產品的一或多個這些值。  
  
|值|描述|  
|-----------|-----------------|  
|**0x00**|停用快照集代理程式指令碼，並使用提供的結構描述之預先建立指令碼中定義*creation_script*。|  
|**0x01**|產生物件的建立作業 (CREATE TABLE、CREATE PROCEDURE 等)。 這是預存程序發行項的預設值。|  
|**0x10**|產生對應的叢集索引。 即使未設定這個選項，如果已發行的資料表上已經有定義與主索引鍵和 UNIQUE 條件約束有關的索引，仍會產生這些索引。|  
|**0x20**|在訂閱者端將使用者定義資料類型 (UDT) 轉換成基底資料型別。 如果 UDT 資料行是主索引鍵的一部分或計算資料行參考 UDT 資料行，則當 UDT 資料行中有 CHECK 或 DEFAULT 條件約束時，就不能使用這個選項。|  
|**0x40**|產生對應的非叢集索引。 即使未設定這個選項，如果已發行的資料表上已經有定義與主索引鍵和 UNIQUE 條件約束有關的索引，仍會產生這些索引。|  
|**0x80**|複寫 PRIMARY KEY 條件約束。 此外，也會複寫任何與條件約束的索引，即使選項**0x10**並**0x40**未啟用。|  
|**0x100**|複寫資料表發行項的使用者觸發程序 (如果定義的話)。|  
|**0x200**|複寫 FOREIGN KEY 條件約束。 如果參考的資料表不是發行集的一部分，便不會複寫發行資料表上任何的 FOREIGN KEY 條件約束。|  
|**0x400**|複寫 CHECK 條件約束。|  
|**0x800**|複寫預設值。|  
|**0x1000**|複寫資料行層級定序。|  
|**0x2000**|複寫與已發行之發行項來源物件相關聯的擴充屬性。|  
|**0x4000**|複寫 UNIQUE 條件約束。 此外，也會複寫任何與條件約束的索引，即使選項**0x10**並**0x40**未啟用。|  
|**0x8000**|這個選項對於執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本的發行者無效。|  
|**0x10000**|將 CHECK 條件約束複寫成 NOT FOR REPLICATION，以免在同步處理期間強制執行條件約束。|  
|**0x20000**|將 FOREIGN KEY 條件約束複寫成 NOT FOR REPLICATION，以免在同步處理期間強制執行條件約束。|  
|**0x40000**|複寫資料分割資料表或索引的相關聯檔案群組。|  
|**0x80000**|複寫資料分割資料表的資料分割配置。|  
|**0x100000**|複寫資料分割索引的資料分割配置。|  
|**0x200000**|複寫資料表統計資料。|  
|**0x400000**|複寫預設繫結。|  
|**0x800000**|複寫規則繫結。|  
|**0x1000000**|複寫全文檢索索引。|  
|**0x2000000**|XML 結構描述集合繫結至**xml**不會複寫資料行。|  
|**0x4000000**|在複寫索引**xml**資料行。|  
|**0x8000000**|建立訂閱者上目前還沒有的任何結構描述。|  
|**0x10000000**|將轉換**xml**資料行**ntext**訂閱者上。|  
|**0x20000000**|將大型物件資料類型 (**nvarchar （max)**， **varchar （max)**，並**varbinary （max)**) 中導入[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]到支援的資料類型[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
|**0x40000000**|複寫權限。|  
|**0x80000000**|試圖卸除對於不在發行集中之任何物件的相依性。|  
|**0x100000000**|使用此選項來複寫 FILESTREAM 屬性，如果同時指定**varbinary （max)** 資料行。 如果您要將資料表複寫至 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 訂閱者，請勿指定這個選項。 將具有 FILESTREAM 資料行的資料表複寫[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]不支援訂閱者，不論這個結構描述選項的設定方式。 請參閱相關的選項**0x800000000**。|  
|**0x200000000**|將日期和時間資料類型轉換 (**日期**，**時間**， **datetimeoffset**，以及**datetime2**) 中導入[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]資料型別所支援的舊版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**0x400000000**|複寫資料與索引的壓縮選項。 如需詳細資訊，請參閱 [Data Compression](../../relational-databases/data-compression/data-compression.md)。|  
|**0x800000000**|設定這個選項即可將 FILESTREAM 資料儲存在訂閱者端的檔案群組中。 如果沒有設定這個選項，FILESTREAM 資料就會儲存在預設檔案群組中。 複寫不會建立檔案群組。因此，如果您設定這個選項，就必須先建立檔案群組，然後再於訂閱者端套用快照集。 如需如何建立物件，然後再套用快照集的詳細資訊，請參閱[前後執行指令碼之後套用快照集](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)。<br /><br /> 請參閱相關的選項**0x100000000**。|  
|**0x1000000000**|將 common language runtime (CLR) 使用者定義類型 (Udt) 轉換成**varbinary （max)** 如此 UDT 類型的資料行可以複寫至訂閱者執行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。|  
|**0x2000000000**|將轉換**hierarchyid**資料類型**varbinary （max)** 以便類型的資料行**hierarchyid**可以複寫到訂閱者執行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 如需有關如何使用**hierarchyid**資料行在複寫資料表中，請參閱[hierarchyid &#40;-&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)。|  
|**0x4000000000**|複寫資料表上任何已篩選的索引。 如需有關篩選索引的詳細資訊，請參閱[建立篩選的索引](../../relational-databases/indexes/create-filtered-indexes.md)。|  
|**0x8000000000**|將轉換**地理**並**幾何**資料類型**varbinary （max)** 使這些類型的資料行可以複寫到訂閱者執行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000000000**|複寫類型的資料行的索引**地理**並**geometry**。|  
  
 如果這個值是 NULL，系統會自動產生發行項的有效結構描述選項。 **預設結構描述選項**< 備註 > 一節的表格顯示所選根據發行項類型的值。 另外，並非所有*schema_option*值對於每個複寫類型和發行項類型都有效。 **有效的結構描述選項**「 備註 」 中的表格顯示可以針對給定發行項類型指定的選項。  
  
> [!NOTE]  
>  *Schema_option*參數只會影響初始快照集的複寫選項。 根據結構描述變更複寫規則發行集結構描述變更複寫到訂閱者端發生之後已經產生快照集代理程式且訂閱者端套用初始的結構描述，而*replicate_ddl*中指定的參數設定[sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
 [  **@subset_filterclause=** ] **'**_subset_filterclause_**'**  
 這是一個 WHERE 子句，指定資料表發行項的水平篩選，但不含 WHERE 一字。 *subset_filterclause*屬於**nvarchar(1000)**，預設值是空字串。  
  
> [!IMPORTANT]  
>  基於效能的考量，建議您不要在參數化資料列篩選器子句中的資料行名稱套用函數，例如 `LEFT([MyColumn]) = SUSER_SNAME()`。 如果您使用[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)在篩選子句和覆寫了 HOST_NAME 值中，您可能必須使用轉換資料類型[轉換](../../t-sql/functions/cast-and-convert-transact-sql.md)。 如需有關此案例的最佳作法的詳細資訊，請參閱 「 覆寫 host_name （） 值 」 中[Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。  
  
 [  **@article_resolver=** ] **'**_article_resolver_**'**  
 這是以 COM 為基礎的解析程式，用於解決資料表發行項的衝突，或為了在資料表發行項上執行自訂商務邏輯而呼叫之 .NET Framework 組件的衝突。 *article_resolver*已**varchar(255)**，預設值是 NULL。 這個參數可用的值列在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 自訂解析程式中。 如果提供的值不是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 解析程式之一，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會利用指定的解析程式來取代系統提供的解析程式。 使用**sp_enumcustomresolvers**來列舉可用自訂解析程式的清單。 如需詳細資訊，請參閱 <<c0> [ 執行期間合併同步處理商務邏輯](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)並[Advanced Merge Replication Conflict Detection 和解析度](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
 [  **@resolver_info=** ] **'**_resolver_info_**'**  
 這用來指定自訂解析程式所需要的其他資訊。 部分 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 解析程式需要用於當做解析程式輸入的資料行。 *resolver_info*已**nvarchar(255)**，預設值是 NULL。 如需詳細資訊，請參閱 [以 COM 為基礎的 Microsoft 解析程式](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)。  
  
 [  **@source_owner=** ] **'**_source_owner_**'**  
 是擁有者的名稱*source_object*。 *source_owner*已**sysname**，預設值是 NULL。 如果是 NULL，就假設目前使用者是擁有者。  
  
 [  **@destination_owner=** ] **'**_destination_owner_**'**  
 如果訂閱資料庫中之物件的擁有者不是 dbo 的話，這便是訂閱資料庫中之物件的擁有者。 *destination_owner*已**sysname**，預設值是 NULL。 如果是 NULL，就假設 'dbo' 是擁有者。  
  
 [  **@vertical_partition=** ] **'**_column_filter_**'**  
 在資料表發行項上，啟用和停用資料行的篩選。 *vertical_partition*已**nvarchar(5)** 預設值是 FALSE。  
  
 **false**表示沒有垂直篩選，並將發佈的所有資料行。  
  
 **true**清除所有其他宣告的主索引鍵資料行和 ROWGUID 資料行。 藉由加入資料行**sp_mergearticlecolumn**。  
  
 [  **@auto_identity_range=** ] **'**_automatic_identity_range_**'**  
 在發行集建立之時，啟用和停用此資料表發行項的自動識別範圍處理。 *auto_identity_range*已**nvarchar(5)**，預設值是 FALSE。 **真**啟用自動識別範圍處理，而**false**會停用它。  
  
> [!NOTE]  
>  *auto_identity_range*已被取代，而且為了回溯相容性才提供。 您應該使用*identityrangemanagementoption*指定識別範圍管理選項。 如需詳細資訊，請參閱[複寫識別資料欄](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
 [  **@pub_identity_range=** ] *pub_identity_range*  
 控制使用自動識別範圍管理時，利用伺服器訂閱配置給訂閱者的識別範圍大小。 這個識別範圍保留供重新發行訂閱者配置給自己的訂閱者。 *pub_identity_range*已**bigint**，預設值是 NULL。 您必須指定這個參數，如果*identityrangemanagementoption*是**自動**或者*auto_identity_range*是**true**。  
  
 [  **@identity_range=** ] *identity_range*  
 控制使用自動識別範圍管理時，配置給發行者和訂閱者的識別範圍大小。 *identity_range*已**bigint**，預設值是 NULL。 您必須指定這個參數，如果*identityrangemanagementoption*是**自動**或者*auto_identity_range*是**true**。  
  
> [!NOTE]  
>  *identity_range*控制重新發行訂閱者使用舊版的識別範圍大小[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 [  **@threshold=** ]*臨界值*  
 這是一個百分比值，用於控制合併代理程式指派新識別範圍的時機。 當指定的百分比值*閾值*是使用，「 合併代理程式會建立新的識別範圍。 *閾值*已**int**，預設值是 NULL。 您必須指定這個參數，如果*identityrangemanagementoption*是**自動**或者*auto_identity_range*是**true**。  
  
 [  **@verify_resolver_signature=** ] *verify_resolver_signature*  
 指定在合併式複寫中使用解析程式之前，是否要驗證數位簽章： *verify_resolver_signature*已**int**，預設值是 1。  
  
 **0**指定不驗證簽章。  
  
 **1**指定將會驗證簽章，來查看它是否來自信任的來源。  
  
 [  **@destination_object=** ] **'**_destination_object_**'**  
 這是訂閱資料庫中之物件的名稱。 *destination_object*已**sysname**，預設值是功能**@source_object**。 只有在這個發行項是僅限結構描述的發行項 (如預存程序、檢視和 UDF) 時，才能指定這個參數。 指定發行項是否在資料表發行項中的值*@source_object*中的值會覆寫*destination_object*。  
  
 [  **@allow_interactive_resolver=** ] **'**_allow_interactive_resolver_**'**  
 啟用或停用發行項的互動解析程式。 *allow_interactive_resolver*已**nvarchar(5)**，預設值是 FALSE。 **true**可讓您使用的發行項; 「 互動解析程式**false**會停用它。  
  
> [!NOTE]  
>  [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者不支援互動解析程式。  
  
 [  **@fast_multicol_updateproc=** ] **'**_fast_multicol_updateproc_**'**  
 這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。  
  
 [  **@check_permissions=** ] *check_permissions*  
 這是合併代理程式將變更套用在發行者時，所驗證之資料表層級權限的點陣圖。 如果合併處理序所使用的發行者登入/使用者帳戶並沒有正確的資料表權限，就會將無效的變更記錄為衝突。 *check_permissions*已**int**，而且可以是[|(位元 OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md)一或多個下列值的乘積。  
  
|值|描述|  
|-----------|-----------------|  
|**0x00** （預設值）|不檢查權限。|  
|**0x10**|先在發行者端檢查權限，之後才能上傳在訂閱者端進行的插入作業。|  
|**0x20**|先在發行者端檢查權限，之後才能上傳在訂閱者端進行的更新作業。|  
|**0x40**|先在發行者端檢查權限，之後才能上傳在訂閱者端進行的刪除作業。|  
  
 [  **@force_invalidate_snapshot=** ] *force_invalidate_snapshot*  
 認可這個預存程序所採取的動作可能使現有的快照集失效。 *force_invalidate_snapshot*已**元**，預設值是 0。  
  
 **0**指定加入發行項並不會導致快照集失效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1**指定加入發行項可能使快照集失效，如果有現有的訂閱需要新的快照集，提供權限來標示為已棄用之現有快照集並產生新的快照集。 *force_invalidate_snapshot*設定為**1**發行項加入含有現有快照集的發行集時。  
  
 [  **@published_in_tran_pub=** ] **'**_published_in_tran_pub_**'**  
 指出合併式發行集中的發行項也在交易式發行集中發行。 *published_in_tran_pub*已**nvarchar(5)**，預設值是 FALSE。 **true**指定也交易式發行集中發行項。  
  
 [  **@force_reinit_subscription=** ] *force_reinit_subscription*  
 認可這個預存程序所採取的動作可能需要重新初始化現有的訂閱。 *force_reinit_subscription*已**元**，預設值是 0。  
  
 **0**指定加入發行項不會不會使訂閱重新初始化。 如果預存程序偵測到變更需要重新初始化現有的訂閱，就會發生錯誤，且不會進行任何變更。  
  
 **1**表示合併發行項的變更會導致現有的訂閱重新初始化，並提供發生之訂閱重新初始化的權限。 *force_reinit_subscription*設定為**1**當*subset_filterclause*指定參數化資料列篩選器。  
  
 [  **@logical_record_level_conflict_detection=** ] **'**_logical_record_level_conflict_detection_**'**  
 指定本身是邏輯記錄成員的發行項之衝突偵測層級。 *logical_record_level_conflict_detection*已**nvarchar(5)**，預設值是 FALSE。  
  
 **true**指定是否邏輯記錄中任何位置進行變更，將會偵測衝突。  
  
 **false**指定使用預設衝突偵測依照*column_tracking*。 如需詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
> [!NOTE]  
>  因為邏輯記錄不會受到[!INCLUDE[ssEW](../../includes/ssew-md.md)]訂閱者，您必須指定的值**false**如*logical_record_level_conflict_detection*以支援這些訂閱者。  
  
 [  **@logical_record_level_conflict_resolution=** ] **'**_logical_record_level_conflict_resolution_**'**  
 指定本身是邏輯記錄成員的發行項之衝突解決層級。 *logical_record_level_conflict_resolution*已**nvarchar(5)**，預設值是 FALSE。  
  
 **true**指定整個優先邏輯記錄會覆寫遺失的邏輯記錄。  
  
 **false**指定優先資料列不限於邏輯記錄。 如果*logical_record_level_conflict_detection*是 **，則為 true**，然後*logical_record_level_conflict_resolution*也必須設定為**true**. 如需詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
> [!NOTE]  
>  因為邏輯記錄不會受到[!INCLUDE[ssEW](../../includes/ssew-md.md)]訂閱者，您必須指定的值**false**如*logical_record_level_conflict_resolution*以支援這些訂閱者。  
  
 [  **@partition_options=** ] *partition_options*  
 定義發行項資料進行資料分割的方式，當所有資料列只屬於單一資料分割或單一訂閱時，能夠使效能最佳化。 *partition_options*已**tinyint**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0** (預設)|發行項的篩選是靜態的，或不產生每個資料分割的唯一資料子集；也就是說，它是一個「重疊」的資料分割。|  
|**1**|資料分割重疊，在訂閱者端進行的資料操作語言 (DML) 更新並不會變更資料列所屬的資料分割。|  
|**2**|發行項的篩選會產生非重疊的資料分割，但多個訂閱者可以接收相同的資料分割。|  
|**3**|發行項的篩選會產生對每項訂閱而言都是唯一的非重疊資料分割。|  
  
> [!NOTE]  
>  如果發行項的來源資料表已在另一個發行集，則會將值的*partition_options*必須是兩個發行項相同。  
  
 [  **@processing_order=** ] *processing_order*  
 指出合併式發行集中發行項的處理順序。 *processing_order*已**int**，預設值是 0。 **0**指出發行項並未排序，任何其他值則表示這個發行項之處理順序的序數值。 發行項會依照從最低值到最高值的順序來處理。 如果兩個發行項有相同的值，處理順序由決定的順序中的發行項暱稱[sysmergearticles](../../relational-databases/system-tables/sysmergearticles-transact-sql.md)系統資料表。 如需詳細資訊，請參閱 <<c0> [ 指定合併式複寫屬性](../../relational-databases/replication/merge/specify-merge-replication-properties.md)。  
  
 [  **@subscriber_upload_options=** ] *subscriber_upload_options*  
 定義客訂閱在訂閱者端進行的更新之限制。 如需詳細資訊，請參閱[使用僅限下載的發行項最佳化合併式複寫效能](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。 *subscriber_upload_options*已**tinyint**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0** (預設)|無限制。 在訂閱者端進行的變更會上傳到發行者|  
|**1**|允許在訂閱者端進行變更，但變更不會上傳到發行者。|  
|**2**|不允許在訂閱者端進行變更。|  
  
 變更*subscriber_upload_options*需要藉由呼叫重新初始化訂閱[sp_reinitmergepullsubscription &#40;-&#41;](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md)。  
  
> [!NOTE]  
>  如果發行項的來源資料表已在另一個發行集的值*subscriber_upload_options*必須是兩個發行項相同。  
  
 [  **@identityrangemanagementoption=** ] *identityrangemanagementoption*  
 指定如何處理發行項的識別範圍管理。 *identityrangemanagementoption*已**nvarchar(10**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**None**|停用識別範圍的管理。|  
|**手動**|利用 NOT FOR REPLICATION 來標示識別欄位，以啟用手動的識別範圍處理。|  
|**自動**|指定自動管理識別範圍。|  
|NULL(default)|預設值為**無**時的值*auto_identity_range*不**true**。|  
  
 回溯相容性，當的值*identityrangemanagementoption*是 NULL，值*auto_identity_range*已核取。 不過，當 windows 7 *identityrangemanagementoption*不是 NULL，則值*auto_identity_range*會被忽略。 如需詳細資訊，請參閱[複寫識別資料欄](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
 [  **@delete_tracking=** ] **'**_delete_tracking_**'**  
 指出是否複寫刪除。 *delete_tracking*已**nvarchar(5)**，預設值是 TRUE。 **false**表示不複寫刪除，並 **，則為 true**表示複寫刪除，這是很平常的行為，合併式複寫。 當*delete_tracking*設為**false**、 訂閱者端刪除的資料列必須手動移除在發行者上，並在 「 訂閱者 」 必須手動移除在發行者端刪除的資料列。  
  
> [!IMPORTANT]  
>  設定*delete_tracking*要**false**導致無法聚合。 如果發行項的來源資料表已在另一個發行集，則會將值的*delete_tracking*必須是兩個發行項相同。  
  
> [!NOTE]  
>  *delete_tracking*選項無法使用設定**新的發行集精靈 」** 或**發行集屬性** 對話方塊。  
  
 [  **@compensate_for_errors=** ] **'**_compensate_for_errors_**'**  
 指出在同步處理期間發現錯誤時，是否採取補償動作。 *compensate_for_errors 我*s **nvarchar(5)**，預設值是 FALSE。 當設定為 **，則為 true**，變更無法套用在訂閱者 」 或一律同步處理期間發行者會導致補償動作恢復變更; 不過，其中一個未正確設定的訂閱者，會產生錯誤可以會造成在恢復其他訂閱者和發行者的變更。 **false**停用這些補償動作，不過，錯誤仍會記錄成含有補償，而且後續的合併會繼續試圖套用變更，直到成功為止。  
  
> [!IMPORTANT]  
>  雖然受影響的資料列之資料可能會有未聚合的表現，但任何錯誤只要獲得處理，就能夠套用變更，聚合資料。 如果發行項的來源資料表已在另一個發行集，則會將值的*compensate_for_errors*必須是兩個發行項相同。  
  
 [  **@stream_blob_columns=** ] **'**_stream_blob_columns_**'**  
 指定在複寫二進位大型物件資料行時，使用資料流最佳化。 *stream_blob_columns*已**nvarchar(5)**，預設值是 FALSE。 **true**表示將嘗試最佳化。 *stream_blob_columns*設為 true 時啟用 FILESTREAM。 這可讓 FILESTREAM 資料的複寫能以最理想的方式執行，並減少記憶體使用量。 若要強制 FILESTREAM 資料表發行項不使用 blob 資料流，請使用**sp_changemergearticle**來設定*stream_blob_columns*設為 false。  
  
> [!IMPORTANT]  
>  啟用這個記憶體最佳化功能可能會減損合併代理程式在同步化時的效能。 只有在複寫包含數 MB 資料的資料行時，才應該使用這個選項。  
  
> [!NOTE]  
>  特定的合併式複寫功能，如邏輯記錄，仍可以防止當複寫二進位大型物件，即使是使用資料流最佳化*stream_blob_columns*設定為**true**.  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addmergearticle**用於合併式複寫中。  
  
 當您發行物件時，它們的定義會複製到訂閱者。 如果您發行相依於一或多個其他物件的資料庫物件，您就必須發行所有參考的物件。 例如，如果您發行相依於資料表的檢視表，同時也必須發行該資料表。  
  
 如果您指定的值**3** for *partition_options*，可以只有單一訂用帳戶每個資料分割的該文章中的資料。 如果建立第二項訂閱，將新訂閱的篩選準則解析成現有訂閱的相同資料分割，就會卸除現有的訂閱。  
  
 指定的值是 3 時*partition_options*，中繼資料都會清除每當執行合併代理程式和資料分割的快照集到期得更快。 當使用這個選項時，您應該考慮啟用訂閱者要求的資料分割快照集。 如需詳細資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
 使用靜態的水平篩選的發行項加入、 使用*subset_filterclause*至現有的發行集使用參數化篩選的發行項需要重新初始化訂閱。  
  
 指定時*processing_order*，我們建議您發行項順序值之間保留間距可以輕鬆設定新的值在未來。 例如，如果您有 Article1、 Article2 和 article3 這三個發行時，設定*processing_order*至 10、 20 和 30，而不是 1、 2 和 3。 如需詳細資訊，請參閱 <<c0> [ 指定合併式複寫屬性](../../relational-databases/replication/merge/specify-merge-replication-properties.md)。  
  
## <a name="default-schema-option-table"></a>預設結構描述選項表  
 下表說明如果指定 NULL 值，會將預存程序所設定的預設值*schema_option*，這取決於發行項類型。  
  
|發行項類型|結構描述選項值|  
|------------------|-------------------------|  
|**僅限 func 結構描述**|**0x01**|  
|**僅限索引檢視表結構描述**|**0x01**|  
|**僅限程序結構描述**|**0x01**|  
|**table**|**0x0C034FD1**  -  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]和更新版本相容發行集使用原生模式快照集。<br /><br /> **0x08034FF1**  -  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]和更新版本相容發行集使用字元模式快照集。|  
|**僅限檢視結構描述**|**0x01**|  
  
> [!NOTE]  
>  如果發行集支援舊版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，預設結構描述選項**表格**是**0x30034FF1**。  
  
## <a name="valid-schema-option-table"></a>有效的結構描述選項表  
 下表描述允許的值*schema_option*根據發行項類型而定。  
  
|發行項類型|結構描述選項值|  
|------------------|--------------------------|  
|**僅限 func 結構描述**|**0x01**和**0x2000**|  
|**僅限索引檢視表結構描述**|**0x01**， **0x040**， **0x0100**， **0x2000**， **0x40000**， **0x1000000**，以及**0x200000**|  
|**僅限程序結構描述**|**0x01**和**0x2000**|  
|**table**|所有選項。|  
|**僅限檢視結構描述**|**0x01**， **0x040**， **0x0100**， **0x2000**， **0x40000**， **0x1000000**，以及**0x200000**|  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-addmergearticle-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員** 固定伺服器角色或 **db_owner** 固定資料庫角色中的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [複寫識別資料行](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
