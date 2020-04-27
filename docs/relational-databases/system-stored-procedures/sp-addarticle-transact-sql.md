---
title: sp_addarticle （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addarticle
- sp_addarticle_TSQL
helpviewer_keywords:
- sp_addarticle
ms.assetid: 0483a157-e403-4fdb-b943-23c1b487bef0
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: e337e04714b0d8dcc9a8227ca48ad9dc33dcc3dc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "68811392"
---
# <a name="sp_addarticle-transact-sql"></a>sp_addarticle (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  建立一個發行項，將它加入發行集中。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addarticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
    [ , [ @source_table = ] 'source_table' ]  
    [ , [ @destination_table = ] 'destination_table' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @type = ] 'type' ]   
    [ , [ @filter = ] 'filter' ]   
    [ , [ @sync_object= ] 'sync_object' ]   
        [ , [ @ins_cmd = ] 'ins_cmd' ]   
    [ , [ @del_cmd = ] 'del_cmd' ]   
        [ , [ @upd_cmd = ] 'upd_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @filter_clause = ] 'filter_clause' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @status = ] status ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @sync_object_owner = ] 'sync_object_owner' ]   
    [ , [ @filter_owner = ] 'filter_owner' ]   
    [ , [ @source_object = ] 'source_object' ]   
    [ , [ @artid = ] article_ID  OUTPUT ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @use_default_datatypes = ] use_default_datatypes  
    [ , [ @identityrangemanagementoption = ] identityrangemanagementoption ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @fire_triggers_on_snapshot = ] 'fire_triggers_on_snapshot' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是包含發行項的發行集名稱。 這個名稱在資料庫內必須是唯一的。 *發行*集是**sysname**，沒有預設值。  
  
`[ @article = ] 'article'`這是發行項的名稱。 這個名稱在發行集內必須是唯一的。 *文章*是**sysname**，沒有預設值。  
  
`[ @source_table = ] 'source_table'`這個參數已被取代;請改用*source_object* 。  
  
 *這個參數不支援 Oracle 發行者。*  
  
`[ @destination_table = ] 'destination_table'`這是目的地（訂閱）資料表的名稱（如果與*source_table*或預存程式不同）。 *destination_table*是**sysname**，預設值是 Null，表示*source_table*等於*destination_table * *。*  
  
`[ @vertical_partition = ] 'vertical_partition'`啟用和停用資料表發行項的資料行篩選。 *vertical_partition*為**Nchar （5）**，預設值為 FALSE。  
  
 **false**表示沒有垂直篩選，而且會發行所有資料行。  
  
 **true**會清除所有資料行，但宣告的主鍵、沒有預設值的可為 null 資料行，以及唯一索引鍵資料行除外。 資料行是使用[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)來加入。  
  
`[ @type = ] 'type'`這是發行項的類型。 *類型*為**sysname**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**aggregate schema only**|只含結構描述的彙總函式。|  
|**func schema only**|只含結構描述的函數。|  
|**indexed view logbased**|記錄式索引檢視發行項。 不支援 Oracle 發行者使用這個值。 這種類型的發行項不需要個別發行基底資料表。|  
|**indexed view logbased manualboth**|記錄式且含有手動篩選和手動檢視的索引檢視發行項。 此選項需要您同時指定*sync_object*和*篩選*參數。 這種類型的發行項不需要個別發行基底資料表。 不支援 Oracle 發行者使用這個值。|  
|**indexed view logbased manualfilter**|記錄式且含有手動篩選準則的索引檢視發行項。 此選項需要您同時指定*sync_object*和*篩選*參數。 這種類型的發行項不需要個別發行基底資料表。 不支援 Oracle 發行者使用這個值。|  
|**indexed view logbased manualview**|含有手動檢視的記錄式索引檢視發行項。 此選項需要您指定*sync_object*參數。 這種類型的發行項不需要個別發行基底資料表。 不支援 Oracle 發行者使用這個值。|  
|**indexed view schema only**|只含結構描述的索引檢視。 這種類型的發行項也必須發行基底資料表。|  
|**logbased** （預設值）|記錄式發行項。|  
|**logbased manualboth**|記錄式且含有手動篩選準則和手動檢視的發行項。 此選項需要您同時指定*sync_object*和*篩選*參數。 不支援 Oracle 發行者使用這個值。|  
|**logbased manualfilter**|記錄式且含有手動篩選準則的發行項。 此選項需要您同時指定*sync_object*和*篩選*參數。 不支援 Oracle 發行者使用這個值。|  
|**logbased manualview**|含有手動檢視的記錄式發行項。 此選項需要您指定*sync_object*參數。 不支援 Oracle 發行者使用這個值。|  
|**proc exec**|將執行預存程序複寫到發行項的所有訂閱者。 不支援 Oracle 發行者使用這個值。 建議您使用**serializable proc exec**選項，而不要使用**proc exec**。 如需詳細資訊，請參閱在[異動複寫中發行預存程式執行](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)中的「預存程式執行文章的類型」一節。 異動資料擷取啟用時無法使用。|  
|**proc schema only**|只含結構描述的程序。 不支援 Oracle 發行者使用這個值。|  
|**serializable proc exec**|只在預存程序是執行於可序列化交易的環境之內時，才複寫執行預存程序。 不支援 Oracle 發行者使用這個值。<br /><br /> 此程序也必須在明確的交易中執行，如此才能複製該程序。|  
|**view schema only**|只含結構描述的檢視。 不支援 Oracle 發行者使用這個值。 使用此選項時，您也必須發行基底資料表。|  
  
`[ @filter = ] 'filter'`這是用來以水準方式篩選資料表的預存程式（使用 FOR REPLICATION 建立）。 *filter*是**Nvarchar （386）**，預設值是 Null。 [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)和[sp_articlefilter](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)必須以手動方式執行，才能建立 view 和 filter 預存程式。 如果不是 NULL，便不會建立篩選程序 (假設預存程序是手動建立)。  
  
`[ @sync_object = ] 'sync_object'`這是用來產生用來表示此發行項之快照集的資料檔案的資料表或視圖名稱。 *sync_object*是**Nvarchar （386）**，預設值是 Null。 如果是 Null，則會呼叫[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)來自動建立用來產生輸出檔的視圖。 加入具有[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)的任何資料行之後，就會發生這種情況。 如果不是 NULL，便不會建立檢視 (假設檢視是手動建立)。  
  
`[ @ins_cmd = ] 'ins_cmd'`這是在複寫此發行項的插入時，所使用的複寫命令類型。 *ins_cmd*是**Nvarchar （255）**，它可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**無**|不採取任何動作。|  
|**CALL sp_MSins_**<br /> **_table_** （預設值）<br /><br /> -或-<br /><br /> **CALL custom_stored_procedure_name**|呼叫要在訂閱者端執行的預存程序。 若要使用這個複寫方法，請使用*schema_option*來指定自動建立預存程式，或在發行項之每個訂閱者的目的地資料庫中建立指定的預存程式。 *custom_stored_procedure*是使用者建立之預存程式的名稱。 <strong>sp_MSins_*資料表*</strong>包含目的地資料表的名稱，以取代參數的 *_table*部分。 當指定*destination_owner*時，它會在目的地資料表名稱前面加上。 例如，對於「訂閱者」端**生產**架構所擁有的**ProductCategory**資料表而言，參數會是`CALL sp_MSins_ProductionProductCategory`。 對於點對點複寫拓撲中的發行項， *_table*會附加 GUID 值。 更新訂閱者不支援指定*custom_stored_procedure* 。|  
|**SQL**或 Null|複寫 INSERT 陳述式。 提供發行項中所發行之所有資料行的值給 INSERT 陳述式。 插入時複寫這個命令：<br /><br /> `INSERT INTO <table name> VALUES (c1value, c2value, c3value, ..., cnvalue)`|  
  
 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
`[ @del_cmd = ] 'del_cmd'`這是複寫此發行項的刪除專案時，所使用的複寫命令類型。 *del_cmd*是**Nvarchar （255）**，它可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**無**|不採取任何動作。|  
|**CALLsp_MSdel_**<br /> **_table_** （預設值）<br /><br /> -或-<br /><br /> **CALL custom_stored_procedure_name**|呼叫要在訂閱者端執行的預存程序。 若要使用這個複寫方法，請使用*schema_option*來指定自動建立預存程式，或在發行項之每個訂閱者的目的地資料庫中建立指定的預存程式。 *custom_stored_procedure*是使用者建立之預存程式的名稱。 <strong>sp_MSdel_*資料表*</strong>包含目的地資料表的名稱，以取代參數的 *_table*部分。 當指定*destination_owner*時，它會在目的地資料表名稱前面加上。 例如，對於「訂閱者」端**生產**架構所擁有的**ProductCategory**資料表而言，參數會是`CALL sp_MSdel_ProductionProductCategory`。 對於點對點複寫拓撲中的發行項， *_table*會附加 GUID 值。 更新訂閱者不支援指定*custom_stored_procedure* 。|  
|**XCALL sp_MSdel_**<br /> **_目錄_**<br /><br /> -或-<br /><br /> **XCALL custom_stored_procedure_name**|以 XCALL 樣式參數來呼叫預存程序。 若要使用這個複寫方法，請使用*schema_option*來指定自動建立預存程式，或在發行項之每個訂閱者的目的地資料庫中建立指定的預存程式。 當更新訂閱者時，不允許指定使用者建立的預存程序。|  
|**SQL**或 Null|複寫 DELETE 陳述式。 提供所有主索引鍵資料行值給 DELETE 陳述式。 刪除時複寫這個命令：<br /><br /> `DELETE FROM <table name> WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
`[ @upd_cmd = ] 'upd_cmd'`這是複寫本文的更新時所使用的複寫命令類型。 *upd_cmd*是**Nvarchar （255）**，它可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**無**|不採取任何動作。|  
|**CALL sp_MSupd_**<br /> **_目錄_**<br /><br /> -或-<br /><br /> **CALL custom_stored_procedure_name**|呼叫要在訂閱者端執行的預存程序。 若要使用這個複寫方法，請使用*schema_option*來指定自動建立預存程式，或在發行項之每個訂閱者的目的地資料庫中建立指定的預存程式。|  
|**MCALL sp_MSupd_**<br /> **_目錄_**<br /><br /> -或-<br /><br /> **MCALL custom_stored_procedure_name**|以 MCALL 樣式參數來呼叫預存程序。 若要使用這個複寫方法，請使用*schema_option*來指定自動建立預存程式，或在發行項之每個訂閱者的目的地資料庫中建立指定的預存程式。 *custom_stored_procedure*是使用者建立之預存程式的名稱。 <strong>sp_MSupd_*資料表*</strong>包含目的地資料表的名稱，以取代參數的 *_table*部分。 當指定*destination_owner*時，它會在目的地資料表名稱前面加上。 例如，對於「訂閱者」端**生產**架構所擁有的**ProductCategory**資料表而言，參數會是`MCALL sp_MSupd_ProductionProductCategory`。 對於點對點複寫拓撲中的發行項， *_table*會附加 GUID 值。 當更新訂閱者時，不允許指定使用者建立的預存程序。|  
|**SCALL sp_MSupd_**<br /> **_table_** （預設值）<br /><br /> -或-<br /><br /> **SCALL custom_stored_procedure_name**|以 SCALL 樣式參數來呼叫預存程序。 若要使用這個複寫方法，請使用*schema_option*來指定自動建立預存程式，或在發行項之每個訂閱者的目的地資料庫中建立指定的預存程式。 *custom_stored_procedure*是使用者建立之預存程式的名稱。 <strong>sp_MSupd_*資料表*</strong>包含目的地資料表的名稱，以取代參數的 *_table*部分。 當指定*destination_owner*時，它會在目的地資料表名稱前面加上。 例如，對於「訂閱者」端**生產**架構所擁有的**ProductCategory**資料表而言，參數會是`SCALL sp_MSupd_ProductionProductCategory`。 對於點對點複寫拓撲中的發行項， *_table*會附加 GUID 值。 當更新訂閱者時，不允許指定使用者建立的預存程序。|  
|**XCALL sp_MSupd_**<br /> **_目錄_**<br /><br /> -或-<br /><br /> **XCALL custom_stored_procedure_name**|以 XCALL 樣式參數來呼叫預存程序。 若要使用這個複寫方法，請使用*schema_option*來指定自動建立預存程式，或在發行項之每個訂閱者的目的地資料庫中建立指定的預存程式。 當更新訂閱者時，不允許指定使用者建立的預存程序。|  
|**SQL**或 Null|複寫 UPDATE 陳述式。 在所有資料行值及主索引鍵資料行值上，提供 UPDATE 陳述式。 更新時複寫這個命令：<br /><br /> `UPDATE <table name> SET c1 = c1value, SET c2 = c2value, SET cn = cnvalue WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
> [!NOTE]  
>  CALL、MCALL、SCALL 和 XCALL 語法會隨著傳播給訂閱者的資料量而不同。 CALL 語法會傳遞所有插入和刪除資料行的值。 SCALL 語法只會傳遞受影響資料行的值。 XCALL 語法會傳遞所有資料行的值，不論是否變更過，其中包括資料行先前的值。 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
`[ @creation_script = ] 'creation_script'`這是選擇性發行項架構腳本的路徑和名稱，用來在訂閱資料庫中建立發行項。 *creation_script*是**Nvarchar （255）**，預設值是 Null。  
  
`[ @description = ] 'description'`這是發行項的描述性專案。 *description*是**Nvarchar （255）**，預設值是 Null。  
  
`[ @pre_creation_cmd = ] 'pre_creation_cmd'`如果在套用此發行項的快照集時，偵測到訂閱者端有相同名稱的現有物件，則指定系統應執行的動作。 *pre_creation_cmd*是**Nvarchar （10）**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**無**|不使用命令。|  
|**delete**|在套用快照集之前，從目的地資料表中刪除資料。 當水平篩選發行項時，只刪除篩選子句指定的資料行中之資料。 當定義水平篩選時，不支援 Oracle 發行者使用這個值。|  
|**drop** （預設值）|卸除目的地資料表。|  
|**各**|截斷目的地資料表。 對 ODBC 或 OLE DB 訂閱者無效。|  
  
`[ @filter_clause = ] 'filter_clause'`這是定義水準篩選的限制（WHERE）子句。 當輸入限制子句時，請省略 WHERE 關鍵字。 *filter_clause*是**Ntext**，預設值是 Null。 如需詳細資訊，請參閱[篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)。  
  
`[ @schema_option = ] schema_option`這是給定發行項之架構產生選項的位元遮罩。 *schema_option*是**binary （8）**，而且可以是[|（位 OR）](../../t-sql/language-elements/bitwise-or-transact-sql.md)下列其中一個或多個值的乘積：  
  
> [!NOTE]  
>  如果這個值是 NULL，系統會相依於其他發行項屬性，自動產生發行項的有效結構描述選項。 [備註] 中提供的 [**預設架構選項**] 資料表會根據發行項類型和複寫類型的組合，顯示要選擇的值。  
  
|值|描述|  
|-----------|-----------------|  
|**0x00**|停用快照集代理程式的腳本，並使用*creation_script*。|  
|**0x01**|產生物件建立指令碼 (CREATE TABLE、CREATE PROCEDURE 等)。 這個值是預存程序發行項的預設值。|  
|**0x02**|如果已定義的話，便產生傳播發行項變更的預存程序。|  
|**0x04**|識別欄位的指令碼是利用 IDENTITY 屬性來編寫的。|  
|**0x08**|複寫**時間戳記**資料行。 如果未設定，**時間戳記**資料行會複寫為**二進位**。|  
|**0x10**|產生對應的叢集索引。 即使未設定這個選項，如果已發行的資料表上已經有定義與主索引鍵和唯一條件約束有關的索引，仍會產生這些索引。|  
|**0x20**|在訂閱者端將使用者定義資料類型 (UDT) 轉換成基底資料型別。 如果 UDT 資料行是主索引鍵的一部分或計算資料行參考 UDT 資料行，則當 UDT 資料行中有 CHECK 或 DEFAULT 條件約束時，就不能使用這個選項。 *不支援 Oracle 發行者*。|  
|**0x40**|產生對應的非叢集索引。 即使未設定這個選項，如果已發行的資料表上已經有定義與主索引鍵和唯一條件約束有關的索引，仍會產生這些索引。|  
|**0x80**|複寫主索引鍵條件約束。 即使未啟用選項**0x10**和**0x40** ，也會複寫與條件約束相關的任何索引。|  
|**0x100**|複寫資料表發行項的使用者觸發程序 (如果定義的話)。 *不支援 Oracle 發行者*。|  
|**0x200**|複寫外部索引鍵條件約束。 如果參考的資料表不是發行集的一部份，便不會複寫發行資料表的所有外部索引鍵條件約束。 *不支援 Oracle 發行者*。|  
|**0x400**|複寫 CHECK 條件約束。 *不支援 Oracle 發行者*。|  
|**0x800**|複寫預設值。 *不支援 Oracle 發行者*。|  
|**0x1000**|複寫資料行層級定序。<br /><br /> **注意：** 您應該為 Oracle 發行者設定此選項，以啟用區分大小寫的比較。|  
|**0x2000**|複寫與已發行之發行項來源物件相關聯的擴充屬性。 *不支援 Oracle 發行者*。|  
|**0x4000**|複寫 UNIQUE 條件約束。 即使未啟用選項**0x10**和**0x40** ，也會複寫與條件約束相關的任何索引。|  
|**0x8000**|這個選項對於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 發行者無效。|  
|**0x10000**|將 CHECK 條件約束複寫成 NOT FOR REPLICATION，以免在同步處理期間強制執行條件約束。|  
|**0x20000**|將 FOREIGN KEY 條件約束複寫成 NOT FOR REPLICATION，以免在同步處理期間強制執行條件約束。|  
|**0x40000**|複寫資料分割資料表或索引的相關聯檔案群組。|  
|**0x80000**|複寫資料分割資料表的資料分割配置。|  
|**0x100000**|複寫資料分割索引的資料分割配置。|  
|**0x200000**|複寫資料表統計資料。|  
|**0x400000**|預設繫結|  
|**0x800000**|規則繫結|  
|**0x1000000**|全文檢索索引|  
|**0x2000000**|不會複寫系結至**xml**資料行的 xml 架構集合。|  
|**0x4000000**|複寫**xml**資料行的索引。|  
|**0x8000000**|建立訂閱者目前還沒有的任何結構描述。|  
|**0x10000000**|將**xml**資料行轉換為訂閱者上的**Ntext** 。|  
|**0x20000000**|將中[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]引進的大型物件資料類型（**Nvarchar （max）**、 **Varchar （max）** 和**Varbinary （max）**）轉換成所支援的資料類型[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。|  
|**0x40000000**|複寫權限。|  
|**0x80000000**|嘗試卸除對於不在發行集中之任何物件的相依性。|  
|**0x100000000**|如果 FILESTREAM 屬性是在**Varbinary （max）** 資料行上指定，請使用此選項來進行複寫。 如果您要將資料表複寫至 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 訂閱者，請勿指定這個選項。 不論如何設定此架構選項， [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]都不支援將含有 FILESTREAM 資料行的資料表複寫至訂閱者。<br /><br /> 請參閱相關的選項**0x800000000**。|  
|**0x200000000**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]將中引進的日期和時間資料類型（**date**、 **time**、 **datetimeoffset**和 datetime2）轉換成舊版所支援的資料類型。 **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**0x400000000**|複寫資料與索引的壓縮選項。 如需詳細資訊，請參閱 [Data Compression](../../relational-databases/data-compression/data-compression.md)。|  
|**0x800000000**|設定這個選項即可將 FILESTREAM 資料儲存在訂閱者端的檔案群組中。 如果沒有設定這個選項，FILESTREAM 資料就會儲存在預設檔案群組中。 複寫不會建立檔案群組。因此，如果您設定這個選項，就必須先建立檔案群組，然後再於訂閱者端套用快照集。 如需如何在套用快照集之前建立物件的詳細資訊，請參閱[在套用快照集之前和之後執行腳本](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)。<br /><br /> 請參閱相關的選項**0x100000000**。|  
|**0x1000000000**|將大於8000個位元組的 common language runtime （CLR）使用者定義型別（Udt）轉換成**Varbinary （max）** ，以便將 UDT 類型的資料行複寫至正在執行的訂閱[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]者。|  
|**0x2000000000**|將**hierarchyid**資料類型轉換成**Varbinary （max）** ，使**hierarchyid**類型的資料行可以複寫至正在執行的訂閱[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]者。 如需如何在複寫資料表中使用**hierarchyid**資料行的詳細資訊，請參閱[hierarchyid &#40;transact-sql&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)。|  
|**0x4000000000**|複寫資料表上任何已篩選的索引。 如需篩選索引的詳細資訊，請參閱[建立篩選的索引](../../relational-databases/indexes/create-filtered-indexes.md)。|  
|**0x8000000000**|將**geography**和**geometry**資料類型轉換成**Varbinary （max）** ，以便將這些型別的資料行複寫至正在執行的訂閱[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]者。|  
|**0x10000000000**|複寫**geography**和**geometry**類型之資料行上的索引。|  
|**0x20000000000**|複寫資料行的 SPARSE 屬性。 如需這個屬性的詳細資訊，請參閱[使用稀疏資料行](../../relational-databases/tables/use-sparse-columns.md)。|  
|**0x40000000000**|啟用「快照集代理程式」的腳本，以在「訂閱者」上建立記憶體優化資料表。|  
|**0x80000000000**|將記憶體優化文章的叢集索引轉換為非叢集索引。|  
|**0x400000000000**|複寫資料表上的任何非叢集資料行存放區索引|  
|**0x800000000000**|複寫資料表上任何服務的非叢集資料行存放區索引。|  
|NULL|複寫會自動將*schema_option*設定為預設值，其值取決於其他發行項屬性。 「備註」一節的「預設結構描述選項」資料表會顯示以發行項類型和複寫類型為基礎的預設結構描述選項。<br /><br /> 非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行集的預設值是**0x050D3**。|  
  
 並非所有的*schema_option*值都適用于每種類型的複寫和發行項類型。 [備註] 區段中的 [**有效架構選項**] 資料表會根據發行項類型和複寫類型的組合，顯示可以選擇的有效架構選項。  
  
`[ @destination_owner = ] 'destination_owner'`這是目的地物件的擁有者名稱。 *destination_owner*是**sysname**，預設值是 Null。 若未指定*destination_owner* ，則會根據下列規則自動指定擁有者：  
  
|狀況|目的地物件擁有者|  
|---------------|------------------------------|  
|發行集利用原生模式大量複製來產生初始快照集，這只支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。|預設為*source_owner*的值。|  
|從非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者發行。|預設為目的地資料庫的擁有者。|  
|發行集利用字元模式大量複製來產生初始快照集，這支援非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。|未指派。|  
  
 若要支援非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者， *DESTINATION_OWNER*必須是 Null。  
  
`[ @status = ] status`指定發行項是否為作用中，以及如何傳播變更的其他選項。 *狀態*為**Tinyint**，而且可以是[|（位 OR）](../../t-sql/language-elements/bitwise-or-transact-sql.md)一或多個這些值的乘積。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|發行項在使用中。|  
|**8**|將資料行名稱包括在 INSERT 陳述式中。|  
|**16** （預設值）|使用參數化的陳述式。|  
|**天**|將資料行名稱包括在 INSERT 陳述式中，且使用參數化陳述式。|  
|**64**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 例如，對於使用參數化陳述式的使用中發行項，這個資料行的值是 17。 值為**0**表示發行項為非使用中，且未定義任何其他屬性。  
  
`[ @source_owner = ] 'source_owner'`這是來源物件的擁有者。 *source_owner*是**sysname**，預設值是 Null。 必須為 Oracle 發行者指定*source_owner* 。  
  
`[ @sync_object_owner = ] 'sync_object_owner'`這是定義已發行之文章的視圖擁有者。 *sync_object_owner*是**sysname**，預設值是 Null。  
  
`[ @filter_owner = ] 'filter_owner'`這是篩選的擁有者。 *filter_owner*是**sysname**，預設值是 Null。  
  
`[ @source_object = ] 'source_object'`這是要發行的資料庫物件。 *source_object*是**sysname**，預設值是 Null。 如果*source_table*為 null， *source_object*不可以是 null。應該使用*source_object* ，而不是*source_table*。 如需可使用快照式或異動複寫來發行之物件類型的詳細資訊，請參閱[發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
`[ @artid = ] _article_ID_ OUTPUT`這是新文章的發行項識別碼。 *article_ID*是**int** ，預設值是 Null，它是一個 OUTPUT 參數。  
  
`[ @auto_identity_range = ] 'auto_identity_range'`在發行集建立時，啟用和停用它的自動識別範圍處理。 *auto_identity_range*是**Nvarchar （5）**，它可以是下列其中一個值：  
  
|值|描述|  
|-----------|-----------------|  
|**true**|啟用自動識別範圍處理|  
|**false**|停用自動識別範圍處理|  
|Null （預設值）|識別範圍處理是由*identityrangemanagementoption*所設定。|  
  
> [!NOTE]  
>  *auto_identity_range*已被取代，而且是為了回溯相容性而提供。 您應該使用*identityrangemanagementoption*來指定識別範圍管理選項。 如需詳細資訊，請參閱[複寫識別資料欄](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
`[ @pub_identity_range = ] pub_identity_range`如果發行項的*identityrangemanagementoption*設為**auto** ，或*auto_identity_range*設定為**true**，則控制發行者端的範圍大小。 *pub_identity_range*是**Bigint**，預設值是 Null。 *不支援 Oracle 發行者*。  
  
`[ @identity_range = ] identity_range`如果發行項的*identityrangemanagementoption*設為**auto** ，或*auto_identity_range*設定為**true**，則控制訂閱者端的範圍大小。 *identity_range*是**Bigint**，預設值是 Null。 當*auto_identity_range*設定為**true**時使用。 *不支援 Oracle 發行者*。  
  
`[ @threshold = ] threshold`這是控制散發代理程式指派新識別範圍的百分比值。 使用 [*臨界*值] 中指定的百分比時，散發代理程式會建立新的識別範圍。 *臨界*值是**Bigint**，預設值是 Null。 當*identityrangemanagementoption*設定為**auto**或*auto_identity_range*設定為**true**時使用。 *不支援 Oracle 發行者*。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`認可這個預存程式所採取的動作可能會使現有的快照集失效。 *force_invalidate_snapshot*是**bit**，預設值是0。  
  
 **0**指定加入發行項並不會使快照集無效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1**指定加入發行項可能會導致快照集無效，而且如果存在需要新快照集的訂閱，則會提供要標示為已淘汰之現有快照集的許可權，並產生新的快照集。  
  
`[ @use_default_datatypes = ] use_default_datatypes`這是指從「Oracle 發行者」發佈發行項時，是否使用預設資料行資料類型對應。 *use_default_datatypes*是 bit，預設值是1。  
  
 **1** = 使用預設發行項資料行對應。 藉由執行[sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)，即可顯示預設的資料類型對應。  
  
 **0** = 自訂發行項資料行對應已定義，因此**sp_addarticle**不會呼叫[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 。  
  
 當*use_default_datatypes*設定為**0**時，您必須針對每個從預設值變更的資料行對應執行一次[sp_changearticlecolumndatatype](../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md) 。 定義所有自訂資料行對應之後，您必須執行[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。  
  
> [!NOTE]  
>  這個參數只應用於 Oracle 發行者。 將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者的*use_default_datatypes*設定為**0**會產生錯誤。  
  
`[ @identityrangemanagementoption = ] identityrangemanagementoption`指定如何處理髮行項的識別範圍管理。 *identityrangemanagementoption*是**Nvarchar （10）**，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**無**|複寫未執行明確識別範圍管理。 建議您只將這個選項用於與舊版 SQL Server 的回溯相容性。 對等複寫不允許這個值。|  
|**手動**|利用 NOT FOR REPLICATION 來標示識別欄位，以啟用手動的識別範圍處理。|  
|**自動**|指定自動管理識別範圍。|  
|Null （預設值）|當*auto_identity_range*的值不是**true**時，預設值為**none** 。 對等拓朴預設值為**手動**（會忽略*auto_identity_range* ）。|  
  
 為了與舊版相容，當*identityrangemanagementoption*的值為 Null 時，會檢查*auto_identity_range*的值。 不過，當*identityrangemanagementoption*的值不是 Null 時，就會忽略*auto_identity_range*的值。  
  
 如需詳細資訊，請參閱[複寫識別資料欄](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
`[ @publisher = ] 'publisher'`指定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *publisher*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  將*發行*項加入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者時，不應使用「發行者」。  
  
`[ @fire_triggers_on_snapshot = ] 'fire_triggers_on_snapshot'`這是指在套用初始快照集時，是否執行複寫的使用者觸發程式。 *fire_triggers_on_snapshot*是**Nvarchar （5）**，預設值是 FALSE。 **true**表示在套用快照集時，會執行複寫資料表上的使用者觸發程式。 為了複寫觸發程式， *schema_option*的位元遮罩值必須包含值**0x100**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addarticle**用於快照式複寫或異動複寫中。  
  
 依預設，當複寫不支援資料行資料類型時，複寫不會在來源資料表中發行任何資料行。 如果您需要發行這類資料行，則必須執行[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)以加入資料行。  
  
 當您將發行項加入支援點對點異動複寫的發行集時，適用下列限制：  
  
-   所有 logbased 發行項都必須指定參數化的陳述式。 您必須在*狀態值*中包含**16** 。  
  
-   目的地資料表的名稱和擁有者必須符合來源資料表。  
  
-   發行項不能進行水平或垂直篩選。  
  
-   不支援自動識別範圍管理。 您必須為*identityrangemanagementoption*指定 manual 的值。  
  
-   如果資料表中有**timestamp**資料行，您就必須在*schema_option*中包含0x08，以將資料行複寫為**時間戳記**。  
  
-   無法指定*ins_cmd*、 *upd_cmd*和*del_cmd*的**SQL**值。  
  
 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 當您發行物件時，它們的定義會複製到訂閱者。 如果您發行相依於一或多個其他物件的資料庫物件，您就必須發行所有參考的物件。 例如，如果您發行相依於資料表的檢視表，同時也必須發行該資料表。  
  
 如果*vertical_partition*設定為**true**， **sp_addarticle**會延遲建立視圖，直到呼叫[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)為止（新增最後一個[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)之後）。  
  
 如果發行集允許更新訂閱，而已發行的資料表沒有**uniqueidentifier**資料行， **sp_addarticle**會自動將**uniqueidentifier**資料行加入資料表。  
  
 當複寫到不[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是實例的訂閱者時（異類複寫）， **INSERT**、 [!INCLUDE[tsql](../../includes/tsql-md.md)] **UPDATE**和**DELETE**命令只支援語句。  
  
 當記錄讀取器代理程式正在執行時，將發行項加入至點對點發行集可能會造成記錄讀取器代理程式和加入發行項的處理序之間發生死結。 為避免這個問題，在將發行項加入至點對點發行集之前，請使用複寫監視器停止您要加入發行項所在節點上的記錄讀取器代理程式。 加入發行項之後重新啟動記錄讀取器代理程式。  
  
 設定`@del_cmd = 'NONE'`或`@ins_cmd = 'NONE'`時，可能也會影響**update**命令的傳播，而不會在界限更新發生時傳送這些命令。 (界限更新是一種來自發行者的 UPDATE 陳述式，會做為訂閱者上的 DELETE/INSERT 配對複寫)。  
  
## <a name="default-schema-options"></a>預設結構描述選項  
 下表描述當使用者未指定*schema_options*時，複寫所設定的預設值，其中此值取決於複寫類型（顯示在頂端）和發行項類型（顯示在第一個資料行下方）。  
  
|發行項類型|複寫類型||  
|------------------|----------------------|------|  
||交易式|快照式|  
|**aggregate schema only**|**0x01**|**0x01**|  
|**func schema only**|**0x01**|**0x01**|  
|**indexed view schema only**|**0x01**|**0x01**|  
|**indexed view logbased**|**0x30F3**|**0x3071**|  
|**indexed view logbase manualboth**|**0x30F3**|**0x3071**|  
|**indexed view logbased manualfilter**|**0x30F3**|**0x3071**|  
|**indexed view logbased manualview**|**0x30F3**|**0x3071**|  
|**logbased**|**0x30F3**|**0x3071**|  
|**logbased manualfilter**|**0x30F3**|**0x3071**|  
|**logbased manualview**|**0x30F3**|**0x3071**|  
|**proc exec**|**0x01**|**0x01**|  
|**proc schema only**|**0x01**|**0x01**|  
|**serializable proc exec**|**0x01**|**0x01**|  
|**view schema only**|**0x01**|**0x01**|  
  
> [!NOTE]
>  如果發行集已啟用佇列更新，則會將*schema_option*值**0x80**加入資料表中顯示的預設值。 非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行集的預設*schema_option*是**0x050D3**。  
  
## <a name="valid-schema-options"></a>有效結構描述選項  
 下表描述以複寫類型（顯示在頂端）和發行項類型（顯示在第一個資料行下方）為依據的*schema_option*可允許的值。  
  
|發行項類型|複寫類型||  
|------------------|----------------------|------|  
||交易式|快照式|  
|**logbased**|所有選項|所有選項，但**0x02**|  
|**logbased manualfilter**|所有選項|所有選項，但**0x02**|  
|**logbased manualview**|所有選項|所有選項，但**0x02**|  
|**indexed view logbased**|所有選項|所有選項，但**0x02**|  
|**indexed view logbased manualfilter**|所有選項|所有選項，但**0x02**|  
|**indexed view logbased manualview**|所有選項|所有選項，但**0x02**|  
|**indexed view logbase manualboth**|所有選項|所有選項，但**0x02**|  
|**proc exec**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和**0x80000000**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和**0x80000000**|  
|**serializable proc exec**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和**0x80000000**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和**0x80000000**|  
|**proc schema only**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和**0x80000000**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和**0x80000000**|  
|**view schema only**|**0x01**、 **0x010**、 **0x020**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x100000**、 **0x200000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x40000000**和**0x80000000**|**0x01**、 **0x010**、 **0x020**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x100000**、 **0x200000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x40000000**和**0x80000000**|  
|**func schema only**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和**0x80000000**|**0x01**、 **0x20**、 **0x2000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x10000000**、 **0x20000000**、 **0x40000000**和**0x80000000**|  
|**indexed view schema only**|**0x01**、 **0x010**、 **0x020**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x100000**、 **0x200000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x40000000**和**0x80000000**|**0x01**、 **0x010**、 **0x020**、 **0x040**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x100000**、 **0x200000**、 **0x400000**、 **0x800000**、 **0x2000000**、 **0x8000000**、 **0x40000000**和**0x80000000**|  
  
> [!NOTE]
>  若為佇列更新發行集，則必須啟用**0x8000**和**0x80**的*schema_option*值。 非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行集支援的*schema_option*值為： **0x01**、 **0x02**、 **0x10**、 **0x40**、 **0x80**、 **0x1000**、 **0x4000**和**0x8000**。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-addarticle-transact-sql_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_addarticle**。  
  
## <a name="see-also"></a>另請參閱  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [sp_articlecolumn &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_articlefilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_articleview &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [&#40;Transact-sql&#41;的複寫預存程式](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
