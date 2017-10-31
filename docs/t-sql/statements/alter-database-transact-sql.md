---
title: "ALTER DATABASE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_TSQL
- ALTER DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- databases [SQL Server], modifying
- ALTER DATABASE statement
- databases [SQL Server], renaming
- renaming databases
- database modifications [SQL Server]
- ALTER DATABASE statement, syntax described
- database names [SQL Server], ALTER DATABASE
- modifying databases
- collations [SQL Server], modifying
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 15f8affd-8f39-4021-b092-0379fc6983da
caps.latest.revision: 282
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 6c498acedd2821127137ec6be1bd2e04e6b3da09
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="alter-database-transact-sql"></a>ALTER DATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改資料庫或與資料庫相關聯的檔案和檔案群組。 在資料庫中新增或移除檔案和檔案群組、變更資料庫或其檔案和檔案群組的屬性、變更資料庫定序，以及設定資料庫選項。 無法修改資料庫快照集。 若要修改與複寫相關聯的資料庫選項，請使用[sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)。  
   
 由於長度的關係，ALTER DATABASE 語法會分成下列主題：  
  
 ALTER DATABASE  
 目前的主題會提供變更資料庫名稱和定序的語法。  
  
 [ALTER DATABASE 檔案及檔案群組選項](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
 提供在資料庫中新增和移除檔案及檔案群組的語法，以及變更檔案及檔案群組之屬性的語法。  
  
 [ALTER DATABASE SET 選項](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
 提供使用 ALTER DATABASE 的 SET 選項來變更資料庫屬性的語法。  
  
 [ALTER DATABASE 資料庫鏡像](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)  
 提供與資料庫鏡像相關之 ALTER DATABASE SET 選項的語法。  
  
 [ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)  
 提供的語法[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]Always On 可用性群組的次要複本上設定次要資料庫的 ALTER DATABASE 選項。  
  
 [ALTER DATABASE 相容性層級](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
 提供與資料庫相容性層級相關之 ALTER DATABASE SET 選項的語法。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
Azure SQL Database，請參閱[ALTER DATABASE &#40;Azure SQL Database &#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
Azure SQL 資料倉儲，請參閱[ALTER DATABASE &#40;Azure SQL 資料倉儲 &#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).  
平行處理資料倉儲，請參閱[ALTER DATABASE &#40;平行資料倉儲 &#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).
  
## <a name="syntax"></a>語法  
  
```  
-- SQL Server Syntax  
ALTER DATABASE { database_name  | CURRENT }  
{  
    MODIFY NAME = new_database_name   
  | COLLATE collation_name  
  | <file_and_filegroup_options>  
  | <set_database_options>  
}  
[;]  
  
<file_and_filegroup_options >::=  
  <add_or_modify_files>::=  
  <filespec>::=   
  <add_or_modify_filegroups>::=  
  <filegroup_updatability_option>::=  
  
<set_database_options>::=  
  <optionspec>::=   
  <auto_option> ::=   
  <change_tracking_option> ::=  
  <cursor_option> ::=   
  <database_mirroring_option> ::=   
  <date_correlation_optimization_option> ::=  
  <db_encryption_option> ::=  
  <db_state_option> ::=  
  <db_update_option> ::=  
  <db_user_access_option> ::=  <delayed_durability_option> ::=  <external_access_option> ::=  
  <FILESTREAM_options> ::=  
  <HADR_options> ::=    
  <parameterization_option> ::=  
  <query_store_options> ::=  
  <recovery_option> ::=   
  <service_broker_option> ::=  
  <snapshot_option> ::=  
  <sql_option> ::=   
  <termination> ::=  
  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 這是要修改之資料庫的名稱。  
  
> [!NOTE]  
>  自主資料庫無法使用這個選項。  
  
 CURRENT  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定應該改變正在使用中的目前資料庫。  
  
 MODIFY NAME  **=**  *new_database_name*  
 重新命名資料庫名稱指定為*new_database_name*。  
  
 COLLATE *sys.databases*  
 指定資料庫的定序。 *sys.databases*可以是 Windows 定序名稱或 SQL 定序名稱。 若未指定，就會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的定序指派給資料庫。  
  
 使用預設定序除外的方式建立資料庫時，資料庫中的資料一律會接受指定的定序。 如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，建立自主的資料庫時，內部維護的目錄資訊是使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]預設定序， **Latin1_General_100_CI_AS_WS_KS_SC**。  
  
 如需有關 Windows 和 SQL 定序名稱的詳細資訊，請參閱[COLLATE &#40;TRANSACT-SQL &#41;](~/t-sql/statements/collations.md).  
  
 **\<delayed_durability_option >:: =**  
 **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 如需詳細資訊，請參閱[ALTER DATABASE SET 選項 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)和[控制交易持久性](../../relational-databases/logs/control-transaction-durability.md)。  
  
 **\<file_and_filegroup_options >:: =**  
 如需詳細資訊，請參閱[ALTER DATABASE 檔案及檔案群組選項 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  
  
## <a name="remarks"></a>備註  
 若要移除的資料庫，請使用[DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)。  
  
 若要減少資料庫大小，請使用[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
 ALTER DATABASE 陳述式必須執行自動認可模式 (預設的交易管理模式)，且不能在明確或隱含的交易中。  
  
 資料庫檔案狀態 (如線上或離線) 的維護與資料庫狀態無關。 如需詳細資訊，請參閱[檔案狀態](../../relational-databases/databases/file-states.md)。 檔案群組內的檔案狀態決定了整個檔案群組的可用性。 若要使某個檔案群組為可用的，則在檔案群組中的所有檔案必須都在線上。 如果檔案群組離線，SQL 陳述式存取檔案群組的任何嘗試都會失敗，且會出現錯誤。 當您建置 SELECT 陳述式的查詢計劃時，查詢最佳化工具會避開在離線檔案群組中的非叢集索引和索引檢視表。 這樣會讓這些陳述式能夠執行成功。 不過，如果離線檔案群組包含目標資料表的堆積或叢集索引，SELECT 陳述式將會失敗。 除此之外，在離線檔案群組中，以 INSERT、UPDATE 或 DELETE 陳述式修改含有索引的資料表將會失敗。  
  
 當資料庫處於 RESTORING 狀態時，大部分的 ALTER DATABASE 陳述式都會失敗。 設定資料庫鏡像選項例外。 在使用中的還原作業期間，或是由於備份檔損毀導致資料庫或記錄檔的還原作業失敗時，資料庫都有可能處於 RESTORING 狀態。  
  
 設定下列其中一個選項，可清除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的計畫快取。  
  
|||  
|-|-|  
|OFFLINE|READ_WRITE|  
|ONLINE|MODIFY FILEGROUP DEFAULT|  
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|  
|COLLATE|MODIFY FILEGROUP READ_ONLY|  
|READ_ONLY|PAGE_VERIFY|  
  
 清除計畫快取會導致重新編譯所有後續執行計畫，而且可能會導致查詢效能突然暫時下降。 針對每次清除計畫快取的快取存放區，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔會包含下列參考訊息：「由於某些資料庫維護或重新設定作業，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 '%s' 快取存放區 (計畫快取的一部分) 發生 %d 次快取存放區排清」。 只要在該時間間隔內快取發生排清，這個訊息就會每五分鐘記錄一次。  
  
 在下列情況下也會排清程序快取：  
  
-   資料庫將 AUTO_CLOSE 資料庫選項設定為 ON。 當沒有任何使用者連接參考或使用資料庫時，背景工作嘗試關閉並自動關閉資料庫。  
  
-   您針對有預設選項的資料庫執行幾個查詢。 然後卸除資料庫。  
  
-   卸除來源資料庫的資料庫快照集。  
  
-   您已成功重建資料庫的交易記錄。  
  
-   您還原資料庫備份。  
  
-   您卸離資料庫。  
  
## <a name="changing-the-database-collation"></a>變更資料庫定序  
 將不同定序套用至資料庫之前，請確定已符合下列條件：  
  
-   您是資料庫目前唯一的使用者。  
  
-   沒有結構描述繫結的物件相依於資料庫的定序。  
  
     如果下列物件，這取決於資料庫定序，存在資料庫中，ALTER DATABASE*database_name*COLLATE 陳述式會失敗。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會針對每一個封鎖 ALTER 動作的物件傳回錯誤訊息：  
  
    -   利用 SCHEMABINDING 來建立的使用者定義函數和檢視表。  
  
    -   計算資料行。  
  
    -   CHECK 條件約束。  
  
    -   傳回包含字元資料行之資料表的資料表值函式，該資料行的定序繼承自預設資料庫定序。  
  
     變更資料庫定序時，就會自動更新非結構描述繫結實體的相依性資訊。  
  
 變更資料庫定序並不會在資料庫物件的任何系統名稱之間建立複本。 如果變更的定序產生重複名稱，下列命名空間可能會使資料庫定序的變更失敗：  
  
-   物件名稱，如程序、資料表、觸發程序或檢視表。  
  
-   結構描述名稱。  
  
-   群組、角色或使用者之類的主體。  
  
-   純量類型名稱，如系統和使用者定義類型。  
  
-   全文檢索目錄名稱。  
  
-   物件內的資料行或參數名稱。  
  
-   資料表內的索引名稱。  
  
新定序所造成的重複名稱會使變更動作失敗，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回錯誤訊息，指出出現重複名稱的命名空間。  
  
## <a name="viewing-database-information"></a>檢視資料庫資訊  
 您可以利用目錄檢視、系統函數和系統預存程序，以傳回資料庫、檔案和檔案群組的相關資訊。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-name-of-a-database"></a>A. 變更資料庫的名稱  
 下列範例會將 `AdventureWorks2012` 資料庫的名稱變更為 `Northwind`。  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
### <a name="b-changing-the-collation-of-a-database"></a>B. 變更資料庫的定序  
 下列範例會使用 `testdb`S 定序來建立名為 `SQL_Latin1_General_CP1_CI_A` 的資料庫，然後將 `testdb` 資料庫的定序變更為 `COLLATE French_CI_AI`。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
USE master;  
GO  
  
CREATE DATABASE testdb  
COLLATE SQL_Latin1_General_CP1_CI_AS ;  
GO  
  
ALTER DATABASE testDB  
COLLATE French_CI_AI ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
- [ALTER DATABASE &#40;Azure SQL Database &#41;](alter-database-azure-sql-database.md)  
- [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
- [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
- [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
- [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
- [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
- [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
- [sp_spaceused &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
- [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
- [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
- [sys.database_mirroring_witnesses &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
- [sys.data_spaces &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
- [sys.filegroups &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
- [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
- [系統資料庫](../../relational-databases/databases/system-databases.md)  
  

