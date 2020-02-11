---
title: sys.databases sp_cdc_enable_table （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_enable_table_TSQL
- sp_cdc_enable_table_TSQL
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], enabling tables
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
ms.assetid: 26150c09-2dca-46ad-bb01-3cb3165bcc5d
author: rothja
ms.author: jroth
ms.openlocfilehash: b846ff31d4acbc9d87f66a76a19f688384c88982
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106465"
---
# <a name="syssp_cdc_enable_table-transact-sql"></a>sys.sp_cdc_enable_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對目前資料庫中指定的來源資料表，啟用異動資料擷取。 當某個資料表啟用異動資料擷取時，系統就會將套用至此資料表之每個資料操作語言 (DML) 作業的記錄寫入交易記錄中。 異動資料擷取處理序會從記錄中擷取這項資訊，並將它寫入使用一組函數所存取的變更資料表中。  
  
 並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中都無法異動資料擷取。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_cdc_enable_table   
  [ @source_schema = ] 'source_schema',   
  [ @source_name = ] 'source_name' ,  [,[ @capture_instance = ] 'capture_instance' ]  
  [,[ @supports_net_changes = ] supports_net_changes ]  
  , [ @role_name = ] 'role_name'  
  [,[ @index_name = ] 'index_name' ]  
  [,[ @captured_column_list = ] 'captured_column_list' ]  
  [,[ @filegroup_name = ] 'filegroup_name' ]  
  [,[ @allow_partition_switch = ] 'allow_partition_switch' ]  
  [;]  
```  
  
## <a name="arguments"></a>引數  
`[ @source_schema = ] 'source_schema'`這是來源資料表所屬的架構名稱。 *source_schema*是**sysname**，沒有預設值，而且不能是 Null。  
  
`[ @source_name = ] 'source_name'`這是要啟用變更資料捕獲的來源資料表名稱。 *source_name*是**sysname**，沒有預設值，而且不能是 Null。  
  
 *source_name*必須存在於目前的資料庫中。 **Cdc**架構中的資料表無法啟用變更資料捕獲。  
  
`[ @role_name = ] 'role_name'`這是用來閘道存取變更資料的資料庫角色名稱。 *role_name*是**sysname** ，必須指定。 如果明確設定為 NULL，就不會使用任何控制角色來限制變更資料的存取權。  
  
 如果角色目前存在，就會使用此角色。 如果角色不存在，系統就會嘗試使用指定的名稱來建立資料庫角色。 嘗試建立角色之前，會先針對角色名稱修剪字串右邊的空白字元。 如果呼叫端未經授權，無法在資料庫中建立角色，預存程序作業就會失敗。  
  
`[ @capture_instance = ] 'capture_instance'`這是用來命名實例特定變更資料 capture 物件的 capture 實例名稱。 *capture_instance*是**sysname** ，不能是 Null。  
  
 如果未指定，名稱會衍生自來源架構名稱加上來源資料表名稱，格式為*schemaname_sourcename*。 *capture_instance*不能超過100個字元，而且在資料庫內必須是唯一的。 不論是指定或衍生， *capture_instance*都會修剪字串右邊的任何空白字元。  
  
 一個來源資料表最多可以有兩個擷取執行個體。 如需詳細資訊，請參閱[sp_cdc_help_change_data_capture &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)。  
  
`[ @supports_net_changes = ] supports_net_changes`指出是否要針對此 capture 實例啟用查詢淨變更的支援。 如果資料表**** 有主鍵，或資料表具有使用@index_name參數識別的唯一索引， *supports_net_changes*是 bit，預設值是1。 否則，此參數的預設值是 0。  
  
 如果為 0，就只會產生查詢所有變更的支援函數。  
  
 如果為 1，也會產生查詢淨變更所需的函數。  
  
 如果*supports_net_changes*設定為1，就必須指定*index_name* ，否則來源資料表必須有已定義的主鍵。  
  
`[ @index_name = ] 'index_name_'`唯一索引的名稱，用來唯一識別來源資料表中的資料列。 *index_name*是**sysname** ，而且可以是 Null。 如果指定的話， *index_name*在來源資料表上必須是有效的唯一索引。 如果指定了*index_name* ，識別的索引資料行會優先于任何定義的主鍵資料行，做為資料表的唯一資料列識別碼。  
  
`[ @captured_column_list = ] 'captured_column_list'`識別要包含在變更資料表中的來源資料表資料行。 *captured_column_list*是**Nvarchar （max）** ，而且可以是 Null。 如果是 NULL，則所有資料行都會包含在變更資料表中。  
  
 資料行名稱必須是來源資料表中的有效資料行。 在主鍵索引中定義的資料行，或是必須包含*index_name*所參考之索引中所定義的資料行。  
  
 *captured_column_list*是資料行名稱的逗號分隔清單。 清單內的個別資料行名稱可以選擇性地使用雙引號 ("") 或方括號 ([]) 括住。 如果資料行名稱包含內嵌逗號，資料行名稱就必須括住。  
  
 *captured_column_list*不能包含下列保留的資料行名稱： **__ $ start_lsn**、 **__ $ end_lsn**、 **__ $ seqval**、 **__ $ operation**和 **__ $ update_mask**。  
  
`[ @filegroup_name = ] 'filegroup_name'`這是針對 capture 實例所建立之變更資料表所使用的檔案群組。 *filegroup_name*是**sysname** ，而且可以是 Null。 若已指定，則必須為目前的資料庫定義*filegroup_name* 。 如果是 NULL，就會使用預設的檔案群組。  
  
 我們建議您針對異動資料擷取的變更資料表建立個別的檔案群組。  
  
`[ @allow_partition_switch = ] 'allow_partition_switch'`指出是否可以針對已啟用變更資料捕獲的資料表執行 ALTER TABLE 的 SWITCH PARTITION 命令。 *allow_partition_switch*是**bit**，預設值是1。  
  
 若為非資料分割資料表，此切換設定一律為 1，而且會忽略實際的設定。 如果非資料分割資料表的切換明確設定為 0，就會發出警告 22857，表示已經忽略此切換設定。 如果資料分割資料表的切換設定明確設定為 0，就會發出警告 22356，表示不允許在來源資料表上進行資料分割切換作業。 最後，如果切換設定明確設定為 1 或允許預設為 1，而且啟用的資料表已進行資料分割，就會發出警告 22855，表示不會封鎖資料分割切換。 如果進行了任何資料分割切換，異動資料擷取將不會追蹤切換所造成的變更。 這會導致取用變更資料時，發生資料不一致的情況。  
  
> [!IMPORTANT]  
>  雖然 SWITCH PARTITION 是中繼資料作業，但是它會導致資料變更。 異動資料擷取變更資料表不會擷取與這項作業相關聯的資料變更。 假設有一份具有三個資料分割的資料表，然後對這份資料表進行變更。 擷取程序將會追蹤針對此資料表執行的使用者插入、更新和刪除作業。 不過，如果某個資料分割切換移出至另一份資料表 (例如，執行大量刪除)，在這項作業中移動的資料列將不會擷取成變更資料表中的已刪除資料列。 同樣地，如果具有預先擴展資料列的新資料分割加入至此資料表，這些資料列將不會反映在變更資料表中。 當這些變更由應用程式取用而且套用至目的地時，這可能會導致資料不一致。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 針對異動資料擷取啟用資料表之前，必須先啟用資料庫。 若要判斷資料庫是否已啟用變更資料捕獲，請查詢[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視中的**is_cdc_enabled**資料行。 若要啟用資料庫，請使用[sys.databases sp_cdc_enable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md)預存程式。  
  
 當資料表已啟用異動資料擷取時，就會產生一份變更資料表以及一個或兩個查詢函數。 變更資料表會當做擷取處理序從交易記錄中擷取之來源資料表變更的儲存機制。 查詢函數是用來從變更資料表中擷取資料。 這些函式的名稱是從*capture_instance*參數衍生而來，方法如下：  
  
-   所有變更函數： **cdc. fn_cdc_get_all_changes_<capture_instance>**  
  
-   Net changes 函數： **cdc. fn_cdc_get_net_changes_<capture_instance>**  
  
 如果來源資料表是資料庫中要啟用變更資料捕獲的第一個資料表，而且資料庫不存在任何交易式發行集，則**sp_cdc_enable_table**也會建立資料庫的 capture 和清除作業。 它會將 sys.databases 目錄檢視中的 [ **is_tracked_by_cdc** []](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)資料行設定為1。  
  
> [!NOTE]  
>  當資料表已啟用異動資料擷取時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 不需要處於執行中狀態。 不過，除非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 正在執行，否則擷取處理序將不會處理交易記錄並將項目寫入變更資料表中。  
  
## <a name="permissions"></a>權限  
 需要**db_owner**固定資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-enabling-change-data-capture-by-specifying-only-required-parameters"></a>A. 只指定需要的參數來啟用異動資料擷取  
 下列範例會啟用 `HumanResources.Employee` 資料表的異動資料擷取。 只會指定需要的參數。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Employee'  
  , @role_name = N'cdc_Admin';  
GO  
```  
  
### <a name="b-enabling-change-data-capture-by-specifying-additional-optional-parameters"></a>B. 指定其他選擇性參數，藉以啟用異動資料擷取  
 下列範例會啟用 `HumanResources.Department` 資料表的異動資料擷取。 指定了 `@allow_partition_switch` 以外的所有參數。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Department'  
  , @role_name = N'cdc_admin'  
  , @capture_instance = N'HR_Department'   
  , @supports_net_changes = 1  
  , @index_name = N'AK_Department_Name'   
  , @captured_column_list = N'DepartmentID, Name, GroupName'   
  , @filegroup_name = N'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_cdc_disable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)   
 [sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [cdc. fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [cdc. fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [sp_cdc_help_jobs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)  
  
  
