---
title: sp_addarticle & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addarticle
- sp_addarticle_TSQL
helpviewer_keywords:
- sp_addarticle
ms.assetid: 0483a157-e403-4fdb-b943-23c1b487bef0
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ae9bb433018d5a329fda378c1f8aa13e171b5742
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830368"
---
# <a name="spaddarticle-transact-sql"></a>sp_addarticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@publication =** ] **'***publication***'**  
 這是發行項所在的發行集名稱。 這個名稱在資料庫內必須是唯一的。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@article =** ] **'***文章***'**  
 這是發行項的名稱。 這個名稱在發行集內必須是唯一的。 *發行項*已**sysname**，沒有預設值。  
  
 [  **@source_table =** ] **'***t***'**  
 這個參數已被取代;使用  *source_object*改。  
  
 *不支援 Oracle 發行者的這個參數。*  
  
 [  **@destination_table =** ] **'***destination_table***'**  
 是目的地 （訂閱） 資料表的名稱，如果不同於*t*或預存程序。 *destination_table*已**sysname**，預設值是 NULL，這表示*t*等於*destination_table * *。*  
  
 [  **@vertical_partition =** ] **'***vertical_partition***'**  
 在資料表發行項上，啟用和停用資料行的篩選。 *vertical_partition*已**nchar(5)**，預設值是 FALSE。  
  
 **false**表示沒有垂直篩選，並將發佈的所有資料行。  
  
 **true**清除所有其他宣告的主索引鍵資料行、 沒有預設值，可為 null 的資料行和唯一索引鍵資料行。 使用加入資料行[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)。  
  
 [ **@type =** ] **'***type***'**  
 這是發行項的類型。 *型別*已**sysname**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**彙總結構描述**|只含結構描述的彙總函式。|  
|**僅限 func 結構描述**|只含結構描述的函數。|  
|**索引檢視表 logbased**|記錄式索引檢視發行項。 不支援 Oracle 發行者使用這個值。 這種類型的發行項不需要個別發行基底資料表。|  
|**索引檢視表 logbased manualboth**|記錄式且含有手動篩選和手動檢視的索引檢視發行項。 這個選項需要您同時指定*sync_object*並*篩選*參數。 這種類型的發行項不需要個別發行基底資料表。 不支援 Oracle 發行者使用這個值。|  
|**索引檢視表 logbased manualfilter**|記錄式且含有手動篩選準則的索引檢視發行項。 這個選項需要您同時指定*sync_object*並*篩選*參數。 這種類型的發行項不需要個別發行基底資料表。 不支援 Oracle 發行者使用這個值。|  
|**索引檢視表 logbased manualview**|含有手動檢視的記錄式索引檢視發行項。 此選項會要求您指定*sync_object*參數。 這種類型的發行項不需要個別發行基底資料表。 不支援 Oracle 發行者使用這個值。|  
|**僅限索引檢視表結構描述**|只含結構描述的索引檢視。 這種類型的發行項也必須發行基底資料表。|  
|**logbased** （預設值）|記錄式發行項。|  
|**logbased manualboth**|記錄式且含有手動篩選準則和手動檢視的發行項。 這個選項需要您同時指定*sync_object*並*篩選*參數。 不支援 Oracle 發行者使用這個值。|  
|**logbased manualfilter**|記錄式且含有手動篩選準則的發行項。 這個選項需要您同時指定*sync_object*並*篩選*參數。 不支援 Oracle 發行者使用這個值。|  
|**logbased manualview**|含有手動檢視的記錄式發行項。 此選項會要求您指定*sync_object*參數。 不支援 Oracle 發行者使用這個值。|  
|**proc exec**|將執行預存程序複寫到發行項的所有訂閱者。 不支援 Oracle 發行者使用這個值。 我們建議您使用選項**serializable proc exec**而不是**proc exec**。 如需詳細資訊，請參閱一節 」 類型的預存程序執行發行項 」 中[發行預存程序執行異動複寫中](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。 異動資料擷取啟用時無法使用。|  
|**僅限程序結構描述**|只含結構描述的程序。 不支援 Oracle 發行者使用這個值。|  
|**serializable proc exec**|只在預存程序是執行於可序列化交易的環境之內時，才複寫執行預存程序。 不支援 Oracle 發行者使用這個值。<br /><br /> 也必須從複寫的程序執行的明確交易內執行的程序。|  
|**僅限檢視結構描述**|只含結構描述的檢視。 不支援 Oracle 發行者使用這個值。 使用此選項時，您也必須發行基底資料表。|  
  
 [  **@filter =** ] **'***篩選***'**  
 這是用來水平篩選資料表的預存程序 (使用 FOR REPLICATION 建立)。 *篩選條件*已**nvarchar(386)**，預設值是 NULL。 [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)並[sp_articlefilter](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)必須以手動方式執行，以建立檢視和篩選預存程序。 如果不是 NULL，便不會建立篩選程序 (假設預存程序是手動建立)。  
  
 [  **@sync_object =** ] **'***sync_object***'**  
 這是用於產生資料檔案，以代表這個發行項之快照集的資料表或檢視表名稱。 *sync_object*已**nvarchar(386)**，預設值是 NULL。 如果是 NULL， [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)呼叫來自動建立用來產生輸出檔案的檢視。 這在之後加入含有的任何資料行，就會發生[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)。 如果不是 NULL，便不會建立檢視 (假設檢視是手動建立)。  
  
 [  **@ins_cmd =** ] **'***ins_cmd***'**  
 當針對此發行項複寫插入時，這是所使用的複寫命令類型。 *ins_cmd*已**nvarchar(255)**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**NONE**|不採取任何動作。|  
|**CALL sp_MSins_**<br /> ***資料表***（預設值）<br /><br /> -或-<br /><br /> **呼叫 custom_stored_procedure_name**|呼叫要在訂閱者端執行的預存程序。 若要使用這個複寫方法，使用*schema_option*來指定自動建立預存程序，或每個訂閱者的發行項在目的地資料庫中建立指定的預存程序。 *custom_stored_procedure*是使用者建立的預存程序的名稱。 **sp_MSins_ * 資料表*** 包含名稱的目的地資料表的位置 *（_t)* 參數的一部分。 當*destination_owner*指定時，它會附加至目的地資料表的名稱。 例如，對於**ProductCategory**資料表屬於**生產**參數會是 「 訂閱者 」 端的結構描述， `CALL sp_MSins_ProductionProductCategory`。 在對等複寫拓撲中，發行項 *（_t)* 會附加 GUID 值。 指定*custom_stored_procedure*不支援更新訂閱者。|  
|**SQL**或 NULL|複寫 INSERT 陳述式。 提供發行項中所發行之所有資料行的值給 INSERT 陳述式。 插入時複寫這個命令：<br /><br /> `INSERT INTO <table name> VALUES (c1value, c2value, c3value, ..., cnvalue)`|  
  
 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
 [  **@del_cmd =**] **'***del_cmd***'**  
 當針對此發行項複寫刪除時，這是所使用的複寫命令類型。 *del_cmd*已**nvarchar(255)**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**NONE**|不採取任何動作。|  
|**CALLsp_MSdel_**<br /> ***資料表***（預設值）<br /><br /> -或-<br /><br /> **呼叫 custom_stored_procedure_name**|呼叫要在訂閱者端執行的預存程序。 若要使用這個複寫方法，使用*schema_option*來指定自動建立預存程序，或每個訂閱者的發行項在目的地資料庫中建立指定的預存程序。 *custom_stored_procedure*是使用者建立的預存程序的名稱。 **sp_MSdel_ * 資料表*** 包含名稱的目的地資料表的位置 *（_t)* 參數的一部分。 當*destination_owner*指定時，它會附加至目的地資料表的名稱。 例如，對於**ProductCategory**資料表屬於**生產**參數會是 「 訂閱者 」 端的結構描述， `CALL sp_MSdel_ProductionProductCategory`。 在對等複寫拓撲中，發行項 *（_t)* 會附加 GUID 值。 指定*custom_stored_procedure*不支援更新訂閱者。|  
|**XCALL sp_MSdel_**<br /> ***table***<br /><br /> -或-<br /><br /> **XCALL custom_stored_procedure_name**|以 XCALL 樣式參數來呼叫預存程序。 若要使用這個複寫方法，使用*schema_option*來指定自動建立預存程序，或每個訂閱者的發行項在目的地資料庫中建立指定的預存程序。 當更新訂閱者時，不允許指定使用者建立的預存程序。|  
|**SQL**或 NULL|複寫 DELETE 陳述式。 提供所有主索引鍵資料行值給 DELETE 陳述式。 刪除時複寫這個命令：<br /><br /> `DELETE FROM <table name> WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
 [  **@upd_cmd =**] **'***upd_cmd***'**  
 當針對此發行項複寫更新時，這是所使用的複寫命令類型。 *upd_cmd*已**nvarchar(255)**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**NONE**|不採取任何動作。|  
|**CALL sp_MSupd_**<br /> ***table***<br /><br /> -或-<br /><br /> **呼叫 custom_stored_procedure_name**|呼叫要在訂閱者端執行的預存程序。 若要使用這個複寫方法，使用*schema_option*來指定自動建立預存程序，或每個訂閱者的發行項在目的地資料庫中建立指定的預存程序。|  
|**MCALL sp_MSupd_**<br /> ***table***<br /><br /> -或-<br /><br /> **MCALL custom_stored_procedure_name**|以 MCALL 樣式參數來呼叫預存程序。 若要使用這個複寫方法，使用*schema_option*來指定自動建立預存程序，或每個訂閱者的發行項在目的地資料庫中建立指定的預存程序。 *custom_stored_procedure*是使用者建立的預存程序的名稱。 **sp_MSupd_ * 資料表*** 包含名稱的目的地資料表的位置 *（_t)* 參數的一部分。 當*destination_owner*指定時，它會附加至目的地資料表的名稱。 例如，對於**ProductCategory**資料表屬於**生產**參數會是 「 訂閱者 」 端的結構描述， `MCALL sp_MSupd_ProductionProductCategory`。 在對等複寫拓撲中，發行項 *（_t)* 會附加 GUID 值。 當更新訂閱者時，不允許指定使用者建立的預存程序。|  
|**SCALL sp_MSupd_**<br /> ***資料表***（預設值）<br /><br /> -或-<br /><br /> **SCALL custom_stored_procedure_name**|以 SCALL 樣式參數來呼叫預存程序。 若要使用這個複寫方法，使用*schema_option*來指定自動建立預存程序，或每個訂閱者的發行項在目的地資料庫中建立指定的預存程序。 *custom_stored_procedure*是使用者建立的預存程序的名稱。 **sp_MSupd_ * 資料表*** 包含名稱的目的地資料表的位置 *（_t)* 參數的一部分。 當*destination_owner*指定時，它會附加至目的地資料表的名稱。 例如，對於**ProductCategory**資料表屬於**生產**參數會是 「 訂閱者 」 端的結構描述， `SCALL sp_MSupd_ProductionProductCategory`。 在對等複寫拓撲中，發行項 *（_t)* 會附加 GUID 值。 當更新訂閱者時，不允許指定使用者建立的預存程序。|  
|**XCALL sp_MSupd_**<br /> ***table***<br /><br /> -或-<br /><br /> **XCALL custom_stored_procedure_name**|以 XCALL 樣式參數來呼叫預存程序。 若要使用這個複寫方法，使用*schema_option*來指定自動建立預存程序，或每個訂閱者的發行項在目的地資料庫中建立指定的預存程序。 當更新訂閱者時，不允許指定使用者建立的預存程序。|  
|**SQL**或 NULL|複寫 UPDATE 陳述式。 在所有資料行值及主索引鍵資料行值上，提供 UPDATE 陳述式。 更新時複寫這個命令：<br /><br /> `UPDATE <table name> SET c1 = c1value, SET c2 = c2value, SET cn = cnvalue WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
> [!NOTE]  
>  CALL、MCALL、SCALL 和 XCALL 語法會隨著傳播給訂閱者的資料量而不同。 CALL 語法會傳遞所有插入和刪除資料行的值。 SCALL 語法只會傳遞受影響資料行的值。 XCALL 語法會傳遞所有資料行的值，不論是否變更過，其中包括資料行先前的值。 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
 [  **@creation_script =**] **'***creation_script***'**  
 在訂閱資料庫中，這是用來建立發行項的選擇性發行項結構描述指令碼的路徑和名稱。 *creation_script*已**nvarchar(255)**，預設值是 NULL。  
  
 [  **@description =**] **'***描述***'**  
 這是發行項的描述項目。 *描述*已**nvarchar(255)**，預設值是 NULL。  
  
 [  **@pre_creation_cmd =**] **'***pre_creation_cmd***'**  
 指定系統應該做什麼套用這個發行項的快照集時偵測到 「 訂閱者 」 具有相同名稱的現有物件時。 *pre_creation_cmd*已**nvarchar(10**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**None**|不使用命令。|  
|**delete**|在套用快照集之前，從目的地資料表中刪除資料。 當水平篩選發行項時，只刪除篩選子句指定的資料行中之資料。 當定義水平篩選時，不支援 Oracle 發行者使用這個值。|  
|**卸除**（預設值）|卸除目的地資料表。|  
|**truncate**|截斷目的地資料表。 對 ODBC 或 OLE DB 訂閱者無效。|  
  
 [  **@filter_clause=**] **'***filter_clause***'**  
 這是定義水平篩選的限制 (WHERE) 子句。 當輸入限制子句時，請省略 WHERE 關鍵字。 *filter_clause*已**ntext**，預設值是 NULL。 如需詳細資訊，請參閱[篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)。  
  
 [  **@schema_option =**] *schema_option*  
 這是給定發行項之結構描述產生選項的位元遮罩。 *schema_option*已**binary(8**，而且可以是[|(位元 OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md)產品的一或多個這些值：  
  
> [!NOTE]  
>  如果這個值是 NULL，系統會相依於其他發行項屬性，自動產生發行項的有效結構描述選項。 **預設結構描述選項**「 備註 」 中的資料表會顯示值，將會選擇根據發行項類型和複寫類型的組合。  
  
|值|描述|  
|-----------|-----------------|  
|**0x00**|停用快照集代理程式指令碼，並使用*creation_script*。|  
|**0x01**|產生物件建立指令碼 (CREATE TABLE、CREATE PROCEDURE 等)。 這個值是預存程序發行項的預設值。|  
|**0x02**|如果已定義的話，便產生傳播發行項變更的預存程序。|  
|**0x04**|識別欄位的指令碼是利用 IDENTITY 屬性來編寫的。|  
|**0x08**|複寫**時間戳記**資料行。 如果未設定，請**時間戳記**資料行會複寫為**二進位**。|  
|**0x10**|產生對應的叢集索引。 即使未設定這個選項，如果已發行的資料表上已經有定義與主索引鍵和唯一條件約束有關的索引，仍會產生這些索引。|  
|**0x20**|在訂閱者端將使用者定義資料類型 (UDT) 轉換成基底資料型別。 如果 UDT 資料行是主索引鍵的一部分或計算資料行參考 UDT 資料行，則當 UDT 資料行中有 CHECK 或 DEFAULT 條件約束時，就不能使用這個選項。 *不支援 Oracle 發行者*。|  
|**0x40**|產生對應的非叢集索引。 即使未設定這個選項，如果已發行的資料表上已經有定義與主索引鍵和唯一條件約束有關的索引，仍會產生這些索引。|  
|**0x80**|複寫主索引鍵條件約束。 此外，也會複寫任何與條件約束的索引，即使選項**0x10**並**0x40**未啟用。|  
|**0x100**|複寫資料表發行項的使用者觸發程序 (如果定義的話)。 *不支援 Oracle 發行者*。|  
|**0x200**|複寫外部索引鍵條件約束。 如果參考的資料表不是發行集的一部份，便不會複寫發行資料表的所有外部索引鍵條件約束。 *不支援 Oracle 發行者*。|  
|**0x400**|複寫 CHECK 條件約束。 *不支援 Oracle 發行者*。|  
|**0x800**|複寫預設值。 *不支援 Oracle 發行者*。|  
|**0x1000**|複寫資料行層級定序。<br /><br /> **注意：** 應該設定此選項，來啟用區分大小寫的比較的 Oracle 發行者。|  
|**0x2000**|複寫與已發行之發行項來源物件相關聯的擴充屬性。 *不支援 Oracle 發行者*。|  
|**0x4000**|複寫 UNIQUE 條件約束。 此外，也會複寫任何與條件約束的索引，即使選項**0x10**並**0x40**未啟用。|  
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
|**0x2000000**|XML 結構描述集合繫結至**xml**不會複寫資料行。|  
|**0x4000000**|在複寫索引**xml**資料行。|  
|**0x8000000**|建立訂閱者目前還沒有的任何結構描述。|  
|**0x10000000**|將轉換**xml**資料行**ntext**訂閱者上。|  
|**0x20000000**|將大型物件資料類型 (**nvarchar （max)**， **varchar （max)**，並**varbinary （max)**) 中導入[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]到支援的資料類型[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
|**0x40000000**|複寫權限。|  
|**0x80000000**|嘗試卸除對於不在發行集中之任何物件的相依性。|  
|**0x100000000**|使用此選項來複寫 FILESTREAM 屬性，如果同時指定**varbinary （max)** 資料行。 如果您要將資料表複寫至 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 訂閱者，請勿指定這個選項。 將具有 FILESTREAM 資料行的資料表複寫[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]不支援訂閱者，不論這個結構描述選項的設定方式。<br /><br /> 請參閱相關的選項**0x800000000**。|  
|**0x200000000**|將日期和時間資料類型轉換 (**日期**，**時間**， **datetimeoffset**，以及**datetime2**) 中導入[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]資料型別所支援的舊版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**0x400000000**|複寫資料與索引的壓縮選項。 如需詳細資訊，請參閱 [Data Compression](../../relational-databases/data-compression/data-compression.md)。|  
|**0x800000000**|設定這個選項即可將 FILESTREAM 資料儲存在訂閱者端的檔案群組中。 如果沒有設定這個選項，FILESTREAM 資料就會儲存在預設檔案群組中。 複寫不會建立檔案群組。因此，如果您設定這個選項，就必須先建立檔案群組，然後再於訂閱者端套用快照集。 如需如何建立物件，然後再套用快照集的詳細資訊，請參閱[前後執行指令碼之後套用快照集](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)。<br /><br /> 請參閱相關的選項**0x100000000**。|  
|**0x1000000000**|將 common language runtime (CLR) 使用者定義類型 (Udt) 大於 8000 位元組**varbinary （max)** 如此 UDT 類型的資料行可以複寫至訂閱者執行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。|  
|**0x2000000000**|將轉換**hierarchyid**資料類型**varbinary （max)** 以便類型的資料行**hierarchyid**可以複寫到訂閱者執行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 如需有關如何使用**hierarchyid**資料行在複寫資料表中，請參閱[hierarchyid &#40;-&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)。|  
|**0x4000000000**|複寫資料表上任何已篩選的索引。 如需有關篩選索引的詳細資訊，請參閱[建立篩選的索引](../../relational-databases/indexes/create-filtered-indexes.md)。|  
|**0x8000000000**|將轉換**地理**並**幾何**資料類型**varbinary （max)** 使這些類型的資料行可以複寫到訂閱者執行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000000000**|複寫類型的資料行的索引**地理**並**geometry**。|  
|**0x20000000000**|複寫資料行的 SPARSE 屬性。 如需有關這個屬性的詳細資訊，請參閱 <<c0> [ 使用疏鬆資料行](../../relational-databases/tables/use-sparse-columns.md)。|  
|**0x40000000000**|啟用快照集代理程式，「 訂閱者 」 上建立記憶體最佳化資料表的指令碼。|  
|**0x80000000000**|轉換成記憶體最佳化的發行項的叢集索引的叢集的索引。|  
|**0x400000000000**|複寫資料表上的任何非叢集資料行存放區索引|  
|**0x800000000000**|複寫資料表上任何 flitered 的非叢集資料行存放區索引。|  
|NULL|複寫會自動將*schema_option*預設值，其值取決於其他發行項屬性。 「備註」一節的「預設結構描述選項」資料表會顯示以發行項類型和複寫類型為基礎的預設結構描述選項。<br /><br /> 預設值為非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行集是**0x050D3**。|  
  
 並非所有*schema_option*值對於每個複寫類型和發行項類型都有效。 **有效的結構描述選項**< 備註 > 一節的表格會顯示有效的結構描述選項可以選擇根據發行項類型和複寫類型的組合。  
  
 [  **@destination_owner =**] **'***destination_owner***'**  
 這是目的地物件的擁有者名稱。 *destination_owner*已**sysname**，預設值是 NULL。 當*destination_owner*未指定，會自動根據下列規則來指定擁有者：  
  
|條件|目的地物件擁有者|  
|---------------|------------------------------|  
|發行集利用原生模式大量複製來產生初始快照集，這只支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。|預設值為*source_owner*。|  
|從非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者發行。|預設為目的地資料庫的擁有者。|  
|發行集利用字元模式大量複製來產生初始快照集，這支援非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。|未指派。|  
  
 若要支援非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者*destination_owner*必須是 NULL。  
  
 [  **@status=**]*狀態*  
 指定發行項是否在使用中，以及如何傳播變更的其他選項。 *狀態*已**tinyint**，而且可以是[|(位元 OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md)產品的一或多個這些值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|發行項在使用中。|  
|**8**|將資料行名稱包括在 INSERT 陳述式中。|  
|**16** （預設值）|使用參數化的陳述式。|  
|**24**|將資料行名稱包括在 INSERT 陳述式中，且使用參數化陳述式。|  
|**64**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 例如，對於使用參數化陳述式的使用中發行項，這個資料行的值是 17。 值為**0**表示發行項處於非使用中，而且沒有其他的屬性所定義。  
  
 [  **@source_owner =**] **'***source_owner***'**  
 這是來源物件的擁有者。 *source_owner*已**sysname**，預設值是 NULL。 *source_owner*必須指定 Oracle 發行者。  
  
 [  **@sync_object_owner =**] **'***sync_object_owner***'**  
 這是定義已發行的發行項之檢視表的擁有者名稱。 *sync_object_owner*已**sysname**，預設值是 NULL。  
  
 [  **@filter_owner =**] **'***filter_owner***'**  
 這是篩選的擁有者。 *filter_owner*已**sysname**，預設值是 NULL。  
  
 [  **@source_object =**] **'***source_object***'**  
 這是要發佈的資料庫物件。 *source_object*已**sysname**，預設值是 NULL。 如果*t*為 NULL，就*source_object*不能是 NULL。*source_object*應使用而不是*t*。 如需可以使用快照式或異動複寫發行之物件的類型的詳細資訊，請參閱[發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
 [  **@artid =** ] *article_ID* **輸出**  
 這是新發行項的發行項識別碼。 *article_ID*已**int**預設值是 NULL，它是一個 OUTPUT 參數。  
  
 [  **@auto_identity_range =** ] **'***auto_identity_range***'**  
 在發行集建立之時，啟用和停用發行集的自動識別範圍處理。 *auto_identity_range*已**nvarchar(5)**，而且可以是下列值之一：  
  
|值|描述|  
|-----------|-----------------|  
|**true**|啟用自動識別範圍處理|  
|**false**|停用自動識別範圍處理|  
|NULL(default)|識別範圍處理由設定*identityrangemanagementoption*。|  
  
> [!NOTE]  
>  *auto_identity_range*已被取代，而且為了回溯相容性才提供。 您應該使用*identityrangemanagementoption*指定識別範圍管理選項。 如需詳細資訊，請參閱[複寫識別資料欄](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
 [  **@pub_identity_range =** ] *pub_identity_range*  
 控制在發行者端的範圍大小，如果發行項*identityrangemanagementoption*設為**自動**或是*auto_identity_range*設為 **，則為 true**. *pub_identity_range*已**bigint**，預設值是 NULL。 *不支援 Oracle 發行者*。  
  
 [  **@identity_range =** ] *identity_range*  
 如果發行項會控制在訂閱者範圍大小*identityrangemanagementoption*設為**自動**或是*auto_identity_range*設為 **，則為 true**. *identity_range*已**bigint**，預設值是 NULL。 使用的時機*auto_identity_range*設為 **，則為 true**。 *不支援 Oracle 發行者*。  
  
 [  **@threshold =** ]*臨界值*  
 這是一個百分比值，用於控制散發代理程式指派新識別範圍的時機。 當指定的百分比值*閾值*是使用，「 散發代理程式會建立新的識別範圍。 *閾值*已**bigint**，預設值是 NULL。 使用的時機*identityrangemanagementoption*設為**自動**或*auto_identity_range*設定為 **，則為 true**。 *不支援 Oracle 發行者*。  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 認可這個預存程序所採取的動作可能使現有的快照集失效。 *force_invalidate_snapshot*已**元**，預設值是 0。  
  
 **0**指定加入發行項並不會導致快照集失效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  
 **1**指定加入發行項可能使快照集失效，而且如果訂閱已存在，需要新的快照集，會提供要標示為已棄用之現有快照集並產生新的快照集的權限。  
  
 [  **@use_default_datatypes =** ] *use_default_datatypes*  
 這是指從 Oracle 發行者發行發行項時，是否使用預設資料行資料類型對應。 *use_default_datatypes* bit，預設值是 1。  
  
 **1** = 會使用對應的預設文件資料行。 會顯示預設資料類型對應，請執行[sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)。  
  
 **0** = 自訂發行項的資料行定義的對應，因此[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)不由呼叫**sp_addarticle**。  
  
 當*use_default_datatypes*設為**0**，您必須執行[sp_changearticlecolumndatatype](../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md)變更預設值從每個資料行對應的一次。 定義所有的自訂資料行對應之後，您必須執行[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。  
  
> [!NOTE]  
>  這個參數只應用於 Oracle 發行者。 設定*use_default_datatypes*要**0**如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者會產生錯誤。  
  
 [  **@identityrangemanagementoption =** ] *identityrangemanagementoption*  
 指定如何處理發行項的識別範圍管理。 *identityrangemanagementoption*已**nvarchar(10**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**None**|複寫未執行明確識別範圍管理。 建議您只將這個選項用於與舊版 SQL Server 的回溯相容性。 對等複寫不允許這個值。|  
|**手動**|利用 NOT FOR REPLICATION 來標示識別欄位，以啟用手動的識別範圍處理。|  
|**自動**|指定自動管理識別範圍。|  
|NULL(default)|預設值為**無**時的值*auto_identity_range*不**true**。 預設值為**手動**在預設的對等項目-拓樸 (*auto_identity_range*會被忽略)。|  
  
 回溯相容性，當的值*identityrangemanagementoption*是 NULL，值*auto_identity_range*已核取。 不過，當 windows 7 *identityrangemanagementoption*不是 NULL，則值*auto_identity_range*會被忽略。  
  
 如需詳細資訊，請參閱[複寫識別資料欄](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
 [  **@publisher =** ] **'***發行者***'**  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應加入至發行項時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
 [  **@fire_triggers_on_snapshot =** ] **'***fire_triggers_on_snapshot***'**  
 這是指在套用初始快照集時，是否執行複寫的使用者觸發程序。 *fire_triggers_on_snapshot*已**nvarchar(5)**，預設值是 FALSE。 **true**表示在套用快照集時，就會執行複寫的資料表上的使用者觸發程序。 為了讓觸發程序，受到要複寫的位元遮罩值*schema_option*必須包含值**0x100**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addarticle**用於快照式複寫或異動複寫中。  
  
 依預設，當複寫不支援資料行資料類型時，複寫不會在來源資料表中發行任何資料行。 如果您需要發行這類資料行，您必須執行[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)中加入資料行。  
  
 當您將發行項加入支援點對點異動複寫的發行集時，適用下列限制：  
  
-   所有 logbased 發行項都必須指定參數化的陳述式。 您必須包含**16**中*狀態*值。  
  
-   目的地資料表的名稱和擁有者必須符合來源資料表。  
  
-   發行項不能進行水平或垂直篩選。  
  
-   不支援自動識別範圍管理。 您必須指定值為 manual *identityrangemanagementoption*。  
  
-   如果**時間戳記**資料行存在於資料表中，您必須包含在 0x08 *schema_option*複寫資料行做為**時間戳記**。  
  
-   值為**SQL**不能指定*ins_cmd*， *upd_cmd*，以及*del_cmd*。  
  
 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 當您發行物件時，它們的定義會複製到訂閱者。 如果您發行相依於一或多個其他物件的資料庫物件，您就必須發行所有參考的物件。 例如，如果您發行相依於資料表的檢視表，同時也必須發行該資料表。  
  
 如果*vertical_partition*設為 **，則為 true**， **sp_addarticle**會延遲建立檢視，直到[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) （之後會呼叫上次[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)加入)。  
  
 如果發行集允許更新訂閱，且已發行的資料表沒有**uniqueidentifier**資料行**sp_addarticle**加入**uniqueidentifier**資料行資料表自動。  
  
 複寫到訂閱者不是執行個體時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（異質性複寫），僅[!INCLUDE[tsql](../../includes/tsql-md.md)]支援陳述式**插入**， **UPDATE**，以及**刪除**命令。  
  
 當記錄讀取器代理程式正在執行時，將發行項加入至點對點發行集可能會造成記錄讀取器代理程式和加入發行項的處理序之間發生死結。 為避免這個問題，在將發行項加入至點對點發行集之前，請使用複寫監視器停止您要加入發行項所在節點上的記錄讀取器代理程式。 加入發行項之後重新啟動記錄讀取器代理程式。  
  
 設定時`@del_cmd = 'NONE'`或是`@ins_cmd = 'NONE'`，散佈**更新**命令可能也會受到界限的更新發生時，未傳送這些命令。 (界限更新是一種來自發行者的 UPDATE 陳述式，會做為訂閱者上的 DELETE/INSERT 配對複寫)。  
  
## <a name="default-schema-options"></a>預設結構描述選項  
 下表描述如果複寫所設定的預設值*schema_options*不由使用者，其中此值取決於複寫類型 （顯示在頂端） 和發行項類型 （顯示在第一個資料行之下） 指定。  
  
|發行項類型|複寫類型||  
|------------------|----------------------|------|  
||異動|快照式|  
|**彙總結構描述**|**0x01**|**0x01**|  
|**僅限 func 結構描述**|**0x01**|**0x01**|  
|**僅限索引檢視表結構描述**|**0x01**|**0x01**|  
|**索引檢視表 logbased**|**0x30F3**|**0x3071**|  
|**索引檢視表對數底數 manualboth**|**0x30F3**|**0x3071**|  
|**索引檢視表 logbased manualfilter**|**0x30F3**|**0x3071**|  
|**索引檢視表 logbased manualview**|**0x30F3**|**0x3071**|  
|**logbased**|**0x30F3**|**0x3071**|  
|**logbased manualfilter**|**0x30F3**|**0x3071**|  
|**logbased manualview**|**0x30F3**|**0x3071**|  
|**proc exec**|**0x01**|**0x01**|  
|**僅限程序結構描述**|**0x01**|**0x01**|  
|**serializable proc exec**|**0x01**|**0x01**|  
|**僅限檢視結構描述**|**0x01**|**0x01**|  
  
> [!NOTE]  
>  如果發行集已啟用佇列更新， *schema_option*的值**0x80**加入至資料表中顯示的預設值。 預設值*schema_option*是非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行集**0x050D3**。  
  
## <a name="valid-schema-options"></a>有效結構描述選項  
 下表描述允許的值*schema_option* （顯示在頂端） 的複寫類型和發行項類型 （顯示在第一個資料行之下） 為基礎。  
  
|發行項類型|複寫類型||  
|------------------|----------------------|------|  
||異動|快照式|  
|**logbased**|所有選項|所有選項，但**0x02**|  
|**logbased manualfilter**|所有選項|所有選項，但**0x02**|  
|**logbased manualview**|所有選項|所有選項，但**0x02**|  
|**索引檢視表 logbased**|所有選項|所有選項，但**0x02**|  
|**索引檢視表 logbased manualfilter**|所有選項|所有選項，但**0x02**|  
|**索引檢視表 logbased manualview**|所有選項|所有選項，但**0x02**|  
|**索引檢視表對數底數 manualboth**|所有選項|所有選項，但**0x02**|  
|**proc exec**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|  
|**serializable proc exec**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|  
|**僅限程序結構描述**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|  
|**僅限檢視結構描述**|**0x01**， **0x010**， **0x020**， **0x040**， **0x0100**， **0x2000**， **0x40000**， **0x100000**， **0x200000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x010**， **0x020**， **0x040**， **0x0100**， **0x2000**， **0x40000**， **0x100000**， **0x200000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x40000000**，和**0x80000000**|  
|**僅限 func 結構描述**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|  
|**僅限索引檢視表結構描述**|**0x01**， **0x010**， **0x020**， **0x040**， **0x0100**， **0x2000**， **0x40000**， **0x100000**， **0x200000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x010**， **0x020**， **0x040**， **0x0100**， **0x2000**， **0x40000**， **0x100000**， **0x200000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x40000000**，和**0x80000000**|  
  
> [!NOTE]  
>  佇列更新的發行集*schema_option*的值**0x8000**並**0x80**必須啟用。 支援*schema_option*的值非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行集： **0x01**， **0x02**， **0x10**， **0x40**， **0x80**， **0x1000**， **0x4000**並**0X8000**。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-addarticle-transact-sql_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addarticle**。  
  
## <a name="see-also"></a>另請參閱  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_articleview &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
