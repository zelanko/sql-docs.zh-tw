---
title: sp_addmergearticle （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: a9163e6d34a0de6200eafd413d163bb6d92fd4a5
ms.sourcegitcommit: 79e6d49ae4632f282483b0be935fdee038f69cc2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2019
ms.locfileid: "72174009"
---
# <a name="sp_addmergearticle-transact-sql"></a>sp_addmergearticle (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'` 是包含發行項的發行集名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @article = ] 'article'` 是發行項的名稱。 這個名稱在發行集內必須是唯一的。 *文章*是**sysname**，沒有預設值。 發行項必須位於執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的本機電腦上，*而且必須符合*識別碼的規則。  
  
`[ @source_object = ] 'source_object'` 是要發行的資料庫物件。 *source_object*是**sysname**，沒有預設值。 如需可以使用合併式複寫來發行之物件類型的詳細資訊，請參閱[發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
`[ @type = ] 'type'` 是發行項的類型。 *類型*是**sysname**，預設值是**table**，它可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**table** （預設值）|含結構描述和資料的資料表。 複寫會監視資料表來判斷要複寫的資料。|  
|**僅限 func 架構**|只含結構描述的函數。|  
|**僅限** **索引視圖**架構|只含結構描述的索引檢視。|  
|**僅限 proc 架構**|僅限結構描述的預存程序。|  
|**僅限同義字架構**|僅限結構描述的同義字。|  
|**僅限 view 架構**|只含結構描述的檢視。|  
  
`[ @description = ] 'description'` 是文章的描述。 *description*是**Nvarchar （255）** ，預設值是 Null。  
  
`[ @column_tracking = ] 'column_tracking'` 是資料行層級追蹤的設定。 *column_tracking*是**Nvarchar （10）** ，預設值是 FALSE。 **true**會開啟資料行追蹤。 **false**會關閉資料行追蹤，並將衝突偵測保留在資料列層級。 如果資料表已發行在其他合併式發行集中，您必須使用依據這份資料表之現有發行項所使用的相同資料行追蹤值。 這個參數只適用於資料表發行項。  
  
> [!NOTE]  
>  如果使用資料列追蹤執行衝突偵測 (預設值)，基底資料表最多可以包含 1,024 個資料行，但必須從發行項篩選資料行，以便發行最多 246 個資料行。 如果使用資料行追蹤，則基底資料表可包括的資料行數上限為 246。  
  
`[ @status = ] 'status'` 是發行項的狀態。 *狀態*是**Nvarchar （10）** ，預設值是未**同步**處理。 如果**使用**中，則會執行發行資料表的初始處理腳本。 如果未**同步**處理，下次執行快照集代理程式時，就會執行發行資料表的初始處理腳本。  
  
`[ @pre_creation_cmd = ] 'pre_creation_cmd'` 指定當套用快照集時，如果資料表存在於訂閱者上，系統要執行的動作。 *pre_creation_cmd*是**Nvarchar （10）** ，而且可以是下列其中一個值。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**無**|如果訂閱者端已有資料表，就不會採取任何動作。|  
|**delete**|根據子集篩選中的 WHERE 子句來發出一項刪除。|  
|**drop** （預設值）|在重新建立資料表之前，先卸除資料表。 支援 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者所需。|  
|**truncate**|截斷目的地資料表。|  
  
`[ @creation_script = ] 'creation_script'` 是選擇性發行項架構腳本的路徑和名稱，用來在訂閱資料庫中建立發行項。 *creation_script*是**Nvarchar （255）** ，預設值是 Null。  
  
> [!NOTE]  
>  建立指令碼並非執行於 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者。  
  
`[ @schema_option = ] schema_option` 是給定發行項之架構產生選項的點陣圖。 *schema_option*是**binary （8）** ，而且可以是[|（位 OR）](../../t-sql/language-elements/bitwise-or-transact-sql.md)一或多個這些值的乘積。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**0x00**|停用快照集代理程式的腳本，並使用*creation_script*中定義的提供的架構 precreation 腳本。|  
|**0x01**|產生物件的建立作業 (CREATE TABLE、CREATE PROCEDURE 等)。 這是預存程序發行項的預設值。|  
|**0x10**|產生對應的叢集索引。 即使未設定這個選項，如果已發行的資料表上已經有定義與主索引鍵和 UNIQUE 條件約束有關的索引，仍會產生這些索引。|  
|**0x20**|在訂閱者端將使用者定義資料類型 (UDT) 轉換成基底資料型別。 如果 UDT 資料行是主索引鍵的一部分或計算資料行參考 UDT 資料行，則當 UDT 資料行中有 CHECK 或 DEFAULT 條件約束時，就不能使用這個選項。|  
|**0x40**|產生對應的非叢集索引。 即使未設定這個選項，如果已發行的資料表上已經有定義與主索引鍵和 UNIQUE 條件約束有關的索引，仍會產生這些索引。|  
|**0x80**|複寫 PRIMARY KEY 條件約束。 即使未啟用選項**0x10**和**0x40** ，也會複寫與條件約束相關的任何索引。|  
|**0x100**|複寫資料表發行項的使用者觸發程序 (如果定義的話)。|  
|**0x200**|複寫 FOREIGN KEY 條件約束。 如果參考的資料表不是發行集的一部分，便不會複寫發行資料表上任何的 FOREIGN KEY 條件約束。|  
|**0x400**|複寫 CHECK 條件約束。|  
|**0x800**|複寫預設值。|  
|**0x1000**|複寫資料行層級定序。|  
|**0x2000**|複寫與已發行之發行項來源物件相關聯的擴充屬性。|  
|**0x4000**|複寫 UNIQUE 條件約束。 即使未啟用選項**0x10**和**0x40** ，也會複寫與條件約束相關的任何索引。|  
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
|**0x2000000**|不會複寫系結至**xml**資料行的 xml 架構集合。|  
|**0x4000000**|複寫**xml**資料行的索引。|  
|**0x8000000**|建立訂閱者上目前還沒有的任何結構描述。|  
|**0x10000000**|將**xml**資料行轉換為訂閱者上的**Ntext** 。|  
|**0x20000000**|將 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中引進的大型物件資料類型（**Nvarchar （max）** 、 **Varchar （max）** 和**Varbinary （max）** ）轉換成 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]支援的資料類型。|  
|**0x40000000**|複寫權限。|  
|**0x80000000**|試圖卸除對於不在發行集中之任何物件的相依性。|  
|**0x100000000**|如果 FILESTREAM 屬性是在**Varbinary （max）** 資料行上指定，請使用此選項來進行複寫。 如果您要將資料表複寫至 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 訂閱者，請勿指定這個選項。 不論如何設定此架構選項，都不支援將含有 FILESTREAM 資料行的資料表複寫至 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 的訂閱者。 請參閱相關的選項**0x800000000**。|  
|**0x200000000**|將 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 引進的日期和時間資料類型（**date**、 **time**、 **datetimeoffset**和**datetime2**），轉換為舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援的資料類型。|  
|**0x400000000**|複寫資料與索引的壓縮選項。 如需詳細資訊，請參閱 [Data Compression](../../relational-databases/data-compression/data-compression.md)。|  
|**0x800000000**|設定這個選項即可將 FILESTREAM 資料儲存在訂閱者端的檔案群組中。 如果沒有設定這個選項，FILESTREAM 資料就會儲存在預設檔案群組中。 複寫不會建立檔案群組。因此，如果您設定這個選項，就必須先建立檔案群組，然後再於訂閱者端套用快照集。 如需如何在套用快照集之前建立物件的詳細資訊，請參閱[在套用快照集之前和之後執行腳本](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)。<br /><br /> 請參閱相關的選項**0x100000000**。|  
|**0x1000000000**|將 common language runtime （CLR）使用者定義型別（Udt）轉換成**Varbinary （max）** ，使 UDT 類型的資料行可以複寫到執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的訂閱者。|  
|**0x2000000000**|將**hierarchyid**資料類型轉換成**Varbinary （max）** ，使**hierarchyid**類型的資料行可以複寫到執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的訂閱者。 如需如何在複寫資料表中使用**hierarchyid**資料行的詳細資訊，請參閱[hierarchyid &#40;transact-sql&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)。|  
|**0x4000000000**|複寫資料表上任何已篩選的索引。 如需篩選索引的詳細資訊，請參閱[建立篩選的索引](../../relational-databases/indexes/create-filtered-indexes.md)。|  
|**0x8000000000**|將**geography**和**geometry**資料類型轉換成**Varbinary （max）** ，如此一來，這些型別的資料行就可以複寫到執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的訂閱者。|  
|**0x10000000000**|複寫**geography**和**geometry**類型之資料行上的索引。|  
  
 如果這個值是 NULL，系統會自動產生發行項的有效結構描述選項。 [備註] 區段中的**預設架構選項**表會顯示根據發行項類型而選擇的值。 此外，並非所有的*schema_option*值都適用于每種類型的複寫和發行項類型。 [備註] 中提供的**有效架構選項**表會顯示指定之發行項類型的選項。  
  
> [!NOTE]  
>  *Schema_option*參數只會影響初始快照集的複寫選項。 一旦快照集代理程式產生初始架構並套用到「訂閱者」之後，就會根據架構變更複寫規則和[sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)中指定的*replicate_ddl*參數設定，將發行集架構變更複寫到「訂閱者」。 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
`[ @subset_filterclause = ] 'subset_filterclause'` 是 WHERE 子句，指定資料表發行項的水準篩選，而不含包含在其中的文字。 *subset_filterclause*是**Nvarchar （1000）** ，預設值是空字串。  
  
> [!IMPORTANT]  
>  基於效能的考量，建議您不要在參數化資料列篩選器子句中的資料行名稱套用函數，例如 `LEFT([MyColumn]) = SUSER_SNAME()`。 如果您在篩選子句中使用[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)並覆寫 HOST_NAME 值，您可能必須使用[convert](../../t-sql/functions/cast-and-convert-transact-sql.md)來轉換資料類型。 如需有關此案例之最佳做法的詳細資訊，請參閱[參數化資料列篩選器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)中的「覆寫 HOST_NAME （）值」一節。  
  
`[ @article_resolver = ] 'article_resolver'` 是以 COM 為基礎的解析程式，用於解決資料表發行項的衝突，或為了在資料表發行項上執行自訂商務邏輯而叫用的 .NET Framework 元件。 *article_resolver*是**Varchar （255）** ，預設值是 Null。 這個參數可用的值列在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 自訂解析程式中。 如果提供的值不是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 解析程式之一，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會利用指定的解析程式來取代系統提供的解析程式。 使用**sp_enumcustomresolvers**來列舉可用自訂解析程式的清單。 如需詳細資訊，請參閱[在合併同步處理期間執行商務邏輯](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)和[先進合併式複寫衝突偵測與解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
`[ @resolver_info = ] 'resolver_info'` 可用來指定自訂解析程式所需的其他資訊。 部分 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 解析程式需要用於當做解析程式輸入的資料行。 *resolver_info*是**Nvarchar （255）** ，預設值是 Null。 如需詳細資訊，請參閱 [Microsoft COM-Based Resolvers](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)。  
  
`[ @source_owner = ] 'source_owner'` 是*source_object*擁有者的名稱。 *source_owner*是**sysname**，預設值是 Null。 如果是 NULL，就假設目前使用者是擁有者。  
  
`[ @destination_owner = ] 'destination_owner'` 是訂閱資料庫中之物件的擁有者（如果不是 ' dbo '）。 *destination_owner*是**sysname**，預設值是 Null。 如果是 NULL，就假設 'dbo' 是擁有者。  
  
`[ @vertical_partition = ] 'column_filter'` 會啟用和停用資料表發行項的資料行篩選。 *vertical_partition*是**Nvarchar （5）** ，預設值是 FALSE。  
  
 **false**表示沒有垂直篩選，而且會發行所有資料行。  
  
 **true**會清除已宣告的主鍵和 ROWGUID 資料行以外的所有資料行。 資料行是使用**sp_mergearticlecolumn**來加入。  
  
`[ @auto_identity_range = ] 'automatic_identity_range'` 在發行集建立時，啟用和停用此資料表發行項的自動識別範圍處理。 *auto_identity_range*是**Nvarchar （5）** ，預設值是 FALSE。 **true**會啟用自動識別範圍處理，而**false**則會停用它。  
  
> [!NOTE]  
>  *auto_identity_range*已被取代，而且是為了回溯相容性而提供。 您應該使用*identityrangemanagementoption*來指定識別範圍管理選項。 如需詳細資訊，請參閱[複寫識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
當使用自動識別範圍管理時，`[ @pub_identity_range = ] pub_identity_range` 會控制使用伺服器訂閱配置給訂閱者的識別範圍大小。 這個識別範圍保留供重新發行訂閱者配置給自己的訂閱者。 *pub_identity_range*是**Bigint**，預設值是 Null。 如果*identityrangemanagementoption*是**auto**或*auto_identity_range*為**true**，您就必須指定這個參數。  
  
`[ @identity_range = ] identity_range` 控制使用自動識別範圍管理時，配置給發行者和訂閱者的識別範圍大小。 *identity_range*是**Bigint**，預設值是 Null。 如果*identityrangemanagementoption*是**auto**或*auto_identity_range*為**true**，您就必須指定這個參數。  
  
> [!NOTE]  
>  *identity_range*使用舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，控制重新發行訂閱者端的識別範圍大小。  
  
`[ @threshold = ] threshold` 百分比值，可控制合併代理程式指派新識別範圍的時機。 使用 [*臨界*值] 中指定的百分比時，合併代理程式會建立新的識別範圍。 *閾值*是**int**，預設值是 Null。 如果*identityrangemanagementoption*是**auto**或*auto_identity_range*為**true**，您就必須指定這個參數。  
  
`[ @verify_resolver_signature = ] verify_resolver_signature` 指定在合併式複寫中使用解析程式之前，是否要驗證數位簽章。 *verify_resolver_signature*是**int**，預設值是1。  
  
 **0**指定不會驗證簽章。  
  
 **1**指定將會驗證簽章，以查看它是否來自信任的來源。  
  
`[ @destination_object = ] 'destination_object'` 是訂閱資料庫中的物件名稱。 *destination_object*是**sysname**，預設值為 **\@source_object**中的內容。 只有在這個發行項是僅限結構描述的發行項 (如預存程序、檢視和 UDF) 時，才能指定這個參數。 如果指定的發行項是資料表發行項， *@source_object* 中的值會覆寫*destination_object*中的值。  
  
`[ @allow_interactive_resolver = ] 'allow_interactive_resolver'` 啟用或停用發行項的互動式解析程式。 *allow_interactive_resolver*是**Nvarchar （5）** ，預設值是 FALSE。 **true**可讓您在發行項上使用互動式解析程式;**false**會停用它。  
  
> [!NOTE]  
>  [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者不支援互動解析程式。  
  
`[ @fast_multicol_updateproc = ] 'fast_multicol_updateproc'` 此參數已被取代，而且會針對腳本的回溯相容性進行維護。  
  
`[ @check_permissions = ] check_permissions` 是在合併代理程式將變更套用至發行者時，所驗證之資料表層級許可權的點陣圖。 如果合併處理序所使用的發行者登入/使用者帳戶並沒有正確的資料表權限，就會將無效的變更記錄為衝突。 *check_permissions*是**int**，而且可以是[|（位 OR）](../../t-sql/language-elements/bitwise-or-transact-sql.md)下列一個或多個值的乘積。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**0x00** （預設值）|不檢查權限。|  
|**0x10**|先在發行者端檢查權限，之後才能上傳在訂閱者端進行的插入作業。|  
|**0x20**|先在發行者端檢查權限，之後才能上傳在訂閱者端進行的更新作業。|  
|**0x40**|先在發行者端檢查權限，之後才能上傳在訂閱者端進行的刪除作業。|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 確認此預存程式所採取的動作可能會使現有的快照集失效。 *force_invalidate_snapshot*是**bit**，預設值是0。  
  
 **0**指定加入發行項並不會使快照集無效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1**指定加入發行項可能會導致快照集無效，如果有現有的訂閱需要新的快照集，則會提供要標示為已淘汰之現有快照集的許可權，並產生新的快照集。 將發行項加入含有現有快照集的發行集中時， *force_invalidate_snapshot*設為**1** 。  
  
`[ @published_in_tran_pub = ] 'published_in_tran_pub'` 表示合併式發行集中的發行項也在交易式發行集中發行。 *published_in_tran_pub*是**Nvarchar （5）** ，預設值是 FALSE。 **true**指定發行項也在交易式發行集中發行。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` 確認此預存程式所採取的動作可能需要重新初始化現有的訂閱。 *force_reinit_subscription*是**bit**，預設值是0。  
  
 **0**指定加入發行項並不會重新初始化訂閱。 如果預存程序偵測到變更需要重新初始化現有的訂閱，就會發生錯誤，且不會進行任何變更。  
  
 **1**表示合併發行項的變更會使現有的訂閱重新初始化，並提供要進行訂閱重新初始化的許可權。 當*subset_filterclause*指定參數化資料列篩選器時， *force_reinit_subscription*會設定為**1** 。  
  
`[ @logical_record_level_conflict_detection = ] 'logical_record_level_conflict_detection'` 指定屬於邏輯記錄成員的發行項之衝突偵測層級。 *logical_record_level_conflict_detection*是**Nvarchar （5）** ，預設值是 FALSE。  
  
 **true**指定在邏輯記錄中的任何位置進行變更時，將會偵測到衝突。  
  
 **false**指定使用預設衝突偵測，如*column_tracking*所指定。 如需詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
> [!NOTE]  
>  因為 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 的訂閱者不支援邏輯記錄，所以您必須針對*logical_record_level_conflict_detection*指定**false**值，以支援這些訂閱者。  
  
`[ @logical_record_level_conflict_resolution = ] 'logical_record_level_conflict_resolution'` 指定屬於邏輯記錄成員的發行項之衝突解決層級。 *logical_record_level_conflict_resolution*是**Nvarchar （5）** ，預設值是 FALSE。  
  
 **true**指定整個獲勝的邏輯記錄會覆寫遺失的邏輯記錄。  
  
 **false**指定獲勝資料列不限於邏輯記錄。 如果*logical_record_level_conflict_detection*為**true**，則*logical_record_level_conflict_resolution*也必須設定為**true**。 如需詳細資訊，請參閱[使用邏輯記錄分組相關資料列的變更](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
> [!NOTE]  
>  因為 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 的訂閱者不支援邏輯記錄，所以您必須針對*logical_record_level_conflict_resolution*指定**false**值，以支援這些訂閱者。  
  
`[ @partition_options = ] partition_options` 定義發行項中資料分割的方式，當所有資料列只屬於一個資料分割或一個訂用帳戶時，可讓效能優化。 *partition_options*是**Tinyint**，它可以是下列其中一個值。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**0** (預設)|發行項的篩選是靜態的，或不產生每個資料分割的唯一資料子集；也就是說，它是一個「重疊」的資料分割。|  
|**1**|資料分割重疊，在訂閱者端進行的資料操作語言 (DML) 更新並不會變更資料列所屬的資料分割。|  
|**2**|發行項的篩選會產生非重疊的資料分割，但多個訂閱者可以接收相同的資料分割。|  
|**3**|發行項的篩選會產生對每項訂閱而言都是唯一的非重疊資料分割。|  
  
> [!NOTE]  
>  如果發行項的來源資料表已經在另一個發行集中發行，則這兩篇文章的*partition_options*值都必須相同。  
  
`[ @processing_order = ] processing_order` 表示合併式發行集中之發行項的處理順序。 *processing_order*是**int**，預設值是0。 **0**指定發行項為未排序，而任何其他值表示此發行項之處理順序的序數值。 發行項會依照從最低值到最高值的順序來處理。 如果兩個發行項具有相同的值，則處理順序是由[sysmergearticles](../../relational-databases/system-tables/sysmergearticles-transact-sql.md)系統資料表中的發行項昵稱順序所決定。 如需詳細資訊，請參閱[指定合併式複寫屬性](../../relational-databases/replication/merge/specify-merge-replication-properties.md)。  
  
`[ @subscriber_upload_options = ] subscriber_upload_options` 定義在訂閱者端使用用戶端訂閱所做之更新的限制。 如需詳細資訊，請參閱[使用僅限下載的發行項最佳化合併式複寫效能](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。 *subscriber_upload_options*是**Tinyint**，它可以是下列其中一個值。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**0** (預設)|無限制。 在訂閱者端進行的變更會上傳到發行者|  
|**1**|允許在訂閱者端進行變更，但變更不會上傳到發行者。|  
|**2**|不允許在訂閱者端進行變更。|  
  
 變更*subscriber_upload_options*需要藉由呼叫[sp_reinitmergepullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md)來重新初始化訂閱。  
  
> [!NOTE]  
>  如果發行項的來源資料表已經在另一個發行集中發行，則這兩篇文章的*subscriber_upload_options*值必須相同。  
  
`[ @identityrangemanagementoption = ] identityrangemanagementoption` 指定如何處理髮行項的識別範圍管理。 *identityrangemanagementoption*是**Nvarchar （10）** ，它可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**無**|停用識別範圍的管理。|  
|**手動**|利用 NOT FOR REPLICATION 來標示識別欄位，以啟用手動的識別範圍處理。|  
|**自動**|指定自動管理識別範圍。|  
|Null （預設值）|當*auto_identity_range*的值不是**true**時，預設值為**none**。|  
  
 為了與舊版相容，當*identityrangemanagementoption*的值為 Null 時，會檢查*auto_identity_range*的值。 不過，當*identityrangemanagementoption*的值不是 Null 時，就會忽略*auto_identity_range*的值。 如需詳細資訊，請參閱[複寫識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
`[ @delete_tracking = ] 'delete_tracking'` 指出刪除是否已複寫。 *delete_tracking*是**Nvarchar （5）** ，預設值是 TRUE。 **false**表示不復寫刪除，而**true**表示複寫已複寫，這是合併式複寫的一般行為。 當*delete_tracking*設定為**false**時，必須在發行者端手動移除在訂閱者端刪除的資料列，而且必須在訂閱者端手動移除在發行者端刪除的資料列。  
  
> [!IMPORTANT]  
>  將*delete_tracking*設定為**false**會導致無法聚合。 如果發行項的來源資料表已經在另一個發行集中發行，則這兩篇文章的*delete_tracking*值都必須相同。  
  
> [!NOTE]  
>  無法使用 [**新增發行集]** 或 [**發行集屬性**] 對話方塊來設定*delete_tracking*選項。  
  
`[ @compensate_for_errors = ] 'compensate_for_errors'` 指出在同步處理期間發生錯誤時，是否採取補償動作。 *compensate_for_errors i*s **Nvarchar （5）** ，預設值為 FALSE。 當設定為**true**時，在同步處理期間無法套用至訂閱者或發行者的變更，一律會導致補償動作復原變更;不過，如果其中一個錯誤設定的「訂閱者」產生錯誤，可能會導致其他「訂閱者」和「發行者」的變更復原。 **false**會停用這些補償動作，不過，錯誤仍會記錄為具有補償，而後續的合併會繼續嘗試套用變更，直到成功為止。  
  
> [!IMPORTANT]  
>  雖然受影響的資料列之資料可能會有未聚合的表現，但任何錯誤只要獲得處理，就能夠套用變更，聚合資料。 如果發行項的來源資料表已經在另一個發行集中發行，則這兩篇文章的*compensate_for_errors*值都必須相同。  
  
`[ @stream_blob_columns = ] 'stream_blob_columns'` 指定在複寫二進位大型物件資料行時，使用資料流程優化。 *stream_blob_columns*是**Nvarchar （5）** ，預設值是 FALSE。 **true**表示將會嘗試優化。 啟用 FILESTREAM 時， *stream_blob_columns*設定為 true。 這可讓 FILESTREAM 資料的複寫能以最理想的方式執行，並減少記憶體使用量。 若要強制 FILESTREAM 資料表發行項不使用 blob 資料流程，請使用**sp_changemergearticle**將*stream_blob_columns*設定為 false。  
  
> [!IMPORTANT]  
>  啟用這個記憶體最佳化功能可能會減損合併代理程式在同步化時的效能。 只有在複寫包含數 MB 資料的資料行時，才應該使用這個選項。  
  
> [!NOTE]  
>  某些合併式複寫功能（例如邏輯記錄）仍可防止在複寫二進位大型物件時使用資料流程優化，即使*stream_blob_columns*設定為**true**也一樣。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>Remarks  
 **sp_addmergearticle**用於合併式複寫中。  
  
 當您發行物件時，它們的定義會複製到訂閱者。 如果您發行相依於一或多個其他物件的資料庫物件，您就必須發行所有參考的物件。 例如，如果您發行相依於資料表的檢視表，同時也必須發行該資料表。  
  
 如果您為*partition_options*指定**3**的值，則該發行項中的每個資料分割都只能有單一訂用帳戶。 如果建立第二項訂閱，將新訂閱的篩選準則解析成現有訂閱的相同資料分割，就會卸除現有的訂閱。  
  
 為*partition_options*指定3的值時，每當合併代理程式執行時，就會清除中繼資料，而分割快照集會更快過期。 當使用這個選項時，您應該考慮啟用訂閱者要求的資料分割快照集。 如需詳細資訊，請參閱＜ [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)＞。  
  
 將具有靜態水準篩選的發行項（使用*subset_filterclause*）加入具有具有參數化篩選之文章的現有發行集，需要重新初始化訂閱。  
  
 指定*processing_order*時，建議您在發行項順序值之間保留間距，讓未來更容易設定新的值。 例如，如果您有三個文章 Article1、Article2 和 Article3 這，請將*processing_order*設定為10、20和30，而不是1、2和3。 如需詳細資訊，請參閱[指定合併式複寫屬性](../../relational-databases/replication/merge/specify-merge-replication-properties.md)。  
  
## <a name="default-schema-option-table"></a>預設結構描述選項表  
 下表描述預存程式所設定的預設值（如果為*schema_option*指定 Null 值，這取決於發行項類型）。  
  
|發行項類型|結構描述選項值|  
|------------------|-------------------------|  
|**僅限 func 架構**|**0x01**|  
|**僅限索引視圖架構**|**0x01**|  
|**僅限 proc 架構**|**0x01**|  
|**table**|使用原生模式快照集， **0x0C034FD1** - [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本相容的發行集。<br /><br /> 使用字元模式快照集， **0x08034FF1** - [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本相容的發行集。|  
|**僅限 view 架構**|**0x01**|  
  
> [!NOTE]  
>  如果發行集支援舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則**資料表**的預設架構選項為**0x30034FF1**。  
  
## <a name="valid-schema-option-table"></a>有效的結構描述選項表  
 下表描述根據發行項類型*schema_option*的允許值。  
  
|發行項類型|結構描述選項值|  
|------------------|--------------------------|  
|**僅限 func 架構**|**0x01**和**0x2000**|  
|**僅限索引視圖架構**|**0x01**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x1000000**和**0x200000**|  
|**僅限 proc 架構**|**0x01**和**0x2000**|  
|**table**|所有選項。|  
|**僅限 view 架構**|**0x01**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x1000000**和**0x200000**|  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-addmergearticle-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員** 固定伺服器角色或 **db_owner** 固定資料庫角色中的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [定義發行項](../../relational-databases/replication/publish/define-an-article.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 複寫[識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
