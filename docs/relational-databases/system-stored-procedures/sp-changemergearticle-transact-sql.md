---
title: sp_changemergearticle （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/09/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergearticle_TSQL
- sp_changemergearticle
helpviewer_keywords:
- sp_changemergearticle
ms.assetid: 0dc3da5c-4af6-45be-b5f0-074da182def2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6c59b4ba84981ff4cb1240d78e1d6d472be61289
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829635"
---
# <a name="sp_changemergearticle-transact-sql"></a>sp_changemergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更合併發行項的屬性。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changemergearticle [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是發行項所在的發行集名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @article = ] 'article'`這是要變更的發行項名稱。 *文章*是**sysname**，沒有預設值。  
  
`[ @property = ] 'property'`這是給定發行項和發行集要變更的屬性。 *property*是**Nvarchar （30）**，它可以是下表所列的其中一個值。  
  
`[ @value = ] 'value'`這是指定之屬性的新值。 *value*是**Nvarchar （1000）**，它可以是資料表中所列的其中一個值。  
  
 下表描述發行項的屬性及這些屬性的值。  
  
|屬性|值|描述|  
|--------------|------------|-----------------|  
|**allow_interactive_resolver**|**true**|啟用發行項的互動式解析程式。|  
||**false**|停用發行項的互動式解析程式。|  
|**article_resolver**||自訂的發行項解析程式。 只適用於資料表發行項。|  
|**check_permissions** （點陣圖）|**0x00**|不檢查資料表層級權限。|  
||**0x10**|在發行者端套用訂閱者所建立的 INSERT 陳述式之前，先在發行者端檢查資料表層級權限。|  
||**0x20**|在發行者端套用訂閱者所建立的 UPDATE 陳述式之前，先檢查發行者端的資料表層級權限。|  
||**0x40**|在發行者端套用訂閱者所建立的 DELETE 陳述式之前，先檢查發行者端的資料表層級權限。|  
|**column_tracking**|**true**|開啟資料行層級追蹤。 只適用於資料表發行項。<br /><br /> 注意：發行具有超過246個數據行的資料表時，不能使用資料行層級追蹤。|  
||**false**|關閉資料行層級追蹤，將衝突偵測保留在資料列層級。 只適用於資料表發行項。|  
|**compensate_for_errors**|**true**|在同步處理期間，當發生錯誤時，執行補償動作。 如需詳細資訊，請參閱[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。|  
||**false**|不執行補償動作，這是預設行為。 如需詳細資訊，請參閱[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。<br /><br /> 重要：雖然受影響資料列中的資料可能會在您解決任何錯誤時出現不一致的情況，但是可以套用變更並將資料聚合。 ** \* \* \* \* ** 如果發行項的來源資料表已經在另一個發行集中發行，則這兩篇文章的*compensate_for_errors*值都必須相同。|  
|**creation_script**||在訂閱資料庫中，用來建立發行項的選擇性發行項結構描述指令碼的路徑和名稱。|  
|**delete_tracking**|**true**|複寫 DELETE 陳述式，這是預設行為。|  
||**false**|不複寫 DELETE 陳述式。<br /><br /> ** \* \* 重要 \* 設定 \* ** **delete_tracking**為**false**會導致無法聚合，而且已刪除的資料列必須以手動方式移除。|  
|**描述**||發行項的描述項目。|  
|**destination_owner**||訂閱資料庫中物件的擁有者名稱（如果不是**dbo**）。|  
|**identity_range**||當發行項的**identityrangemanagementoption**設為**auto** ，或**auto_identity_range**設定為**true**時，指定指派新識別值時所要使用之範圍大小的**Bigint** 。 只適用於資料表發行項。 如需詳細資訊，請參閱複寫[識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)的「合併式複寫」一節。|  
|**identityrangemanagementoption**|**手動**|停用自動識別範圍的管理。 利用 NOT FOR REPLICATION 來標示識別欄位，以啟用手動識別範圍的處理。 如需詳細資訊，請參閱[複寫識別資料欄](../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
||**無**|停用所有識別範圍的管理。|  
|**logical_record_level_conflict_detection**|**true**|如果在邏輯記錄的任何位置進行變更，便會偵測到衝突。 要求**logical_record_level_conflict_resolution**必須設定為**true**。|  
||**false**|預設的衝突偵測會依照**column_tracking**所指定的方式來使用。|  
|**logical_record_level_conflict_resolution**|**true**|用整個優先邏輯記錄來覆寫遺失的邏輯記錄。|  
||**false**|優先資料列不限於邏輯記錄。|  
|**partition_options**|**0**|發行項的篩選是靜態的，或不產生每個資料分割的唯一資料子集，也就是「重疊」的資料分割。|  
||**1**|資料分割重疊，在訂閱者端進行的 DML 更新並不會變更資料列所屬的資料分割。|  
||**2**|發行項的篩選會產生非重疊的資料分割，但多個訂閱者可以接收相同的資料分割。|  
||**3**|發行項的篩選會產生對每項訂閱而言都是唯一的非重疊資料分割。<br /><br /> 注意：如果您針對**partition_options**指定**3**的值，則該發行項中的每個資料分割都只能有單一訂用帳戶。 如果建立第二項訂閱，將新訂閱的篩選準則解析成現有訂閱的相同資料分割，就會卸除現有的訂閱。|  
|**pre_creation_command**|**無**|如果訂閱者端已有資料表，就不會採取任何動作。|  
||**delete**|根據子集篩選中的 WHERE 子句來發出一項刪除。|  
||**下拉式**|在重新建立資料表之前，先卸除資料表。|  
||**各**|截斷目的地資料表。|  
|**processing_order**||**int** ，指出合併式發行集中之發行項的處理順序。|  
|**pub_identity_range**||當發行項的**identityrangemanagementoption**設為**auto**或**auto_identity_range**設定為**True****時，指定**配置給訂閱者的範圍大小（如果發行項具有伺服器訂閱）。 這個識別範圍保留供重新發行訂閱者配置給自己的訂閱者。 只適用於資料表發行項。 如需詳細資訊，請參閱複寫[識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)的「合併式複寫」一節。|  
|**published_in_tran_pub**|**true**|發行項也在交易式發行集中發行。|  
||**false**|發行項也不在交易式發行集中發行。|  
|**resolver_info**||這用來指定自訂解析程式所需要的其他資訊。 部分 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 解析程式需要用於當做解析程式輸入的資料行。 **resolver_info**是**Nvarchar （255）**，預設值是 Null。 如需詳細資訊，請參閱 [以 COM 為基礎的 Microsoft 解析程式](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)。|  
|**schema_option** （點陣圖）||如需詳細資訊，請參閱本主題稍後的＜備註＞一節。|  
||**0x00**|停用快照集代理程式的腳本，並使用**creation_script**中提供的腳本。|  
||**0x01**|產生物件建立指令碼 (CREATE TABLE、CREATE PROCEDURE 等)。|  
||**0x10**|產生對應的叢集索引。|  
||**0x20**|在訂閱者端將使用者自訂資料類型轉換成基底資料型別。 如果使用者自訂類型 (UDT) 資料行是主索引鍵的一部分，或者計算資料行參考 UDT 資料行，則當 UDT 資料行中有 CHECK 或 DEFAULT 條件約束時，就不能使用這個選項。|  
||**0x40**|產生對應的非叢集索引。|  
||**0x80**|包括主索引鍵的宣告式參考完整性。|  
||**0x100**|複寫資料表發行項的使用者觸發程序 (如果定義的話)。|  
||**0x200**|複寫 FOREIGN KEY 條件約束。 如果參考的資料表不是發行集的一部分，便不會複寫發行資料表上任何的 FOREIGN KEY 條件約束。|  
||**0x400**|複寫 CHECK 條件約束。|  
||**0x800**|複寫預設值。|  
||**0x1000**|複寫資料行層級定序。|  
||**0x2000**|複寫與已發行之發行項來源物件相關聯的擴充屬性。|  
||**0x4000**|如果資料表發行項上定義了唯一索引鍵，便複寫唯一索引鍵。|  
||**0x8000**|當編寫條件約束指令碼時，產生 ALTER TABLE 陳述式。|  
||**0x10000**|將 CHECK 條件約束複寫成 NOT FOR REPLICATION，以免在同步處理期間強制執行條件約束。|  
||**0x20000**|將 FOREIGN KEY 條件約束複寫成 NOT FOR REPLICATION，以免在同步處理期間強制執行條件約束。|  
||**0x40000**|複寫資料分割資料表或索引的相關聯檔案群組。|  
||**0x80000**|複寫資料分割資料表的資料分割配置。|  
||**0x100000**|複寫資料分割索引的資料分割配置。|  
||**0x200000**|複寫資料表統計資料。|  
||**0x400000**|複寫預設繫結|  
||**0x800000**|複寫規則繫結|  
||**0x1000000**|複寫全文檢索索引|  
||**0x2000000**|不會複寫系結至**xml**資料行的 xml 架構集合。|  
||**0x4000000**|複寫**xml**資料行的索引。|  
||**0x8000000**|建立訂閱者目前還沒有的任何結構描述。|  
||**0x10000000**|將**xml**資料行轉換為訂閱者上的**Ntext** 。|  
||**0x20000000**|將中引進的大型物件資料類型（**Nvarchar （max）**、 **Varchar （** max）和**Varbinary （max）**）轉換 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 成所支援的資料類型 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 。|  
||**0x40000000**|複寫權限。|  
||**0x80000000**|嘗試卸除對於不在發行集中之任何物件的相依性。|  
||**0x100000000**|如果 FILESTREAM 屬性是在**Varbinary （max）** 資料行上指定，請使用此選項來進行複寫。 如果您要將資料表複寫至 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 訂閱者，請勿指定這個選項。 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]不論如何設定此架構選項，都不支援將含有 FILESTREAM 資料行的資料表複寫至訂閱者。 請參閱相關的選項**0x800000000**。|  
||**0x200000000**|將中導入的日期和時間資料類型（**date**、 **time**、 **datetimeoffset**和**datetime2**）轉換 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 成舊版所支援的資料類型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
||**0x400000000**|複寫資料與索引的壓縮選項。 如需詳細資訊，請參閱 [Data Compression](../../relational-databases/data-compression/data-compression.md)。|  
||**0x800000000**|設定這個選項即可將 FILESTREAM 資料儲存在訂閱者端的檔案群組中。 如果沒有設定這個選項，FILESTREAM 資料就會儲存在預設檔案群組中。 複寫不會建立檔案群組。因此，如果您設定這個選項，就必須先建立檔案群組，然後再於訂閱者端套用快照集。 如需如何在套用快照集之前建立物件的詳細資訊，請參閱[在套用快照集之前和之後執行腳本](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)。<br /><br /> 請參閱相關的選項**0x100000000**。|  
||**0x1000000000**|將 common language runtime （CLR）使用者定義型別（Udt）轉換成**Varbinary （max）** ，以便將 UDT 類型的資料行複寫至正在執行的訂閱者 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。|  
||**0x2000000000**|將**hierarchyid**資料類型轉換成**Varbinary （max）** ，使**hierarchyid**類型的資料行可以複寫至正在執行的訂閱者 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。 如需如何在複寫資料表中使用**hierarchyid**資料行的詳細資訊，請參閱[hierarchyid &#40;transact-sql&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)。|  
||**0x4000000000**|複寫資料表上任何已篩選的索引。 如需篩選索引的詳細資訊，請參閱[建立篩選的索引](../../relational-databases/indexes/create-filtered-indexes.md)。|  
||**0x8000000000**|將**geography**和**geometry**資料類型轉換成**Varbinary （max）** ，以便將這些型別的資料行複寫至正在執行的訂閱者 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。|  
||**0x10000000000**|複寫**geography**和**geometry**類型之資料行上的索引。|  
||NULL|系統會自動產生發行項的有效結構描述選項。|  
|**status**|**active**|發行資料表的初始處理指令碼在執行中。|  
||**unsynced**|在下次執行快照集代理程式時，執行發行資料表的初始處理指令碼。|  
|**stream_blob_columns**|**true**|當複寫二進位大型物件資料行時，使用資料流最佳化。 不過，特定合併式複寫功能，如邏輯記錄，仍能夠防止使用資料流最佳化。 啟用 FILESTREAM 時， *stream_blob_columns*設定為 true。 這可讓 FILESTREAM 資料的複寫能以最理想的方式執行，並減少記憶體使用量。 若要強制 FILESTREAM 資料表發行項不使用 blob 資料流程，請將*stream_blob_columns*設定為 false。<br /><br /> ** \* \* 重要 \* ： \* **啟用此記憶體優化可能會在同步處理期間損害合併代理程式的效能。 只有在複寫包含數 MB 資料的資料行時，才應該使用這個選項。|  
||**false**|當複寫二進位大型物件資料行時，不使用最佳化。|  
|**subscriber_upload_options**|**0**|客訂閱在訂閱者端進行的更新沒有任何限制；變更會上傳到發行者。 變更這個屬性可能需要重新初始化現有的訂閱者。|  
||**1**|允許客訂閱在訂閱者端進行變更；但它們不會上傳到發行者。|  
||**2**|不允許客訂閱在訂閱者端進行變更。|  
|**subset_filterclause**||指定水平篩選的 WHERE 子句。 只適用於資料表發行項。<br /><br /> ** \* \* 重要 \* 事項 \* ** ：基於效能考慮，建議您不要在參數化資料列篩選器子句（例如）中，將函數套用至資料行名稱 `LEFT([MyColumn]) = SUSER_SNAME()` 。 如果您在篩選子句中使用[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)並覆寫 HOST_NAME 值，您可能必須使用[convert](../../t-sql/functions/cast-and-convert-transact-sql.md)來轉換資料類型。 如需有關此案例之最佳做法的詳細資訊，請參閱[參數化資料列篩選器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)中的「覆寫 HOST_NAME （）值」一節。|  
|**閾值**||執行或舊版的訂閱者所使用的百分比值 [!INCLUDE[ssEW](../../includes/ssew-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 當合併代理程式指派新的識別範圍時，**臨界值**控制。 當使用 threshold 指定的百分比值，合併代理程式會建立新的識別範圍。 當**identityrangemanagementoption**設定為**auto**或**auto_identity_range**設定為**true**時使用。 只適用於資料表發行項。 如需詳細資訊，請參閱複寫[識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)的「合併式複寫」一節。|  
|**verify_resolver_signature**|**1**|驗證自訂解析程式的數位簽章來判斷它是否來自信任來源。|  
||**0**|不驗證自訂解析程式的數位簽章來判斷它是否來自信任來源。|  
|NULL (預設值)||傳回*屬性*的支援值清單。|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`認可這個預存程式所採取的動作可能會使現有的快照集失效。 *force_invalidate_snapshot*是**bit**，預設值是**0**。  
  
 **0**指定合併發行項的變更不會使快照集無效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1**表示合併發行項的變更可能會導致快照集無效，如果有現有的訂閱需要新的快照集，則會提供要標示為已淘汰之現有快照集的許可權，並產生新的快照集。  
  
 請參閱＜備註＞一節，以了解在變更時需要產生新快照集的屬性。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`認可這個預存程式所採取的動作可能需要重新初始化現有的訂閱。 *force_reinit_subscription*是**bit**，預設值是**0**。  
  
 **0**指定合併發行項的變更不會使訂閱重新初始化。 如果預存程序偵測到變更需要重新初始化現有的訂閱，就會發生錯誤，且不會進行任何變更。  
  
 **1**表示合併發行項的變更會使現有的訂閱重新初始化，並提供將發生之訂閱重新初始化的許可權。  
  
 請參閱＜備註＞一節，以了解在變更時需要重新初始化所有現有的訂閱之屬性。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changemergearticle**用於合併式複寫中。  
  
 因為**sp_changemergearticle**是用來變更一開始使用[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)所指定的發行項屬性，請參閱[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)以取得這些屬性的其他相關資訊。  
  
 變更下列屬性需要產生新的快照集，而且您必須為*force_invalidate_snapshot*參數指定**1**的值：  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **schema_options**  
  
-   **subset_filterclause**  
  
 變更下列屬性需要重新初始化現有的訂閱，而且您必須為*force_reinit_subscription*參數指定**1**的值：  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **identityrangemanagementoption**  
  
-   **subscriber_upload_options**  
  
-   **subset_filterclause**  
  
-   **creation_script**  
  
-   **schema_option**  
  
-   **logical_record_level_conflict_detection**  
  
-   **logical_record_level_conflict_resolution**  
  
 為**partition_options**指定3的值時，每當合併代理程式執行時，就會清除中繼資料，而分割快照集會更快過期。 當使用這個選項時，您應該考慮啟用訂閱者要求的資料分割快照集。 如需詳細資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
 當設定**column_tracking**屬性時，如果資料表已經在其他合併式發行集中發行，則資料行追蹤必須和現有發行項根據此資料表所使用的值相同。 這個參數只適用於資料表發行項。  
  
 如果有多個發行集根據相同的基礎資料表來發佈發行項，變更**delete_tracking**屬性或一篇文章的**compensate_for_errors**屬性，會使其他以相同資料表為基礎的文章進行相同的變更。  
  
 如果合併處理序所使用的發行者登入/使用者帳戶並沒有正確的資料表權限，就會將無效的變更記錄為衝突。  
  
 變更**schema_option**的值時，系統不會執行位更新。 這表示當您使用**sp_changemergearticle**設定**schema_option**時，可能會關閉現有的位設定。 若要保留現有的設定，您應該在所設定的值和目前的*schema_option*值之間執行[& （位 and）](../../t-sql/language-elements/bitwise-and-transact-sql.md) ，這可以藉由執行[sp_helpmergearticle](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)來判斷。  
  
> [!CAUTION]  
>  當您的發行集中有許多（或許上百個）的文章，而且您對其中一個文章執行**sp_changemergearticle**時，可能需要很長的時間才能完成執行。  
  
## <a name="valid-schema-option-table"></a>有效的結構描述選項表  
 下表描述允許的*schema_option*值，視發行項類型而定。  
  
|發行項類型|結構描述選項值|  
|------------------|--------------------------|  
|**func schema only**|**0x01**和**0x2000**|  
|**indexed view schema only**|**0x01**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x1000000**和**0x200000**|  
|**proc schema only**|**0x01**和**0x2000**|  
|**table**|所有選項。|  
|**view schema only**|**0x01**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x1000000**和**0x200000**|  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_changemergearticle](../../relational-databases/replication/codesnippet/tsql/sp-changemergearticle-tr_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_changemergearticle**。  
  
## <a name="see-also"></a>另請參閱  
 [查看和修改發行項屬性](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
