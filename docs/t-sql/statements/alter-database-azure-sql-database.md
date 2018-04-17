---
title: ALTER DATABASE (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6fc5fd95-2045-4f20-a914-3598091bc7cc
caps.latest.revision: 37
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ddec688efe7ce468b7af1c05389b9cc1e86cf4c4
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/05/2018
---
# <a name="alter-database-azure-sql-database"></a>ALTER DATABASE (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  修改 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 變更資料庫的名稱、資料庫的版本和服務目標、聯結彈性集區，以及設定資料庫選項。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Azure SQL Database Syntax  
ALTER DATABASE { database_name }  
{  
    MODIFY NAME = new_database_name  
  | MODIFY ( <edition_options> [, ... n] ) 
  | SET { <option_spec> [ ,... n ] } 
  | ADD SECONDARY ON SERVER <partner_server_name>  
    [WITH ( <add-secondary-option>::= [, ... n] ) ]  
  | REMOVE SECONDARY ON SERVER <partner_server_name>  
  | FAILOVER  
  | FORCE_FAILOVER_ALLOW_DATA_LOSS  
}  
[;] 

<edition_options> ::= 
{  

  MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 … 1024 … 4096 GB }  
  | EDITION = { 'basic' | 'standard' | 'premium' | 'GeneralPurpose' | 'BusinessCritical'} 
  | SERVICE_OBJECTIVE = 
       {  <service-objective>
       | { ELASTIC_POOL (name = <elastic_pool_name>) } 
       } 
}  

<add-secondary-option> ::=  
   {  
      ALLOW_CONNECTIONS = { ALL | NO }  
     | SERVICE_OBJECTIVE = 
       {  <service-objective> 
       | { ELASTIC_POOL ( name = <elastic_pool_name>) } 
       } 
   }  

<service-objective> ::=  { 'S0' | 'S1' | 'S2' | 'S3'| 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |
       | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'
      | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_4' | 'GP_GEN4_8' | 'GP_GEN4_16' 
      | 'BC_GEN4_1' | 'BC_GEN4_2' | 'BC_GEN4_4' | 'BC_GEN4_8' | 'BC_GEN4_16' | 
      }

```  
  
```
-- SET OPTIONS AVAILABLE FOR SQL Database  
-- Full descriptions of the set options are available in the topic 
-- ALTER DATABASE SET Options. The supported syntax is listed here.  

<option_spec> ::= 
{  
    <auto_option> 
  | <change_tracking_option> 
  | <cursor_option> 
  | <db_encryption_option>  
  | <db_update_option> 
  | <db_user_access_option> 
  | <delayed_durability_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <snapshot_option>  
  | <sql_option> 
  | <target_recovery_time_option> 
  | <termination>  
  | <temporal_history_retention>  
}  
  
<auto_option> ::= 
{  
    AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] } 
  | AUTO_SHRINK { ON | OFF } 
  | AUTO_UPDATE_STATISTICS { ON | OFF } 
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
}  

<change_tracking_option> ::=  
{  
  CHANGE_TRACKING 
   { 
       = OFF  
     | = ON [ ( <change_tracking_option_list > [,...n] ) ] 
     | ( <change_tracking_option_list> [,...n] )  
   }  
}  

   <change_tracking_option_list> ::=  
   {  
       AUTO_CLEANUP = { ON | OFF } 
     | CHANGE_RETENTION = retention_period { DAYS | HOURS | MINUTES }  
   }  

<cursor_option> ::= 
{  
    CURSOR_CLOSE_ON_COMMIT { ON | OFF } 
}  
  
<db_encryption_option> ::=  
  ENCRYPTION { ON | OFF }  
  
<db_update_option> ::=  
  { READ_ONLY | READ_WRITE }  
  
<db_user_access_option> ::=  
  { RESTRICTED_USER | MULTI_USER }  
  
<delayed_durability_option> ::=  DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
<parameterization_option> ::=  
  PARAMETERIZATION { SIMPLE | FORCED }  
  
<query_store_options> ::=  
{  
  QUERY_STORE 
  {  
    = OFF 
    | = ON [ ( <query_store_option_list> [,... n] ) ]  
    | ( < query_store_option_list> [,... n] )  
    | CLEAR [ ALL ]  
  }  
} 
  
<query_store_option_list> ::=  
{  
  OPERATION_MODE = { READ_WRITE | READ_ONLY } 
  | CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = number )  
  | DATA_FLUSH_INTERVAL_SECONDS = number 
  | MAX_STORAGE_SIZE_MB = number 
  | INTERVAL_LENGTH_MINUTES = number 
  | SIZE_BASED_CLEANUP_MODE = [ AUTO | OFF ]  
  | QUERY_CAPTURE_MODE = [ ALL | AUTO | NONE ]  
  | MAX_PLANS_PER_QUERY = number  
}  
  
<snapshot_option> ::=  
{  
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
  | READ_COMMITTED_SNAPSHOT {ON | OFF }  
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT {ON | OFF }  
}  
<sql_option> ::= 
{  
    ANSI_NULL_DEFAULT { ON | OFF }   
  | ANSI_NULLS { ON | OFF }   
  | ANSI_PADDING { ON | OFF }   
  | ANSI_WARNINGS { ON | OFF }   
  | ARITHABORT { ON | OFF }   
  | COMPATIBILITY_LEVEL = { 100 | 110 | 120 | 130 | 140 }  
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }   
  | NUMERIC_ROUNDABORT { ON | OFF }   
  | QUOTED_IDENTIFIER { ON | OFF }   
  | RECURSIVE_TRIGGERS { ON | OFF }   
}  
  
<termination>  ::=   
{  
    ROLLBACK AFTER integer [ SECONDS ]   
  | ROLLBACK IMMEDIATE   
  | NO_WAIT  
}  

<temporal_history_retention>  ::=  TEMPORAL_HISTORY_RETENTION { ON | OFF }
```  
  
 如需有關 set 選項的完整描述，請參閱 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) 和 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
## <a name="arguments"></a>引數  

*database_name*  

這是要修改之資料庫的名稱。  
  
CURRENT  

指定應該改變正在使用中的目前資料庫。  
  
MODIFY NAME **=***new_database_name*  

使用指定為 *new_database_name* 的名稱來重新命名資料庫。 下列範例會將資料庫 `db1` 的名稱變更為 `db2`：   

```  
ALTER DATABASE db1  
    MODIFY Name = db2 ;  
```    

MODIFY (EDITION **=** ['basic' | 'standard' | 'premium' |'GeneralPurpose' | 'BusinessCritical'])    

變更資料庫的服務層。 已移除 'premiumrs' 的支援。 如有疑問，請使用此電子郵件別名： premium-rs@microsoft.com。

下列範例會將版本變更為 `premium`：
  
```  
ALTER DATABASE current 
    MODIFY (EDITION = 'premium');
``` 

如果為資料庫 MAXSIZE 屬性設定的值超出該版本所支援的有效範圍，EDITION 變更就會失敗。  

MODIFY (MAXSIZE **=** [100 MB | 500 MB | 1 | 1024…4096] GB)  

指定資料庫的大小上限。 大小上限必須符合資料庫的有效 EDITION 屬性值集合。 變更資料庫的大小上限可能也會造成資料庫版本變更。 下表列出 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服務層支援的 MAXSIZE 值與預設值 (D)：  
  
**以 DTU 為基礎的模型**

|**MAXSIZE**|**基本**|**S0-S2**|**S3-S12**|**P1-P6**|**P11-P15**|  
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|  
|100 MB|√|√|√|√|√|  
|250 MB|√|√|√|√|√|  
|500 MB|√|√|√|√|√|  
|1 GB|√|√|√|√|√|  
|2 GB|√ (D)|√|√|√|√|  
|5 GB|不適用|√|√|√|√|  
|10 GB|不適用|√|√|√|√|  
|20 GB|不適用|√|√|√|√|  
|30 GB|不適用|√|√|√|√|  
|40 GB|不適用|√|√|√|√|  
|50 GB|不適用|√|√|√|√|  
|100 GB|不適用|√|√|√|√|  
|150 GB|不適用|√|√|√|√|  
|200 GB|不適用|√|√|√|√|  
|250 GB|不適用|√ (D)|√ (D)|√|√|  
|300 GB|不適用|√|√|√|√|  
|400 GB|不適用|√|√|√|√|  
|500 GB|不適用|√|√|√ (D)|√|  
|750 GB|不適用|√|√|√|√|  
|1024 GB|不適用|√|√|√|√ (D)|  
|從 1024 GB 至最大 4096 GB (以每 256 GB 的大小遞增)*|不適用|不適用|不適用|不適用|√|√|  
  
\* P11 和 P15 允許 MAXSIZE 最大至 4 TB，並以 1024 GB 作為預設大小。  P11 和 P15 最多可使用 4 TB 的隨附儲存體，且不另收費。 在進階層中，大於 1 TB 的 MAXSIZE 目前已提供下列區域使用：美國東部2、美國西部、美國維吉尼亞州政府、西歐、德國中部、東南亞、日本東部、澳洲東部、加拿大中部和加拿大東部。 針對以 DTU 為基礎的模型，如需資源限制的額外詳細資訊，請參閱[以 DTU 為基礎的資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) \(英文\)。  

對於以 DTU 為基礎的模型，若指定了 MAXSIZE 值，則此值必須為上表中所示適用於所指定服務層的有效值。
 
**以 vCore 為基礎的模型**

**一般用途的服務層**

|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_4|GP_Gen4_8|GP_Gen4_16|
|:--- | --: |--: |--: |--: |--: |
|資料大小上限 (GB)|1024|1024|1536|3072|4096|

**業務關鍵服務層**

|效能等級|BC_Gen4_1|BC_Gen4_2|BC_Gen4_4|BC_Gen4_8|BC_Gen4_16|
|:--- | --: |--: |--: |--: |--: |
|資料大小上限 (GB)|1024|1024|1536|2048|2048|

當使用 vCore 模型時，如果未設定 `MAXSIZE` 值，預設值為 32 GB。 針對以 vCore 為基礎的模型，如需資源限制的額外詳細資訊，請參閱[以 vCore 為基礎的資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) \(英文\)。
  
以下規則會套用到 MAXSIZE 和 EDITION 引數：  
  
- 如果指定了 EDITION 但是未指定 MAXSIZE，就會使用版本的預設值。 例如，如果將 EDITION 設定為 Standard，而未指定 MAXSIZE，則 MAXSIZE 會自動設定為 500 MB。  
  
- 如果 MAXSIZE 和 EDITION 皆未指定，則 EDITION 會設定為 Standard (S0) 而 MAXSIZE 則設定為 250 GB。  

MODIFY (SERVICE_OBJECTIVE = \<service-objective>)  

指定效能等級。 下列範例會將進階資料庫的服務目標變更為 `P6`：
 
```sql  
ALTER DATABASE current 
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```  

指定效能等級。 服務目標的可用值為：`S0`、`S1`、`S2`、`S3`、`S4`、`S6`、`S7`、`S9`、`S12`、`P1`、`P2`、`P4`、`P6`、`P11`、`P15`、`GP_GEN4_1`、`GP_GEN4_2`、`GP_GEN4_4`、`GP_GEN4_8`、`GP_GEN4_16`、`BC_GEN4_1` `BC_GEN4_2` `BC_GEN4_4` `BC_GEN4_8` `BC_GEN4_16`。 

如需服務目標描述和大小、版本及服務目標組合的詳細資訊，請參閱 [Azure SQL Database 服務層和效能層級](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)、[以 DTU 為基礎的資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) \(英文\) 和[以 vCore 為基礎的資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) \(英文\)。 目前已移除對 PRS 服務目標的支援。 如有疑問，請使用此電子郵件別名： premium-rs@microsoft.com。 
  
MODIFY (SERVICE_OBJECTIVE = ELASTIC\_POOL (name = \<elastic_pool_name>)  

若要將現有的資料庫新增至彈性集區，請將資料庫的 SERVICE_OBJECTIVE 設定為 ELASTIC_POOL，並提供彈性集區的名稱。 您也可以使用此選項將資料庫變更至相同伺服器內的不同彈性集區。 如需詳細資訊，請參閱[建立和管理 SQL Database 彈性資料庫集區](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)。 若要從彈性集區中移除資料庫，請使用 ALTER DATABASE 將 SERVICE_OBJECTIVE 設定為單一資料庫效能等級。  

ADD SECONDARY ON SERVER \<partner_server_name>  

在夥伴伺服器上使用相同名稱來建立異地複寫次要資料庫，其中將本機資料庫設定為異地複寫主要資料庫，然後開始以非同步方式將資料從主要端複寫到新的次要端。 如果次要端上已經有相同名稱的資料庫，命令就會失敗。 此命令會在伺服器的 master 資料庫上執行，該伺服器裝載了成為主要資料庫的本機資料庫。  
  
WITH ALLOW_CONNECTIONS { **ALL** | NO }  

未指定 ALLOW_CONNECTIONS 時，預設會設定為 ALL。 如果設定為 ALL，就是允許所有具備適當權限的登入進行連線的唯讀資料庫。  
  
WITH SERVICE_OBJECTIVE {  `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_4`, `GP_GEN4_8`, `GP_GEN4_16`, `BC_GEN4_1` `BC_GEN4_2` `BC_GEN4_4` `BC_GEN4_8` `BC_GEN4_16` }  

未指定 SERVICE_OBJECTIVE 時，會在與主要資料庫相同的服務層級建立次要資料庫。 已指定 SERVICE_OBJECTIVE 時，則會在指定的層級建立次要資料庫。 此選項支援以成本較低廉的服務層級建立異地複寫次要端。 所指定的 SERVICE_OBJECTIVE 必須是在與來源相同的版本內。 例如，如果版本為 Premium，您便無法指定 S0。  
  
ELASTIC_POOL (name = \<elastic_pool_name)  

未指定 ELASTIC_POOL 時，不會在彈性集區中建立次要資料庫。 已指定 ELASTIC_POOL 時，則會在指定的集區中建立次要資料庫。  
  
> [!IMPORTANT]  
>  執行 ADD SECONDARY 命令的使用者必須是主要伺服器上的 DBManager、具備本機資料庫中的 db_owner 成員資格，並且是次要伺服器上的 DBManager。  
  
REMOVE SECONDARY ON SERVER  \<partner_server_name>  

移除所指定伺服器上指定的異地複寫次要資料庫。 此命令會在裝載主要資料庫之伺服器的 master 資料庫上執行。  
  
> [!IMPORTANT]  
>  執行 REMOVE SECONDARY 命令的使用者必須是主要伺服器上的 DBManager。  
  
FAILOVER  

將異地複寫合作關係中用來執行命令的次要資料庫升階成主要端，而將目前的主要端降級成新的次要端。 在此程序中，異地複寫模式會從非同步模式暫時切換至同步模式。 在容錯移轉程序期間：  
  
1.  主要端會停止接受新的交易。  
  
2.  所有未完成的交易都會排清至次要端。  
  
3.  次要端會變成主要端，然後開始與舊的主要端/新的次要端進行非同步異地複寫。  
  
這個順序可確保不會發生任何資料遺失。 兩個資料庫都無法使用的期間大約是 0-25 秒，即切換角色時。 整個作業應該花費不超過一分鐘的時間。 如果在發出此命令時，無法使用主要資料庫，命令就會失敗，並顯示指出無法使用主要資料庫的錯誤訊息。 如果容錯移轉程序未完成並出現停滯現象，您可以使用強制容錯移轉命令並接受資料遺失，然後，如果您需要復原遺失的資料，便呼叫 devops (CSS) 來復原遺失的資料。  
  
> [!IMPORTANT]  
>  執行 FAILOVER 命令的使用者必須同時是主要伺服器和次要伺服器上的 DBManager。  
  
FORCE_FAILOVER_ALLOW_DATA_LOSS  

將異地複寫合作關係中用來執行命令的次要資料庫升階成主要端，而將目前的主要端降級成新的次要端。 請只在目前主要端不再可供使用的情況下，才使用此命令。 這是僅針對在必須緊急復原可用性而可接受遺失部分資料的災害復原情況而設計。  
  
在強制容錯移轉期間：  
  
1. 指定的次要資料庫會立即變成主要資料庫，並開始接受新的交易。  
  
2. 當原始主要端可以與新的主要端重新連線時，就會在原始主要端上進行增量備份，然後原始主要端會變成新的次要端。  
  
3. 若要從舊主要端上的這個增量備份復原資料，使用者必須進行 devops/CSS。  
  
4. 如果有額外的次要端，這些次要端將會自動重新成新主要端的次要端。 此程序會以非同步方式進行，因此可能會有延遲，直到此程序完成為止。 在重新設定完成之前，次要端仍繼續是舊主要端的次要端。  
  
> [!IMPORTANT]  
>  執行 FORCE_FAILOVER_ALLOW_DATA_LOSS 命令的使用者必須同時是主要伺服器和次要伺服器上的 DBManager。  
  
## <a name="remarks"></a>Remarks  

若要移除資料庫，請使用 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)。  
若要縮小資料庫大小，請使用 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
ALTER DATABASE 陳述式必須執行自動認可模式 (預設的交易管理模式)，且不能在明確或隱含的交易中。  
  
清除計畫快取會導致重新編譯所有後續執行計畫，而且可能會導致查詢效能突然暫時下降。 針對每次清除計畫快取的快取存放區，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔會包含下列參考訊息：「由於某些資料庫維護或重新設定作業，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 '%s' 快取存放區 (計畫快取的一部分) 發生 %d 次快取存放區排清」。 只要在該時間間隔內快取發生排清，這個訊息就會每五分鐘記錄一次。  
  
在下列情況下也會排清程序快取：  
  
- 資料庫將 AUTO_CLOSE 資料庫選項設定為 ON。 當沒有任何使用者連接參考或使用資料庫時，背景工作嘗試關閉並自動關閉資料庫。  
  
- 您針對有預設選項的資料庫執行幾個查詢。 然後卸除資料庫。  
  
- 您已成功重建資料庫的交易記錄。  
  
- 您還原資料庫備份。  
  
- 您卸離資料庫。  
  
## <a name="viewing-database-information"></a>檢視資料庫資訊  

您可以利用目錄檢視、系統函數和系統預存程序，以傳回資料庫、檔案和檔案群組的相關資訊。  
  
## <a name="permissions"></a>Permissions  

只有伺服器層級主體登入 (由佈建程序所建立) 或 `dbmanager` 資料庫角色成員可以改變資料庫。  
  
> [!IMPORTANT]  
>  資料庫的擁有者不能改變資料庫，除非他們是 `dbmanager` 角色的成員。  
  
## <a name="examples"></a>範例  
  
### <a name="a-check-the-edition-options-and-change-them"></a>A. 檢查版本選項並變更這些選項：

```sql
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>B. 將資料庫移至不同的彈性集區  

將現有的資料庫移至名為 pool1 的集區：  
  
```sql  
ALTER DATABASE db1   
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;  
```  
  
### <a name="c-add-a-geo-replication-secondary"></a>C. 新增異地複寫次要端  

在本機伺服器之 db1 的伺服器 `secondaryserver` 上建立可讀取的次要資料庫 db1。  
  
```sql  
ALTER DATABASE db1   
ADD SECONDARY ON SERVER secondaryserver   
WITH ( ALLOW_CONNECTIONS = ALL )  
```  
  
### <a name="d-remove-a-geo-replication-secondary"></a>D. 移除異地複寫次要端  
 
移除伺服器 `secondaryserver`上的次要資料庫 db1。  
  
```sql  
ALTER DATABASE db1   
REMOVE SECONDARY ON SERVER testsecondaryserver   
```  
  
### <a name="e-failover-to-a-geo-replication-secondary"></a>E. 容錯移轉至異地複寫次要端  

當在伺服器 `secondaryserver` 上執行時，會將伺服器 `secondaryserver` 上的次要資料庫 db1 升階成新的主要資料庫。  
  
```sql  
ALTER DATABASE db1 FAILOVER  
```  
  
## <a name="see-also"></a>另請參閱
  
[CREATE DATABASE - Azure SQL Database](../../t-sql/statements/create-database-azure-sql-database.md)   
 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [系統資料庫](../../relational-databases/databases/system-databases.md)  
  
  
