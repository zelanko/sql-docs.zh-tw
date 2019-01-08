---
title: sp_helpmergepublication & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepublication
- sp_helpmergepublication_TSQL
helpviewer_keywords:
- sp_helpmergepublication
ms.assetid: dfe1e1e1-9a65-406a-aced-6385a078e135
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3328facfd0f19d6fa5f5f02a614c45cd22a79f76
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754121"
---
# <a name="sphelpmergepublication-transact-sql"></a>sp_helpmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關合併式發行集的資訊。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpmergepublication [ [ @publication = ] 'publication' ]  
    [ , [ @found = ] 'found' OUTPUT ]  
    [ , [ @publication_id = ] 'publication_id' OUTPUT ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>引數  
 [ @publication **=** ] **'***出版物***'**  
 發行集的名稱。 *發行集*已**sysname**，預設值是**%**，傳回目前資料庫中所有合併式發行集的相關資訊。  
  
 [ @found **=** ] **'***找到***'** 輸出  
 這是指示傳回資料列的旗標。 *找到*已**int**和一個 OUTPUT 參數，預設值是 NULL。 **1**表示找到發行集。 **0**指出找不到發行集。  
  
 [ @publication_id **=**] **'***publication_id&lt***'** 輸出  
 這是發行集識別碼。 *publication_id&lt*已**uniqueidentifier**和一個 OUTPUT 參數，預設值是 NULL。  
  
 [ @reserved **=**] **'***保留***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *保留*已**nvarchar(20)**，預設值是 NULL。  
  
 [ @publisher **=** ] **'***發行者***'**  
 發行者的名稱。 *發行者*已**sysname**，預設值是 NULL。  
  
 [@publisher_db **=** ] **'***publisher_db***'**  
 發行集資料庫的名稱。 *publisher_db*已**sysname**，預設值是 NULL。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|id|**int**|結果集清單中的發行集循序排列順序。|  
|NAME|**sysname**|發行集的名稱。|  
|description|**nvarchar(255)**|發行集的描述。|  
|status|**tinyint**|指示發行集資料的可用時機。|  
|retention|**int**|儲存發行集中的發行項變更相關中繼資料時，所需的時間。 這段時間的單位可以是天、週、月或年。 如需有關單位的資訊，請參閱 retention_period_unit 欄。|  
|sync_mode|**tinyint**|這個發行集的同步處理模式：<br /><br /> **0** = 原生大量複製程式 (**bcp**公用程式)<br /><br /> **1** = 字元大量複製|  
|allow_push|**int**|判斷是否可以針對給定發行集建立發送訂閱。 **0**表示不允許發送訂閱。|  
|allow_pull|**int**|判斷是否可以針對給定發行集建立提取訂閱。 **0**表示不允許提取訂閱。|  
|allow_anonymous|**int**|判斷是否可以針對給定發行集建立匿名訂閱。 **0**表示不允許匿名訂閱。|  
|centralized_conflicts|**int**|判斷是否將衝突記錄儲存在給定的發行者上：<br /><br /> **0** = 將衝突記錄儲存在發行者端和造成衝突的訂閱者端。<br /><br /> **1** = 所有衝突記錄儲存在 「 發行者 」。|  
|priority|**float(8)**|回送訂閱的優先權。|  
|snapshot_ready|**tinyint**|指示這個發行集的快照集是否已備妥：<br /><br /> **0** = 快照集可供使用。<br /><br /> **1** = 快照集未備妥可用。|  
|publication_type|**int**|發行集的類型：<br /><br /> **0** = 快照集。<br /><br /> **1** = 交易式。<br /><br /> **2** = 合併式。|  
|pubid|**uniqueidentifier**|這個發行集的唯一識別碼。|  
|snapshot_jobid|**binary(16)**|快照集代理程式的作業識別碼。 若要取得的項目中的快照集作業[sysjobs](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)系統資料表中，您必須這個十六進位值轉換成**uniqueidentifier**。|  
|enabled_for_internet|**int**|判斷是否啟用發行集的網際網路功能。 如果**1**，發行集的同步處理檔案會放入`C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\Ftp`目錄。 使用者必須建立檔案傳輸通訊協定 (FTP) 目錄。 如果**0**，發行集未啟用網際網路存取。|  
|dynamic_filter|**int**|指示是否要使用參數化資料列篩選器。 **0**表示不會使用參數化資料列篩選器。|  
|has_subscription|**bit**|指示發行集是否有任何訂閱。 **0**表示目前沒有任何訂閱此發行集。|  
|snapshot_in_default_folder|**bit**|指定是否將快照集檔案儲存在預設資料夾中。<br /><br /> 如果**1**，可以在預設資料夾中找到快照集檔案。<br /><br /> 如果**0**，快照集檔案會儲存在所指定的替代位置**alt_snapshot_folder**。 替代位置可以在另一部伺服器、網路磁碟機或抽取式媒體 (如 CD-ROM 或抽取式磁碟) 中。 另外，您也可以將快照集檔案儲存在 FTP 站台中，供訂閱者以後擷取它們。<br /><br /> 注意：這個參數可以是 true 中, 仍有位置**alt_snapshot_folder**參數。 這個組合會指定將快照集檔案同時儲存在預設位置和替代位置中。|  
|alt_snapshot_folder|**nvarchar(255)**|指定快照集替代資料夾的位置。|  
|pre_snapshot_script|**nvarchar(255)**|指定的指標 **.sql**套用在訂閱者端的快照集時，指令碼檔案，「 合併代理程式會執行任何複寫的物件之前。|  
|post_snapshot_script|**nvarchar(255)**|指定的指標 **.sql**檔案，執行合併代理程式在所有其他複寫物件指令碼和資料的初始同步處理期間，套用。|  
|compress_snapshot|**bit**|指定的快照集，會寫入**alt_snapshot_folder**位置壓縮成[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。|  
|ftp_address|**sysname**|這是散發者之 FTP 服務的網路位址。 指定發行集快照集檔案所在的位置，以便合併代理程式能夠加以收取。|  
|ftp_port|**int**|這是散發者的 FTP 服務通訊埠編號。 **ftp_port**具有預設值是**21**。 指定發行集快照集檔案所在的位置，以便合併代理程式能夠加以收取。|  
|ftp_subdirectory|**nvarchar(255)**|指定當利用 FTP 來傳遞快照集時，合併代理程式能夠從中收取快照集檔案的位置。|  
|ftp_login|**sysname**|這是用於連接到 FTP 服務的使用者名稱。|  
|conflict_retention|**int**|指定衝突的保留期限 (以天為單位)。 過了指定天數之後，便從衝突資料表中清除衝突資料列。|  
|keep_partition_changes|**int**|指定這個發行集是否進行最佳化的同步處理。 **keep_partition_changes**具有預設值是**0**。 值為**0**表示同步處理未最佳化，而且資料分割中的資料變更時，會驗證傳送給所有訂閱者資料分割。<br /><br /> **1**表示同步處理最佳化，而且只有擁有已變更的資料分割中的資料列的訂閱者會受到影響。<br /><br /> 注意：依預設，合併式發行集會使用預先計算的資料分割，以取得高於這個選項的最佳化程度。 如需詳細資訊，請參閱 < [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)並[最佳化 Parameterized Filter Performance with Precomputed Partitions&lt](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。|  
|allow_subscription_copy|**int**|指定是否已啟用複製訂閱這個發行集之訂閱資料庫的能力。 值為**0**表示不允許複製。|  
|allow_synctoalternate|**int**|指定是否允許替代的同步處理夥伴與這個發行者同步。 值為**0**表示不允許同步夥伴。|  
|validate_subscriber_info|**nvarchar(500)**|列出用於擷取訂閱者資訊以及驗證訂閱者參數化資料列篩選器準則的函數。 它可以協助您確認每項合併的資訊分割都一致。|  
|backward_comp_level|**int**|資料庫相容性層級，它可以是下列項目之一：<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_activedirectory|**bit**|指定發行集資訊是否發行到 Active Directory。 值為**0**表示發行集資訊不是從 Active Directory。<br /><br /> 這個參數已被取代，支援它的目的，只是為了與舊版的指令碼相容。 您不能再將發行集資訊加入 Active Directory 中。|  
|max_concurrent_merge|**int**|並行合併處理序的數目。 如果**0**，在任何給定時間執行的並行合併處理序數目沒有限制。|  
|max_concurrent_dynamic_snapshots|**int**|可以針對合併式發行集來執行的最大並行已篩選資料快照集工作階段數目。 如果**0**，能夠同時針對的發行集之任何指定時間執行的並行已篩選的資料快照集工作階段最大數目沒有限制。|  
|use_partition_groups|**int**|判斷是否使用預先計算的資料分割。 值為**1**表示預先計算的分割區使用。|  
|num_of_articles|**int**|發行集中的發行項數目。|  
|replicate_ddl|**int**|是否複寫已發行的資料表之結構描述變更。 值為**1**表示複寫結構描述變更。|  
|publication_number|**smallint**|指派給這個發行集的號碼。|  
|allow_subscriber_initiated_snapshot|**bit**|判斷訂閱者是否能夠起始產生已篩選資料快照集的程序。 值為**1**表示訂閱者可以起始快照集處理。|  
|allow_web_synchronization|**bit**|判斷是否啟用發行集的 Web 同步處理。 值為**1**表示啟用 Web 同步處理。|  
|web_synchronization_url|**nvarchar(500)**|Web 同步處理所用的網際網路 URL。|  
|allow_partition_realignment|**bit**|判斷當修改發行者的資料列造成資料分割的變更時，是否要將刪除動作傳給訂閱者。 值為**1**表示，刪除動作傳給訂閱者。  如需詳細資訊，請參閱 < [sp_addmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。|  
|retention_period_unit|**tinyint**|定義保留時所使用的單位。 這個值可以是下列其中一個值：<br /><br /> **0** = 日<br /><br /> **1** = 週<br /><br /> **2** = 月<br /><br /> **3** = 年|  
|has_downloadonly_articles|**bit**|指出是否有任何屬於發行集的發行項是只限下載的發行項。 值為**1**表示有只限下載的發行項。|  
|decentralized_conflicts|**int**|指出是否將衝突記錄儲存在造成衝突的訂閱者端。 值為**0**表示衝突記錄不會儲存在訂閱者。 1 的值表示衝突記錄會儲存在訂閱者端。|  
|generation_leveling_threshold|**int**|指定某個層代中包含的變更數目。 層代是指傳遞給發行者或訂閱者的變更集合|  
|automatic_reinitialization_policy|**bit**|指出在自動重新初始化之前，是否從訂閱者上傳變更。 值為**1**指出在自動重新初始化發生之前，會從訂閱者上載變更。 0 的值指出在自動重新初始化之前，不會上傳變更。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 sp_helpmergepublication 用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 發行集的發行集存取清單成員可以執行這個發行集的 sp_helpmergepublication。 發行集資料庫的 db_owner 固定資料庫角色成員能夠執行 sp_helpmergepublication，以取得所有發行集的相關資訊。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_helpmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-helpmergepublication-_1.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addmergepublication &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
