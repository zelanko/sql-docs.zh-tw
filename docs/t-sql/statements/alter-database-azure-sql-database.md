---
title: "ALTER DATABASE (Azure SQL Database) |Microsoft 文件"
ms.custom: 
ms.date: 12/20/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6fc5fd95-2045-4f20-a914-3598091bc7cc
caps.latest.revision: "37"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e8d0df617bef08305166f4112fcb4f4d371137d2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="alter-database-azure-sql-database"></a>ALTER DATABASE (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  修改[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 變更資料庫的版本和服務的目標資料庫，聯結彈性集區，並設定資料庫選項的名稱。  
  
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
    | EDITION = { 'basic' | 'standard' | 'premium' | 'premiumrs' }   
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
                 | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15' | 
                 | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' | }

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
  
<delayed_durability_option> ::=    DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
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
  
 如需 set 選項的完整描述，請參閱[ALTER DATABASE SET 選項 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)和[ALTER DATABASE 相容性層級 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="arguments"></a>引數  
 *database_name*  
 這是要修改之資料庫的名稱。  
  
 CURRENT  
 指定應該改變正在使用中的目前資料庫。  
  
 MODIFY NAME  **=**  *new_database_name*  
 重新命名資料庫名稱指定為*new_database_name*。 下列範例會變更資料庫的名稱`db1`至`db2`:   

```  
ALTER DATABASE db1  
    MODIFY Name = db2 ;  
```    

 修改 (版本 **=**  ['basic' |[標準] |「 高階 」 |premiumrs'])    
 變更資料庫的服務層。 下列範例會變更版本到`premium`:
  
```  
ALTER DATABASE current 
    MODIFY (EDITION = 'premium');
``` 

如果資料庫的 MAXSIZE 屬性設定為該版本所支援的有效範圍以外的值，版本變更將會失敗。  

 修改 (MAXSIZE  **=**  [100 MB | 500 MB | 1 | 1024...4096] GB)  
 指定資料庫的大小上限。 大小上限必須符合資料庫的有效 EDITION 屬性值集合。 變更資料庫的大小上限可能也會造成資料庫版本變更。 下表列出 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服務層支援的 MAXSIZE 值與預設值 (D)：  
  
|**MAXSIZE**|**Basic**|**S0 S2**|**S3 S12**|**P1 P6 和 PRS1 PRS6**|**P11 P15**|  
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
|從 1024 GB 高達 4096 GB 增量的 256 GB *|不適用|不適用|不適用|不適用|√|√|  
  
 \*P11 和 P15 允許 MAXSIZE 4 TB 1024 gb 預設大小。  P11 和 P15 可以使用 4 TB，包括存放裝置，不另收費。 在優質層次中，大於 1 TB 的 MAXSIZE 是目前已提供下列區域： 美國 East2、 美國西部、 美國 Gov 維吉尼亞州、 西歐、 德國中央、 南東亞、 日本東部、 澳洲東部、 加拿大中央和加拿大東部。 如需目前的限制，請參閱[單一資料庫](https://docs.microsoft.com/azure/sql-database-single-database-resources)。  

  
 以下規則會套用到 MAXSIZE 和 EDITION 引數：  
  
-   MAXSIZE 值，如果指定，必須是有效的值，如上表所示。  
  
-   如果指定了 EDITION 但是未指定 MAXSIZE，就會使用版本的預設值。 例如，則 EDITION 會設定為標準，和未指定 MAXSIZE，則 MAXSIZE 會自動設為 500 MB。  
  
-   如果 MAXSIZE 和 EDITION 都不指定，則 EDITION 會設定為標準 (S0)，和 MAXSIZE 設為 250 GB。  
 

 修改 (SERVICE_OBJECTIVE =\<服務目標 >)  
 指定效能等級。 下列範例會變更服務的高階資料庫，以目標`P6`:
 
```  
ALTER DATABASE current 
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```  
 可用的服務目標的值為： `S0`， `S1`， `S2`， `S3`， `S4`， `S6`， `S7`， `S9`， `S12`， `P1`， `P2`，`P4`， `P6`， `P11`， `P15`， `PRS1`， `PRS2`， `PRS4`，和`PRS6`。 服務目標描述和大小、 版本及服務目標組合的詳細資訊，請參閱[Azure SQL Database 服務層和效能層級](http://msdn.microsoft.com/library/azure/dn741336.aspx)。 如果版本不支援指定的 SERVICE_OBJECTIVE，您會收到錯誤。 若要將 SERVICE_OBJECTIVE 值從某一層變更為另一層 (例如，從 S1 到 P1)，您還必須變更 EDITION 值。  
  
 修改 (SERVICE_OBJECTIVE = 彈性\_集區 (名稱 = \<elastic_pool_name >)  
 要將現有的資料庫加入至彈性集區中，資料庫的 SERVICE_OBJECTIVE 設 ELASTIC_POOL 並提供彈性集區的名稱。 您也可以使用這個選項的資料庫變更至同一部伺服器內不同彈性集區。 如需詳細資訊，請參閱[建立及管理 SQL Database 彈性集區](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)。 若要從彈性集區中移除資料庫，使用 ALTER DATABASE 將 service_objective，將設定為單一資料庫的效能層級。  

 新增次要 ON SERVER \<partner_server_name >  
 建立異地備援的次要資料庫具有相同名稱的夥伴伺服器上，建立主要異地複寫到本機資料庫，並開始以非同步方式將資料從主要複寫到新的次要資料庫。 如果在次要複本上已存在具有相同名稱的資料庫，則命令會失敗。 在 master 資料庫上的本機資料庫會變成主要伺服器上執行命令。  
  
 與 ALLOW_CONNECTIONS {所有 |**否**}  
 當未指定 ALLOW_CONNECTIONS 時，它會設定為否，根據預設。 如果它將所有設定，它是唯讀的資料庫，可讓所有連接的適當權限的登入。  
  
 與 SERVICE_OBJECTIVE {'S0' |'S1' |'S2' |' S3"|'S4' |'S6' |'S7' |'S9' |'S12' |'P1' |'P2' |'P4' |'P6' |'P11' |'P15' |'PRS1' |'PRS2' |'PRS4' |PRS6'}  
 當未指定 SERVICE_OBJECTIVE 時，次要資料庫會建立在與主要資料庫相同的服務層級。 當指定 SERVICE_OBJECTIVE 時，次要資料庫會建立在指定層級。 此選項支援建立具有成本較低服務層級的地理複寫的次要資料庫。 指定的 SERVICE_OBJECTIVE 必須位在相同的版本做為來源。 例如，您無法指定 S0 如果版本是 premium。  
  
 ELASTIC_POOL (名稱 = \<elastic_pool_name)  
 如果沒有指定 ELASTIC_POOL，次要資料庫不會建立彈性集區中。 當指定 ELASTIC_POOL 時，次要資料庫會建立在指定的集區中。  
  
> [!IMPORTANT]  
>  執行 [新增次要] 命令的使用者必須為主要伺服器上的 DBManager，、 具有 db_owner 的成員資格本機資料庫和 DBManager 次要伺服器上。  
  
 移除次要 ON SERVER \<partner_server_name >  
 移除指定的地理複寫的次要資料庫上指定的伺服器。 在裝載主要資料庫的伺服器上之主要資料庫上執行命令。  
  
> [!IMPORTANT]  
>  執行移除第二個命令的使用者必須是 DBManager，主要伺服器上。  
  
 FAILOVER  
 提升命令執行主要和會降級，目前的主要複本變成新的次要資料庫所在的地理複寫合作關係中之次要資料庫。 此程序的一部分，地理複寫模式暫時從非同步模式切換為同步的模式。 在容錯移轉程序：  
  
1.  主要會停止接受新的交易。  
  
2.  所有未完成的交易排清至次要資料庫。  
  
3.  次要資料庫會變成主要且開始使用舊的主要的非同步地理複寫 / 新的次要資料庫。  
  
 此順序可確保不會遺失資料就會發生。 在這兩個資料庫都無法使用的期間是 0-25 秒的順序，而角色切換。 總作業花費時間不超過約 1 分鐘。 如果在發出此命令時，主要資料庫無法使用時，命令會失敗錯誤訊息，指出主要資料庫不提供的。 如果容錯移轉程序不會完成，而且會陷入不斷出現，您可以使用強制容錯移轉命令和接受資料遺失-並如果您要復原遺失的資料，然後呼叫 devops (CSS) 來復原遺失的資料。  
  
> [!IMPORTANT]  
>  執行容錯移轉命令的使用者必須是 DBManager，主要伺服器和次要伺服器上。  
  
 FORCE_FAILOVER_ALLOW_DATA_LOSS  
 提升命令執行主要和會降級，目前的主要複本變成新的次要資料庫所在的地理複寫合作關係中之次要資料庫。 只有在目前主要複本已無法再使用時，才使用此命令。 還原可用性並重要，而且是可接受的部分資料遺失時，它被針對只，災害復原。  
  
 在強制容錯移轉：  
  
1.  指定的次要資料庫會立即變成主要資料庫，並開始接受新的交易。  
  
2.  當原始的主要複本可以與新的主要複本重新連接時，增量備份取得原始主要，而原始的主要複本會變成新的次要資料庫。  
  
3.  若要從舊的主要此增量備份復原資料，使用者就會 devops/CSS。  
  
4.  如果沒有其他次要位置，它們會自動重新設定成為新主要複本的次要資料庫。 此程序為非同步且可能會延遲完成此程序之前。 重新設定完成為止，次要複本繼續次要資料庫的舊的主要。  
  
> [!IMPORTANT]  
>  執行 FORCE_FAILOVER_ALLOW_DATA_LOSS 命令的使用者必須是 DBManager，主要伺服器和次要伺服器上。  
  
## <a name="remarks"></a>備註  
 若要移除的資料庫，請使用[DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)。  
  
 若要減少資料庫大小，請使用[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
 ALTER DATABASE 陳述式必須執行自動認可模式 (預設的交易管理模式)，且不能在明確或隱含的交易中。  
  
 清除計畫快取會導致重新編譯所有後續執行計畫，而且可能會導致查詢效能突然暫時下降。 針對每次清除計畫快取的快取存放區，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔會包含下列參考訊息：「由於某些資料庫維護或重新設定作業，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 '%s' 快取存放區 (計畫快取的一部分) 發生 %d 次快取存放區排清」。 只要在該時間間隔內快取發生排清，這個訊息就會每五分鐘記錄一次。  
  
 在下列情況下也會排清程序快取：  
  
-   資料庫將 AUTO_CLOSE 資料庫選項設定為 ON。 當沒有任何使用者連接參考或使用資料庫時，背景工作嘗試關閉並自動關閉資料庫。  
  
-   您針對有預設選項的資料庫執行幾個查詢。 然後卸除資料庫。  
  
-   您已成功重建資料庫的交易記錄。  
  
-   您還原資料庫備份。  
  
-   您卸離資料庫。  
  
## <a name="viewing-database-information"></a>檢視資料庫資訊  
 您可以利用目錄檢視、系統函數和系統預存程序，以傳回資料庫、檔案和檔案群組的相關資訊。  
  
## <a name="permissions"></a>Permissions  
 只有伺服器層級主體登入 (由佈建程序所建立) 或 `dbmanager` 資料庫角色成員可以改變資料庫。  
  
> [!IMPORTANT]  
>  資料庫的擁有者不能改變資料庫，除非他們是 `dbmanager` 角色的成員。  
  
## <a name="examples"></a>範例  
  
### <a name="a-check-the-edition-options-and-change-them"></a>A. 檢查版本選項，以及變更：

```
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>B. 將資料庫移至不同的彈性集區  
 將現有的資料庫移至名為 pool1 集區：  
  
```  
ALTER DATABASE db1   
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;  
```  
  
### <a name="c-add-a-geo-replication-secondary"></a>C. 新增異地備援的次要資料庫  
 伺服器上建立非可讀取次要資料庫 db1 `secondaryserver` db1 中，本機伺服器上。  
  
```  
ALTER DATABASE db1   
ADD SECONDARY ON SERVER secondaryserver   
WITH ( ALLOW_CONNECTIONS = NO )  
```  
  
### <a name="d-remove-a-geo-replication-secondary"></a>D. 移除地理複寫的次要資料庫  
 移除伺服器上的次要資料庫 db1 `secondaryserver`。  
  
```  
ALTER DATABASE db1   
REMOVE SECONDARY ON SERVER testsecondaryserver   
```  
  
### <a name="e-failover-to-a-geo-replication-secondary"></a>E. 容錯移轉至次要地理複寫  
 升級伺服器上的次要資料庫 db1`secondaryserver`成為新主要資料庫在伺服器上執行`secondaryserver`。  
  
```  
ALTER DATABASE db1 FAILOVER  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立資料庫 &#40;Azure SQL Database &#41;](../../t-sql/statements/create-database-azure-sql-database.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.data_spaces &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.filegroups &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [系統資料庫](../../relational-databases/databases/system-databases.md)  
  
  
