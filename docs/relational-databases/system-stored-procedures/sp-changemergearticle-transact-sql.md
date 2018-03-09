---
title: "sp_changemergearticle (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 11/09/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changemergearticle_TSQL
- sp_changemergearticle
helpviewer_keywords:
- sp_changemergearticle
ms.assetid: 0dc3da5c-4af6-45be-b5f0-074da182def2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97c2b4b07b79b061b85e50cd51c4716173f073a6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spchangemergearticle-transact-sql"></a>sp_changemergearticle (Transact-SQL)
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
 [  **@publication=**] **'***發行集***'**  
 這是發行項所在發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@article=**] **'***文章***'**  
 這是要變更的發行項名稱。 *發行項*是**sysname**，沒有預設值。  
  
 [  **@property=**] **'***屬性***'**  
 這是給定發行項和發行集要變更的屬性。 *屬性*是**nvarchar （30)**，它可以其中一個值列出資料表中。  
  
 [  **@value=**] **'***值***'**  
 這是指定之屬性的新值。 *值*是**nvarchar （1000)**，它可以其中一個值列出資料表中。  
  
 下表描述發行項的屬性及這些屬性的值。  
  
|屬性|值|Description|  
|--------------|------------|-----------------|  
|**allow_interactive_resolver**|**true**|啟用發行項的互動式解析程式。|  
||**false**|停用發行項的互動式解析程式。|  
|**article_resolver**||自訂的發行項解析程式。 只適用於資料表發行項。|  
|**check_permissions** （點陣圖）|**0x00**|不檢查資料表層級權限。|  
||**0x10**|在發行者端套用訂閱者所建立的 INSERT 陳述式之前，先在發行者端檢查資料表層級權限。|  
||**0x20**|在發行者端套用訂閱者所建立的 UPDATE 陳述式之前，先檢查發行者端的資料表層級權限。|  
||**0x40**|在發行者端套用訂閱者所建立的 DELETE 陳述式之前，先檢查發行者端的資料表層級權限。|  
|**column_tracking**|**true**|開啟資料行層級追蹤。 只適用於資料表發行項。<br /><br /> 注意： 發行的資料表超過 246 個資料行不能使用資料行層級追蹤。|  
||**false**|關閉資料行層級追蹤，將衝突偵測保留在資料列層級。 只適用於資料表發行項。|  
|**compensate_for_errors**|**true**|在同步處理期間，當發生錯誤時，執行補償動作。 如需詳細資訊，請參閱[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。|  
||**false**|不執行補償動作，這是預設行為。 如需詳細資訊，請參閱[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。<br /><br /> **\*\*重要\* \*** 雖然受影響的資料列中的資料可能會顯示為聚合，解決任何錯誤時，可以套用變更，聚合資料。 如果發行項的來源資料表已在另一個發行集，則會將值的*compensate_for_errors*必須是兩個發行項相同。|  
|**creation_script**||在訂閱資料庫中，用來建立發行項的選擇性發行項結構描述指令碼的路徑和名稱。|  
|**delete_tracking**|**true**|複寫 DELETE 陳述式，這是預設行為。|  
||**false**|不複寫 DELETE 陳述式。<br /><br /> **\*\*重要\* \*** 設定**delete_tracking**至**false**導致非聚合狀況，和已刪除的資料列必須以手動方式移除。|  
|**描述**||發行項的描述項目。|  
|**destination_owner**||在訂閱資料庫中，如果不是物件的擁有者名稱**dbo**。|  
|**identity_range**||**bigint** ，指定如果發行項，指派新識別值時要使用的範圍大小**identityrangemanagementoption**設**自動**或**auto_identity_範圍**設**true**。 只適用於資料表發行項。 如需詳細資訊，請參閱 「 合併式複寫 」 一節[複寫識別資料行](../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
|**identityrangemanagementoption**|**手動**|停用自動識別範圍的管理。 利用 NOT FOR REPLICATION 來標示識別欄位，以啟用手動識別範圍的處理。 如需詳細資訊，請參閱[複寫識別資料欄](../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
||**無**|停用所有識別範圍的管理。|  
|**logical_record_level_conflict_detection**|**true**|如果在邏輯記錄的任何位置進行變更，便會偵測到衝突。 要求**logical_record_level_conflict_resolution**設**true**。|  
||**false**|會使用預設衝突偵測，依指定**column_tracking**。|  
|**logical_record_level_conflict_resolution**|**true**|用整個優先邏輯記錄來覆寫遺失的邏輯記錄。|  
||**false**|優先資料列不限於邏輯記錄。|  
|**partition_options**|**0**|發行項的篩選是靜態的，或不產生每個資料分割的唯一資料子集，也就是「重疊」的資料分割。|  
||**1**|資料分割重疊，在訂閱者端進行的 DML 更新並不會變更資料列所屬的資料分割。|  
||**2**|發行項的篩選會產生非重疊的資料分割，但多個訂閱者可以接收相同的資料分割。|  
||**3**|發行項的篩選會產生對每項訂閱而言都是唯一的非重疊資料分割。<br /><br /> 注意： 如果您指定的值**3**如**partition_options**，可以是只能有單一訂閱的每個資料分割的文件中的資料。 如果建立第二項訂閱，將新訂閱的篩選準則解析成現有訂閱的相同資料分割，就會卸除現有的訂閱。|  
|**pre_creation_command**|**無**|如果訂閱者端已有資料表，就不會採取任何動作。|  
||**刪除**|根據子集篩選中的 WHERE 子句來發出一項刪除。|  
||**卸除**|在重新建立資料表之前，先卸除資料表。|  
||**截斷**|截斷目的地資料表。|  
|**processing_order**||**int** ，指出合併式發行集中發行項的處理順序。|  
|**pub_identity_range**||**bigint**指定配置到含主訂閱的訂閱者，如果發行項的範圍大小**identityrangemanagementoption**設**自動**或**自動_identity_range**設**true**。 這個識別範圍保留供重新發行訂閱者配置給自己的訂閱者。 只適用於資料表發行項。 如需詳細資訊，請參閱 「 合併式複寫 」 一節[複寫識別資料行](../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
|**published_in_tran_pub**|**true**|發行項也在交易式發行集中發行。|  
||**false**|發行項也不在交易式發行集中發行。|  
|**resolver_info**||這用來指定自訂解析程式所需要的其他資訊。 部分 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 解析程式需要用於當做解析程式輸入的資料行。 **resolver_info**是**nvarchar （255)**，預設值是 NULL。 如需詳細資訊，請參閱 [以 COM 為基礎的 Microsoft 解析程式](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)。|  
|**schema_option** （點陣圖）||如需詳細資訊，請參閱本主題稍後的＜備註＞一節。|  
||**0x00**|停用快照集代理程式的指令碼，並使用提供的指令碼**creation_script**。|  
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
||**0x2000000**|XML 結構描述集合繫結至**xml**不複寫資料行。|  
||**0x4000000**|在複寫索引**xml**資料行。|  
||**0x8000000**|建立訂閱者目前還沒有的任何結構描述。|  
||**0x10000000**|將轉換**xml**欄**ntext** 「 訂閱者 」。|  
||**0x20000000**|將大型物件資料類型 (**nvarchar （max)**， **varchar （max)**，和**varbinary （max)**) 中所導入[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]支援的資料類型在[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。|  
||**0x40000000**|複寫權限。|  
||**0x80000000**|嘗試卸除對於不在發行集中之任何物件的相依性。|  
||**0x100000000**|使用此選項來複寫 FILESTREAM 屬性，如果在上指定**varbinary （max)**資料行。 如果您要將資料表複寫至 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 訂閱者，請勿指定這個選項。 具有 FILESTREAM 資料行的資料表複寫[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]不支援訂閱者，不論這個結構描述選項的設定方式。 請參閱相關的選項**0x800000000**。|  
||**0x200000000**|將日期和時間資料類型轉換 (**日期**，**時間**， **datetimeoffset**，和**datetime2**) 中引進[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]資料型別所支援的舊版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
||**0x400000000**|複寫資料與索引的壓縮選項。 如需詳細資訊，請參閱 [Data Compression](../../relational-databases/data-compression/data-compression.md)。|  
||**0x800000000**|設定這個選項即可將 FILESTREAM 資料儲存在訂閱者端的檔案群組中。 如果沒有設定這個選項，FILESTREAM 資料就會儲存在預設檔案群組中。 複寫不會建立檔案群組。因此，如果您設定這個選項，就必須先建立檔案群組，然後再於訂閱者端套用快照集。 如需如何建立物件，然後再套用快照集的詳細資訊，請參閱[前後執行指令碼之後套用快照集](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)。<br /><br /> 請參閱相關的選項**0x100000000**。|  
||**0x1000000000**|將 common language runtime (CLR) 使用者定義型別 (Udt) 轉換成**varbinary （max)**如此 UDT 類型的資料行可以複寫至 「 訂閱者 」 執行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。|  
||**0x2000000000**|將轉換**hierarchyid**資料型別**varbinary （max)**使類型的資料行**hierarchyid**可以複寫到訂閱者執行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 如需有關如何使用**hierarchyid**資料行在複寫資料表中，請參閱[hierarchyid &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
||**0x4000000000**|複寫資料表上任何已篩選的索引。 如需篩選索引的詳細資訊，請參閱[Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)。|  
||**0x8000000000**|將轉換**geography**和**幾何**資料類型為**varbinary （max)**如此這些類型的資料行可以複寫至 「 訂閱者 」 執行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x10000000000**|複寫類型的資料行的索引**geography**和**幾何**。|  
||NULL|系統會自動產生發行項的有效結構描述選項。|  
|**status**|**使用中**|發行資料表的初始處理指令碼在執行中。|  
||**unsynced**|在下次執行快照集代理程式時，執行發行資料表的初始處理指令碼。|  
|**stream_blob_columns**|**true**|當複寫二進位大型物件資料行時，使用資料流最佳化。 不過，特定合併式複寫功能，如邏輯記錄，仍能夠防止使用資料流最佳化。 *stream_blob_columns*設為 true 時，並啟用 FILESTREAM。 這可讓 FILESTREAM 資料的複寫能以最理想的方式執行，並減少記憶體使用量。 若要強制 FILESTREAM 資料表發行項不使用 blob 資料流，設定*stream_blob_columns*設為 false。<br /><br /> **\*\*重要\* \*** 啟用這個記憶體最佳化功能可能會減損合併代理程式同步處理期間的效能。 只有在複寫包含數 MB 資料的資料行時，才應該使用這個選項。|  
||**false**|當複寫二進位大型物件資料行時，不使用最佳化。|  
|**subscriber_upload_options**|**0**|客訂閱在訂閱者端進行的更新沒有任何限制；變更會上傳到發行者。 變更這個屬性可能需要重新初始化現有的訂閱者。|  
||**1**|允許客訂閱在訂閱者端進行變更；但它們不會上傳到發行者。|  
||**2**|不允許客訂閱在訂閱者端進行變更。|  
|**subset_filterclause**||指定水平篩選的 WHERE 子句。 只適用於資料表發行項。<br /><br /> **\*\*重要\* \*** 基於效能考量，我們建議，您不將函數套用至資料行名稱在參數化資料列篩選子句，例如`LEFT([MyColumn]) = SUSER_SNAME()`。 如果您使用[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)在篩選子句和覆寫了 HOST_NAME 值中，您可能必須將資料類型轉換使用[轉換](../../t-sql/functions/cast-and-convert-transact-sql.md)。 如需此案例的最佳作法的詳細資訊，請參閱 「 覆寫 host_name （） 值 」 一節中[Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。|  
|**臨界值**||用於執行的訂閱者的百分比值[!INCLUDE[ssEW](../../includes/ssew-md.md)]或更早版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 **閾值**控制合併代理程式指派新識別範圍的時機。 當使用 threshold 指定的百分比值，合併代理程式會建立新的識別範圍。 時使用**identityrangemanagementoption**設**自動**或**auto_identity_range**設**true**。 只適用於資料表發行項。 如需詳細資訊，請參閱 「 合併式複寫 」 一節[複寫識別資料行](../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
|**verify_resolver_signature**|**1**|驗證自訂解析程式的數位簽章來判斷它是否來自信任來源。|  
||**0**|不驗證自訂解析程式的數位簽章來判斷它是否來自信任來源。|  
|NULL (預設值)||傳回支援的值清單*屬性*。|  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 認可這個預存程序所採取的動作可能使現有的快照集失效。 *force_invalidate_snapshot*是**元**，預設值是**0**。  
  
 **0**指定合併發行項的變更不會使快照集失效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1**表示的合併發行項的變更可能使快照集失效，並且如果有現有的訂閱需要新的快照集，提供要標示為已棄用之現有快照集並產生新的快照集的權限。  
  
 請參閱＜備註＞一節，以了解在變更時需要產生新快照集的屬性。  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 認可這個預存程序所採取的動作可能需要重新初始化現有的訂閱。 *force_reinit_subscription*是**元**，預設值是**0**。  
  
 **0**指定合併發行項的變更不會使訂閱重新初始化。 如果預存程序偵測到變更需要重新初始化現有的訂閱，就會發生錯誤，且不會進行任何變更。  
  
 **1**表示合併發行項的變更會導致現有的訂閱重新初始化，並提供發生訂閱重新初始化的權限。  
  
 請參閱＜備註＞一節，以了解在變更時需要重新初始化所有現有的訂閱之屬性。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changemergearticle**用於合併式複寫中。  
  
 因為**sp_changemergearticle**用來變更一開始以使用指定的發行項屬性[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)，請參閱[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)如需有關這些屬性的詳細資訊。  
  
 變更下列屬性需要產生新的快照集的而且您必須指定值為**1**如*force_invalidate_snapshot*參數：  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **schema_options**  
  
-   **subset_filterclause**  
  
 變更下列屬性需要現有的訂閱重新初始化，而且您必須指定值為**1**如*force_reinit_subscription*參數：  
  
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
  
 指定的值是 3 時**partition_options**，都會清除中繼資料，每當合併代理程式執行和資料分割的快照集到期得更快。 當使用這個選項時，您應該考慮啟用訂閱者要求的資料分割快照集。 如需詳細資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
 設定時**column_tracking**屬性，如果在其他合併式發行集中，已經發行的資料表資料行追蹤必須是正在使用此資料表上現有的發行項的值相同。 這個參數只適用於資料表發行項。  
  
 如果多個發行集發行在相同的基礎資料表上的發行項，變更**delete_tracking**屬性或**compensate_for_errors**一個發行項屬性會導致相同的變更對相同的資料表為基礎的其他文章。  
  
 如果合併處理序所使用的發行者登入/使用者帳戶並沒有正確的資料表權限，就會將無效的變更記錄為衝突。  
  
 值變更時**schema_option**，系統不會執行位元更新。 這表示當您設定**schema_option**使用**sp_changemergearticle**現有位元設定可能已關閉。 若要保留現有的設定，您應該執行[& (位元 AND)](../../t-sql/language-elements/bitwise-and-transact-sql.md)您要設定的值與目前的值之間*schema_option*，這可藉由執行[sp_helpmergearticle](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)。  
  
> [!CAUTION]  
>  當您許多 （百） 的發行項中發行集，而且您執行**sp_changemergearticle**對於其中一個發行項，它可能會花費很長的時間才能完成執行。  
  
## <a name="valid-schema-option-table"></a>有效的結構描述選項表  
 下表描述允許*schema_option*值，根據發行項類型而定。  
  
|發行項類型|結構描述選項值|  
|------------------|--------------------------|  
|**僅限 func 結構描述**|**0x01**和**0x2000**|  
|**僅限索引檢視表結構描述**|**0x01**， **0x040**， **0x0100**， **0x2000**， **0x40000**， **0x1000000**，和**0x200000**|  
|**僅限程序結構描述**|**0x01**和**0x2000**|  
|**table**|所有選項。|  
|**僅限檢視結構描述**|**0x01**， **0x040**， **0x0100**， **0x2000**， **0x40000**， **0x1000000**，和**0x200000**|  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_changemergearticle](../../relational-databases/replication/codesnippet/tsql/sp-changemergearticle-tr_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_changemergearticle**。  
  
## <a name="see-also"></a>請參閱＜  
 [檢視和修改發行項屬性](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergearticle &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
