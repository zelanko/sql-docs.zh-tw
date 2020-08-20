---
description: sp_changearticle (Transact-SQL)
title: sp_changearticle (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changearticle
- sp_changearticle_TSQL
helpviewer_keywords:
- sp_changearticle
ms.assetid: 24c33ca5-f03a-4417-a267-131ca5ba6bb5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 46afab7da64374922f20e5736c2a3d31217056b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464464"
---
# <a name="sp_changearticle-transact-sql"></a>sp_changearticle (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  變更交易式或快照式發行集中之發行項的屬性。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changearticle [ [@publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是包含發行項的發行集名稱。 *發行* 集是 **sysname**，預設值是 Null。  
  
`[ @article = ] 'article'` 這是要變更其屬性的發行項名稱。 *文章* 是 **sysname**，預設值是 Null。  
  
`[ @property = ] 'property'` 這是要變更的發行項屬性。 *屬性* 是 **Nvarchar (100) **。  
  
`[ @value = ] 'value'` 這是發行項屬性的新值。 *值* 為 **Nvarchar (255) **。  
  
 下表描述發行項的屬性及這些屬性的值。  
  
|屬性|值|描述|  
|--------------|------------|-----------------|  
|**creation_script**||用來建立目標資料表之發行項結構描述指令碼的路徑和名稱。 預設值是 NULL。|  
|**del_cmd**||要執行的 DELETE 陳述式；否則，便從記錄檔中建構它。|  
|**description**||發行項的新描述項目。|  
|**dest_object**||提供這個項目的目的，是為了與舊版相容。 使用 **dest_table**。|  
|**dest_table**||新的目的地資料表。|  
|**destination_owner**||目的地物件的擁有者名稱。|  
|**濾波器**||用於篩選資料表 (水平篩選) 的新預存程序。 預設值是 NULL。 點對點複寫發行集的這個項目不能變更。|  
|**fire_triggers_on_snapshot**|**true**|在套用初始快照集時，執行複寫的使用者觸發程序。<br /><br /> 注意：若要複寫觸發程式， *schema_option* 的位元遮罩值必須包含 **0x100**值。|  
||**false**|在套用初始快照集時，不執行複寫的使用者觸發程序。|  
|**identity_range**||控制在訂閱者端指派的指派識別範圍大小。 不支援點對點複寫使用這個項目。|  
|**ins_cmd**||要執行的 INSERT 陳述式；否則，便從記錄檔中建構它。|  
|**pre_creation_cmd**||可以在套用同步處理之前，卸除、刪除或截斷目的地資料表的預先建立命令。|  
||無|不使用命令。|  
||**drop**|卸除目的地資料表。|  
||**delete**|刪除目的地資料表。|  
||**截斷**|截斷目的地資料表。|  
|**pub_identity_range**||控制在訂閱者端指派的指派識別範圍大小。 不支援點對點複寫使用這個項目。|  
|**schema_option**||指定給定發行項之結構描述產生選項的點陣圖。 *schema_option* 為 **binary (8) **。 如需詳細資訊，請參閱本主題稍後的＜備註＞一節。|  
||**0x00**|停用快照集代理程式的指令碼。|  
||**0x01**|產生物件的建立作業 (CREATE TABLE、CREATE PROCEDURE 等)。|  
||**0x02**|如果已定義的話，便產生傳播發行項變更的預存程序。|  
||**0x04**|識別欄位的指令碼是利用 IDENTITY 屬性來編寫的。|  
||**0x08**|複寫 **時間戳記** 資料行。 如果未設定，則會將 **時間戳記** 資料行複寫為 **二進位**。|  
||**0x10**|產生對應的叢集索引。|  
||**0x20**|在訂閱者端將使用者定義資料類型 (UDT) 轉換成基底資料型別。 如果 UDT 資料行是主索引鍵的一部分或計算資料行參考 UDT 資料行，則當 UDT 資料行中有 CHECK 或 DEFAULT 條件約束時，就不能使用這個選項。 不支援 Oracle 發行者使用這個值。|  
||**0x40**|產生對應的非叢集索引。|  
||**0x80**|包括主索引鍵的宣告式參考完整性。|  
||**0x100**|複寫資料表發行項的使用者觸發程序 (如果定義的話)。|  
||**0x200**|複寫 FOREIGN KEY 條件約束。 如果參考的資料表不是發行集的一部分，便不會複寫發行資料表上任何的 FOREIGN KEY 條件約束。|  
||**0x400**|複寫 CHECK 條件約束。|  
||**0x800**|複寫預設值。|  
||**0x1000**|複寫資料行層級定序。|  
||**0x2000**|複寫與已發行之發行項來源物件相關聯的擴充屬性。|  
||**0x4000**|如果資料表發行項上定義了唯一索引鍵，便複寫唯一索引鍵。|  
||**0x8000**|複寫資料表發行項的主索引鍵和唯一索引鍵，來做為使用 ALTER TABLE 陳述式的條件約束。<br /><br /> 注意：此選項已被取代。 請改用 **0x80** 和 **0x4000** 。|  
||**0x10000**|將 CHECK 條件約束複寫成 NOT FOR REPLICATION，以免在同步處理期間強制執行條件約束。|  
||**0x20000**|將 FOREIGN KEY 條件約束複寫成 NOT FOR REPLICATION，以免在同步處理期間強制執行條件約束。|  
||**0x40000**|複寫資料分割資料表或索引的相關聯檔案群組。|  
||**0x80000**|複寫資料分割資料表的資料分割配置。|  
||**0x100000**|複寫資料分割索引的資料分割配置。|  
||**0x200000**|複寫資料表統計資料。|  
||**0x400000**|預設繫結|  
||**0x800000**|規則繫結|  
||**0x1000000**|全文檢索索引|  
||**0x2000000**|不會複寫系結至 **xml** 資料行的 xml 架構集合。|  
||**0x4000000**|複寫 **xml** 資料行上的索引。|  
||**0x8000000**|建立訂閱者目前還沒有的任何結構描述。|  
||**0x10000000**|將訂閱者上的 **xml** 資料行轉換為 **Ntext** 。|  
||**0x20000000**|將大型物件資料類型轉換 (**Nvarchar (max) **、 **Varchar (max) **和 **Varbinary (最大 **) ) ，這是在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 支援的資料類型中所引進 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 。|  
||**0x40000000**|複寫權限。|  
||**0x80000000**|嘗試卸除對於不在發行集中之任何物件的相依性。|  
||**0x100000000**|如果在 **Varbinary (max) ** 資料行上指定 FILESTREAM 屬性，請使用此選項來複寫它。 如果您要將資料表複寫至 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 訂閱者，請勿指定這個選項。 不支援將具有 FILESTREAM 資料行的資料表複寫至 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 訂閱者，不論此架構選項的設定方式為何。<br /><br /> 請參閱相關選項 **0x800000000**。|  
||**0x200000000**|將日期和時間資料類型，轉換為舊版所支援的資料類型中所引進**的日期、****時間**、 **datetimeoffset**和**datetime2**)  ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
||**0x400000000**|複寫資料與索引的壓縮選項。 如需詳細資訊，請參閱 [Data Compression](../../relational-databases/data-compression/data-compression.md)。|  
||**0x800000000**|設定這個選項即可將 FILESTREAM 資料儲存在訂閱者端的檔案群組中。 如果沒有設定這個選項，FILESTREAM 資料就會儲存在預設檔案群組中。 複寫不會建立檔案群組。因此，如果您設定這個選項，就必須先建立檔案群組，然後再於訂閱者端套用快照集。 如需如何在套用快照集之前建立物件的詳細資訊，請參閱 [在套用快照集之前和之後執行腳本](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)。<br /><br /> 請參閱相關選項 **0x100000000**。|  
||**0x1000000000**|將 common language runtime (CLR) 使用者定義型別（ (Udt) 大於8000位元組）轉換成 **Varbinary (max) ** ，以便將 udt 類型的資料行複寫至執行的訂閱者 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。|  
||**0x2000000000**|將 **hierarchyid** 資料類型轉換成 **Varbinary (max) ** ，以便將 **hierarchyid** 類型的資料行複寫至正在執行的訂閱者 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。 如需有關如何在複寫資料表中使用 **hierarchyid** 資料行的詳細資訊，請參閱 [hierarchyid &#40;transact-sql&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)。|  
||**0x4000000000**|複寫資料表上任何已篩選的索引。 如需篩選索引的詳細資訊，請參閱 [建立篩選的索引](../../relational-databases/indexes/create-filtered-indexes.md)。|  
||**0x8000000000**|將 **geography** 和 **geometry** 資料類型轉換成 **Varbinary (max) ** ，以便將這些類型的資料行複寫至正在執行的訂閱者 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。|  
||**0x10000000000**|複寫 **geography** 和 **geometry**類型之資料行的索引。|  
||**0x20000000000**|複寫資料行的 SPARSE 屬性。 如需此屬性的詳細資訊，請參閱 [使用稀疏資料行](../../relational-databases/tables/use-sparse-columns.md)。|  
||**0x40000000000**|啟用快照集代理程式的腳本，以在訂閱者上建立記憶體優化的資料表。|  
||**0x80000000000**|將叢集索引轉換為記憶體優化發行項的非叢集索引。|  
|**status**||指定屬性的新狀態。|  
||**dts horizontal partitions**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
||**include column names**|資料行名稱包括在複寫的 INSERT 陳述式中。|  
||**no column names**|資料行名稱不包括在複寫的 INSERT 陳述式中。|  
||**no dts horizontal partitions**|發行項的水平資料分割並非由可轉換的訂閱來定義。|  
||無|清除 [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md) 資料表中的所有狀態選項，並將發行項標示為非作用中。|  
||**parameters**|利用參數化的命令，將變更傳播到訂閱者。 這是新發行項的預設值。|  
||**字串**|利用字串常值，將變更傳播到訂閱者。|  
|**sync_object**||用於產生同步處理輸出檔之資料表或檢視的名稱。 預設值是 NULL。 不支援 Oracle 發行者使用這個值。|  
|**資料表空間**||識別 Oracle 資料庫發行的發行項之記錄資料表所用的資料表空間。 如需詳細資訊，請參閱[管理 Oracle 資料表空間](../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md)。|  
|**threshold**||用來控制散發代理程式指派新識別範圍之時機的百分比值。 不支援點對點複寫使用這個項目。|  
|**type**||不支援 Oracle 發行者使用這個值。|  
||**logbased**|記錄式發行項。|  
||**logbased manualboth**|記錄式且含有手動篩選準則和手動檢視的發行項。 此選項需要同時設定 *sync_object* 和 *篩選* 屬性。 不支援 Oracle 發行者使用這個值。|  
||**logbased manualfilter**|記錄式且含有手動篩選準則的發行項。 此選項需要同時設定 *sync_object* 和 *篩選* 屬性。 不支援 Oracle 發行者使用這個值。|  
||**logbased manualview**|含有手動檢視的記錄式發行項。 此選項需要同時設定 *sync_object* 屬性。 不支援 Oracle 發行者使用這個值。|  
||**索引 viewlogbased**|記錄式索引檢視發行項。 不支援 Oracle 發行者使用這個值。 這種類型的發行項不需要個別發行基底資料表。|  
||**索引 viewlogbased manualboth**|記錄式且含有手動篩選和手動檢視的索引檢視發行項。 此選項需要同時設定 *sync_object* 和 *篩選* 屬性。 這種類型的發行項不需要個別發行基底資料表。 不支援 Oracle 發行者使用這個值。|  
||**索引 viewlogbased manualfilter**|記錄式且含有手動篩選準則的索引檢視發行項。 此選項需要同時設定 *sync_object* 和 *篩選* 屬性。 這種類型的發行項不需要個別發行基底資料表。 不支援 Oracle 發行者使用這個值。|  
||**索引 viewlogbased manualview**|含有手動檢視的記錄式索引檢視發行項。 此選項需要同時設定 *sync_object* 屬性。 這種類型的發行項不需要個別發行基底資料表。 不支援 Oracle 發行者使用這個值。|  
|**upd_cmd**||要執行的 UPDATE 陳述式；否則，便從記錄檔中建構它。|  
|NULL|NULL|傳回可變更的發行項屬性清單。|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 認可這個預存程式所採取的動作可能使現有的快照集失效。 *force_invalidate_snapshot* 是 **bit**，預設值是 **0**。  
  
 **0** 指定發行項的變更不會使快照集失效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1** 指定發行項的變更可能使快照集失效，如果有現有的訂閱需要新的快照集，則會將現有快照集的許可權標示為已淘汰，並產生新的快照集。  
  
 請參閱＜備註＞一節，以了解在變更時需要產生新快照集的屬性。  
  
`[ @force_reinit_subscription = ]force_reinit_subscription_` 認可這個預存程式所採取的動作可能需要重新初始化現有的訂閱。 *force_reinit_subscription* 是 **bit** ，預設值是 **0**。  
  
 **0** 指定發行項的變更不會使訂閱重新初始化。 如果預存程序偵測到變更需要重新初始化現有的訂閱，就會發生錯誤，且不會進行任何變更。  
  
 **1** 指定發行項的變更會使現有的訂閱重新初始化，且會提供將發生之訂閱重新初始化的許可權。  
  
 請參閱＜備註＞一節，以了解在變更時需要重新初始化所有現有的訂閱之屬性。  
  
`[ @publisher = ] 'publisher'` 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *publisher* 是 **sysname**，預設值是 Null。  
  
> [!NOTE]  
>  在發行者上變更發行項屬性時，不應使用「*發行者*」 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_changearticle** 用於快照式複寫和異動複寫中。  
  
 當發行項屬於支援點對點異動複寫的發行集時，您只能變更 **描述**、 **ins_cmd**、 **upd_cmd**和 **del_cmd** 屬性。  
  
 變更下列任何屬性都需要產生新的快照集，而且您必須為*force_invalidate_snapshot*參數指定**1**的值：  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **ins_cmd**  
  
-   **pre_creation_cmd**  
  
-   **schema_options**  
  
-   **upd_cmd**  
  
 變更下列任何屬性都需要重新初始化現有的訂閱，而且您必須為*force_reinit_subscription*參數指定**1**的值。  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **濾波器**  
  
-   **ins_cmd**  
  
-   **status**  
  
-   **upd_cmd**  
  
 在現有的發行集中，您可以使用 **sp_changearticle** 來變更發行項，而不需要卸載和重新建立整個發行集。  
  
> [!NOTE]  
>  變更 *schema_option*的值時，系統不會執行位更新。 這表示當您使用**sp_changearticle**設定*schema_option*時，可能會關閉現有的位設定。 若要保留現有的設定，您應該在您要設定的值與目前的*schema_option*值（可透過執行[sp_helparticle](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)判斷）之間，執行[| (位或) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) 。  
  
## <a name="valid-schema-options"></a>有效結構描述選項  
 下表描述 schema_option 的可*schema_option*值（以複寫類型為基礎） (顯示在上方) ，而發行項類型 (顯示于第一個資料行) 。  
  
| 發行項類型 | 複寫類型-交易式 | 複寫類型-快照集 |
| ------------ | -------------------------------- | --------------------------- |
|**logbased**|所有選項|所有選項但 **0x02**|  
|**logbased manualfilter**|所有選項|所有選項但 **0x02**|  
|**logbased manualview**|所有選項|所有選項但 **0x02**|  
|**indexed view logbased**|所有選項|所有選項但 **0x02**|  
|**indexed view logbased manualfilter**|所有選項|所有選項但 **0x02**|  
|**indexed view logbased manualview**|所有選項|所有選項但 **0x02**|  
|**indexed view logbase manualboth**|所有選項|所有選項但 **0x02**|  
|**proc exec**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和 **0x80000000**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和 **0x80000000**|  
|**serializable proc exec**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和 **0x80000000**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和 **0x80000000**|  
|**proc schema only**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和 **0x80000000**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和 **0x80000000**|  
|**view schema only**|**0x01**、 **0x010**、 **0x020**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x100000**、 **0x200000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x40000000**和 **0x80000000**|**0x01**、 **0x010**、 **0x020**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x100000**、 **0x200000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x40000000**和 **0x80000000**|  
|**func schema only**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和 **0x80000000**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和 **0x80000000**|  
|**indexed view schema only**|**0x01**、 **0x010**、 **0x020**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x100000**、 **0x200000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x40000000**和 **0x80000000**|**0x01**、 **0x010**、 **0x020**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x100000**、 **0x200000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x40000000**和 **0x80000000**|  
  
> [!NOTE]
>  如果是佇列更新發行集，則必須啟用**0x80**的*schema_option*值。 非發行集支援的 *schema_option* 值為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ： **0x01**、 **0x02**、 **0x10**、 **0x40**、 **0x80**、 **0x1000** 和 **0x4000**。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_changetranarticle](../../relational-databases/replication/codesnippet/tsql/sp-changearticle-transac_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_changearticle**。  
  
## <a name="see-also"></a>另請參閱  
 [查看和修改發行項屬性](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addarticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_droparticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)  
  
  
