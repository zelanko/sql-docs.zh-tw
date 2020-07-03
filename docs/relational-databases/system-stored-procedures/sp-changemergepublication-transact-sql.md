---
title: sp_changemergepublication （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergepublication_TSQL
- sp_changemergepublication
helpviewer_keywords:
- sp_changemergepublication
ms.assetid: 81fe1994-7678-4852-980b-e02fedf1e796
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ba7a6785952152632a9435269bc7b4a9b236ad38
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85872519"
---
# <a name="sp_changemergepublication-transact-sql"></a>sp_changemergepublication (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  變更合併式發行集的屬性。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changemergepublication [ @publication= ] 'publication'  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @property = ] 'property'`要針對給定發行集變更的屬性。 *屬性*是**sysname**，它可以是下表所列的其中一個值。  
  
`[ @value = ] 'value'`指定之屬性的新值。 *value*是**Nvarchar （255）**，它可以是下表所列的其中一個值。  
  
 下表描述可變更之發行集的屬性及這些屬性值的限制。  
  
|屬性|值|說明|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|允許匿名訂閱。|  
||**false**|不允許匿名訂閱。|  
|**allow_partition_realignment**|**true**|刪除動作會傳給訂閱者來反映資料分割變更的結果，其方式是移除已不屬於訂閱者資料分割之一部分的資料。 此為預設行為。|  
||**false**|舊資料分割的資料會留在訂閱者上，發行者上對於這項資料的變更並不會複寫到這個訂閱者中， 而是會將訂閱者上做的變更複寫到發行者。 當因為記錄而需要存取舊資料分割中的訂閱資料時，便利用這個方式來保留這份資料。|  
|**allow_pull**|**true**|允許給定發行集的提取訂閱。|  
||**false**|不允許給定發行集的提取訂閱。|  
|**allow_push**|**true**|允許給定發行集的發送訂閱。|  
||**false**|不允許給定發行集的發送訂閱。|  
|**allow_subscriber_initiated_snapshot**|**true**|訂閱者可以起始快照集處理序。|  
||**false**|訂閱者不能起始快照集處理序。|  
|**allow_subscription_copy**|**true**|您可以複製訂閱這個發行集的訂閱資料庫。|  
||**false**|您無法複製訂閱這個發行集的訂閱資料庫。|  
|**allow_synctoalternate**|**true**|允許與這個發行者同步的替代同步夥伴。|  
||**false**|不允許與這個發行者同步的替代同步夥伴。|  
|**allow_web_synchronization**|**true**|可以透過 HTTPS 來同步處理訂閱。|  
||**false**|無法透過 HTTPS 來同步處理訂閱。|  
|**alt_snapshot_folder**||指定快照集替代資料夾的位置。|  
|**automatic_reinitialization_policy**|**1**|在重新初始化訂閱之前，從訂閱者上傳變更。|  
||**0**|重新初始化訂閱，但不先上傳變更。|  
|**centralized_conflicts**|**true**|所有衝突記錄都會儲存在發行者端。 如果您變更這個屬性，就必須重新初始化現有的訂閱者。|  
||**false**|衝突記錄會儲存在衝突解決中失敗的伺服器。 如果您變更這個屬性，就必須重新初始化現有的訂閱者。|  
|**compress_snapshot**|**true**|替代快照集資料夾中的快照集會壓縮成 CAB 格式。 預設快照集資料夾中的快照集無法壓縮。 變更這個屬性需要新的快照集。|  
||**false**|預設不會壓縮快照集。 變更這個屬性需要新的快照集。|  
|**conflict_logging**|**publisher**|衝突記錄會儲存在發行者端。|  
||**預訂**|衝突記錄會儲存在造成衝突的訂閱者端。 [!INCLUDE[ssEW](../../includes/ssew-md.md)]訂閱者不支援 *。*|  
||**既**|衝突記錄會儲存在發行者端和訂閱者端。|  
|**conflict_retention**||**Int** ，指定保留衝突的保留期限（以天為單位）。 將*conflict_retention*設定為**0** ，表示不需要清除衝突。|  
|**description**||發行集的描述。|  
|**dynamic_filters**|**true**|根據動態子句來篩選發行集。|  
||**false**|不動態篩選發行集。|  
|**enabled_for_internet**|**true**|不啟用發行集的網際網路功能。 檔案傳輸通訊協定 (FTP) 可用來將快照集檔案傳送至訂閱者。 發行集的同步處理檔案會放在 C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\ftp 目錄中。|  
||**false**|不啟用發行集的網際網路功能。|  
|**ftp_address**||散發者之 FTP 服務的網路位址。 指定發行集快照集的儲存位置。|  
|**ftp_login**||用來連接 FTP 服務的使用者名稱。|  
|**ftp_password**||用來連接 FTP 服務的使用者密碼。|  
|**ftp_port**||散發者的 FTP 服務通訊埠編號。 指定儲存發行集快照集檔案的 FTP 站台之 TCP 通訊埠編號。|  
|**ftp_subdirectory**||指定在發行集支援利用 FTP 來傳播快照集時，要在何處建立快照集檔案。|  
|**generation_leveling_threshold**|**int**|指定某個層代中包含的變更數目。 層代是指傳遞給發行者或訂閱者的變更集合。|  
|**keep_partition_changes**|**true**|將同步處理最佳化，只有在已變更之資料分割中具有資料列的訂閱者會受到影響。 變更這個屬性需要新的快照集。|  
||**false**|同步處理未最佳化，而當資料分割的資料有了改變時，就會驗證傳給訂閱者的資料分割。 變更這個屬性需要新的快照集。|  
|**max_concurrent_merge**||這是**int** ，代表可以針對發行集執行的並行合併處理數目上限。 如果這個值是 0，表示沒有限制。如果排程同時執行的合併處理超出這個數目，超出的作業便會放在佇列中，等到目前的合併處理完成為止。|  
|**max_concurrent_dynamic_snapshots**||這是一個**int** ，代表產生已篩選資料快照集的最大快照集會話數目，可以同時針對使用參數化資料列篩選的合併式發行集執行。 如果是**0**，則沒有限制。 如果排程同時執行的快照集處理超出這個數目，超出的作業便會放在佇列中，等到目前的合併處理完成為止。|  
|**post_snapshot_script**||指定 **.sql**檔案位置的指標。 在初始同步處理期間，散發代理程式或合併代理程式會先套用所有其他複寫的物件指令碼和資料，然後才執行後快照集 (post-snapshot) 指令碼。 變更這個屬性需要新的快照集。|  
|**pre_snapshot_script**||指定 **.sql**檔案位置的指標。 當在訂閱者端套用快照集時，合併代理程式會在任何複寫的物件指令碼之前，先執行前快照集 (pre-snapshot) 指令碼。 變更這個屬性需要新的快照集。|  
|**publication_compatibility_level**|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
||**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**publish_to_activedirectory**|**true**|這個參數已被取代，支援它的目的，只是為了與舊版的指令碼相容。 您不能再將發行集資訊加入 Active Directory 中。|  
||**false**|從 Active Directory 中移除發行集資訊。|  
|**replicate_ddl**|**1**|在發行者上執行的資料定義語言 (DDL) 陳述式會進行複寫。|  
||**0**|不複寫 DDL 陳述式。|  
|**保存**||這是**int** ，代表要儲存給定發行集之變更的*retention_period_unit*單位數。 如果未在保留期限內同步處理訂閱，且散發者端的清除作業移除了它已收到的暫止變更，訂閱便會到期，必須重新初始化。 允許的最大保留期限是 9999 年 12 月 31 日和目前日期之間的天數。<br /><br /> 注意：合併式發行集的保留期限為24小時寬限期，以配合不同時區的訂閱者。|  
|**retention_period_unit**|**day**|以天為保留週期的指定單位。|  
||**week**|以星期為保留週期的指定單位。|  
||**month**|以月為保留週期的指定單位。|  
||**year**|以年為保留週期的指定單位。|  
|**snapshot_in_defaultfolder**|**true**|快照集檔案儲存在預設快照集資料夾中。|  
||**false**|快照集檔案會儲存在*alt_snapshot_folder*所指定的替代位置中。 這個組合會指定將快照集檔案同時儲存在預設位置和替代位置中。|  
|**snapshot_ready**|**true**|可以使用發行集的快照集。|  
||**false**|無法使用發行集的快照集。|  
|**status**|**active**|發行集在使用狀態中。|  
||**inactive**|發行集在非使用狀態中。|  
|**sync_mode**|**原生**或<br /><br /> **bcp native**|所有資料表的原生模式大量複製程式輸出會用在初始快照集上。|  
||**字母**<br /><br /> 或**bcp 字元**|所有資料表的字元模式大量複製程式輸出會用在初始快照集上，所有非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者也需要如此。|  
|**use_partition_groups**<br /><br /> 注意：使用 partition_groups 之後，如果您要還原為使用**setupbelongs**，並在**changemergearticle**中設定**use_partition_groups = false** ，則在建立快照集之後可能無法正確反映這種情況。 快照集所產生的觸發程序與資料分割群組相容。<br /><br /> 此案例的因應措施是將狀態設定為非作用中、修改**use_partition_groups**，然後將狀態設定為 [作用中]。|**true**|發行集使用預先計算的資料分割。|  
||**false**|發行集不使用預先計算的資料分割。|  
|**validate_subscriber_info**||列出用來擷取訂閱者資訊的函數。 然後驗證用來針對訂閱者確認資訊分割一致的動態篩選準則。|  
|**web_synchronization_url**||Web 同步處理所用的網際網路 URL 預設值。|  
|NULL (預設值)||傳回*屬性*的支援值清單。|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`認可這個預存程式所採取的動作可能會使現有的快照集失效。 *force_invalidate_snapshot*是**bit**，預設值是**0**。  
  
 **0**指定變更發行集並不會使快照集失效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1**指定變更發行集可能會使快照集。 如果有現有的訂閱需要新的快照集，這個值會提供要標示為已棄用之現有快照集的權限，此時會產生新的快照集。  
  
 請參閱「備註」一節，以了解在變更時需要產生新快照集的屬性。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`認可這個預存程式所採取的動作可能需要重新初始化現有的訂閱。 *force_reinit_subscription*是**位**，預設值是**0**。  
  
 **0**指定變更發行集不需要重新初始化訂閱。 如果預存程序偵測到變更需要重新初始化現有的訂閱，就會發生錯誤，且不會進行任何變更。  
  
 **1**指定變更發行集會使現有的訂閱重新初始化，並提供將發生之訂閱重新初始化的許可權。  
  
 請參閱＜備註＞一節，以了解在變更時需要重新初始化所有現有的訂閱之屬性。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changemergepublication**用於合併式複寫中。  
  
 變更下列屬性需要產生新的快照集。 您必須針對*force_invalidate_snapshot*參數指定**1**的值。  
  
-   **alt_snapshot_folder**  
  
-   **compress_snapshot**  
  
-   **dynamic_filters**  
  
-   **ftp_address**  
  
-   **ftp_login**  
  
-   **ftp_password**  
  
-   **ftp_port**  
  
-   **ftp_subdirectory**  
  
-   **post_snapshot_script**  
  
-   **publication_compatibility_level** （僅限**80SP3** ）  
  
-   **pre_snapshot_script**  
  
-   **snapshot_in_defaultfolder**  
  
-   **sync_mode**  
  
-   **use_partition_groups**  
  
 變更下列屬性需要重新初始化現有的訂閱。 您必須針對*force_reinit_subscription*參數指定**1**的值。  
  
-   **dynamic_filters**  
  
-   **validate_subscriber_info**  
  
 若要使用*publish_to_active_directory*來列出要 Active Directory 的發行集物件， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件必須已在 Active Directory 中建立。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_changemergepublication](../../relational-databases/replication/codesnippet/tsql/sp-changemergepublicatio_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_changemergepublication**。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
