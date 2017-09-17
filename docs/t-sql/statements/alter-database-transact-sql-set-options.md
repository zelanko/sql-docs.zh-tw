---
title: "ALTER DATABASE SET 選項 (TRANSACT-SQL) |Microsoft 文件"
description: "深入了解如何設定資料庫選項，例如自動微調，加密，SQL Server 和 Azure SQL Database 中的查詢存放區"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- online database state [SQL Server]
- database options [SQL Server]
- emergency database state [SQL Server]
- databases [SQL Server], options
- read-only databases
- recovery models [SQL Server], switching
- ALTER DATABASE statement, SET options
- offline database state [SQL Server]
- snapshot isolation framework option
- checksums [SQL Server]
- automatic tuning
- SQL plan regression correction
ms.assetid: f76fbd84-df59-4404-806b-8ecb4497c9cc
caps.latest.revision: 159
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 802642d2c9ba70c2a8750dc0ed5536e198a33f6f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-set-options-transact-sql"></a>ALTER DATABASE SET 選項 (Transact-SQL) 
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  本主題包含與設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中資料庫選項有關的 ALTER DATABASE 語法。 如需其他 ALTER DATABASE 語法，請參閱下列主題。  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  

-   [ALTER DATABASE &#40;Azure SQL Database &#41;](https://msdn.microsoft.com/library/mt574871.aspx) 

-   [ALTER DATABASE &#40;Azure SQL 資料倉儲 &#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)  
  
-   [ALTER DATABASE &#40;平行資料倉儲 &#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)  
  
資料庫鏡像， [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]，相容性層級和`SET`選項但這是個別的主題所述篇幅的因素。 如需詳細資訊，請參閱[ALTER DATABASE 資料庫鏡像 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)， [ALTER DATABASE SET HADR &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)，和[ALTER DATABASE 相容性層級 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
> [!NOTE]  
>  許多資料庫 set 選項可以設定目前工作階段使用[SET 陳述式 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-statements-transact-sql.md) ，通常會設定應用程式連線時。 工作階段層級 SET 選項會覆寫 **ALTER DATABASE SET** 值。 以下所述的資料庫選項皆為未明確提供其他 SET 選項值，因而可針對工作階段進行設定的值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ALTER DATABASE { database_name  | CURRENT }  
SET   
{  
    <optionspec> [ ,...n ] [ WITH <termination> ]   
}  
  
<optionspec> ::=   
{  
    <auto_option>   
  | <automatic_tuning_option>   
  | <change_tracking_option>   
  | <containment_option>   
  | <cursor_option>   
  | <database_mirroring_option>  
  | <date_correlation_optimization_option>  
  | <db_encryption_option>  
  | <db_state_option>  
  | <db_update_option>   
  | <db_user_access_option>   
  | <delayed_durability_option>  
  | <external_access_option>  
  | FILESTREAM ( <FILESTREAM_option> )  
  | <HADR_options>  
  | <mixed_page_allocation_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <recovery_option>  
  | <remote_data_archive_option>  
  | <service_broker_option>  
  | <snapshot_option>  
  | <sql_option>   
  | <target_recovery_time_option>   
  | <termination>  
}  
  
<auto_option> ::=   
{  
    AUTO_CLOSE { ON | OFF }   
  | AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] }   
  | AUTO_SHRINK { ON | OFF }   
  | AUTO_UPDATE_STATISTICS { ON | OFF }   
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
}  
  
<automatic_tuning_option> ::=  
{  
  AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = { ON | OFF } )
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
  
<containment_option> ::=   
   CONTAINMENT = { NONE | PARTIAL }  
  
<cursor_option> ::=   
{  
    CURSOR_CLOSE_ON_COMMIT { ON | OFF }   
  | CURSOR_DEFAULT { LOCAL | GLOBAL }   
}  
  
<database_mirroring_option>  
  ALTER DATABASE Database Mirroring  
  
<date_correlation_optimization_option> ::=  
    DATE_CORRELATION_OPTIMIZATION { ON | OFF }  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
  
<db_state_option> ::=  
    { ONLINE | OFFLINE | EMERGENCY }  
  
<db_update_option> ::=  
    { READ_ONLY | READ_WRITE }  
  
<db_user_access_option> ::=  
    { SINGLE_USER | RESTRICTED_USER | MULTI_USER }  
  
<delayed_durability_option> ::=  
    DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
<external_access_option> ::=  
{  
    DB_CHAINING { ON | OFF }  
  | TRUSTWORTHY { ON | OFF }  
  | DEFAULT_FULLTEXT_LANGUAGE = { <lcid> | <language name> | <language alias> }  
  | DEFAULT_LANGUAGE = { <lcid> | <language name> | <language alias> }  
  | NESTED_TRIGGERS = { OFF | ON }  
  | TRANSFORM_NOISE_WORDS = { OFF | ON }  
  | TWO_DIGIT_YEAR_CUTOFF = { 1753, ..., 2049, ..., 9999 }  
}  
<FILESTREAM_option> ::=  
{  
    NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL   
  | DIRECTORY_NAME = <directory_name>  
}  
<HADR_options> ::=  
    ALTER DATABASE SET HADR  
  
<mixed_page_allocation_option> ::=  
    MIXED_PAGE_ALLOCATION { OFF | ON }  
  
<parameterization_option> ::=  
    PARAMETERIZATION { SIMPLE | FORCED }  
  
<query_store_options> ::=  
{  
    QUERY_STORE   
    {  
          = OFF   
        | = ON [ ( <query_store_option_list> [,...n] ) ]  
        | ( < query_store_option_list> [,...n] )  
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
    | WAIT_STATS_CAPTURE_MODE = [ ON | OFF ]
}  
  
<recovery_option> ::=   
{  
    RECOVERY { FULL | BULK_LOGGED | SIMPLE }   
  | TORN_PAGE_DETECTION { ON | OFF }  
  | PAGE_VERIFY { CHECKSUM | TORN_PAGE_DETECTION | NONE }  
}  
  
<remote_data_archive_option> ::=  
{  
    REMOTE_DATA_ARCHIVE =  
    {  
        ON ( SERVER = <server_name> ,   
                  {   CREDENTIAL = <db_scoped_credential_name>  
                     | FEDERATED_SERVICE_ACCOUNT =  ON | OFF   
                  }  
               )  
      | OFF  
    }  
}  
  
<service_broker_option> ::=  
{  
    ENABLE_BROKER  
  | DISABLE_BROKER  
  | NEW_BROKER  
  | ERROR_BROKER_CONVERSATIONS  
  | HONOR_BROKER_PRIORITY { ON | OFF}  
}  
  
<snapshot_option> ::=  
{  
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
  | READ_COMMITTED_SNAPSHOT {ON | OFF }  
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = {ON | OFF }  
}  
<sql_option> ::=   
{  
    ANSI_NULL_DEFAULT { ON | OFF }   
  | ANSI_NULLS { ON | OFF }   
  | ANSI_PADDING { ON | OFF }   
  | ANSI_WARNINGS { ON | OFF }   
  | ARITHABORT { ON | OFF }   
  | COMPATIBILITY_LEVEL = { 90 | 100 | 110 | 120}  
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }   
  | NUMERIC_ROUNDABORT { ON | OFF }   
  | QUOTED_IDENTIFIER { ON | OFF }   
  | RECURSIVE_TRIGGERS { ON | OFF }   
}  
  
<target_recovery_time_option> ::=  
    TARGET_RECOVERY_TIME = target_recovery_time { SECONDS | MINUTES }  
  
<termination>  ::=   
{  
    ROLLBACK AFTER integer [ SECONDS ]   
  | ROLLBACK IMMEDIATE   
  | NO_WAIT  
}  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 這是要修改之資料庫的名稱。  
  
 CURRENT  
 **適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 `CURRENT`目前資料庫中執行的動作。 `CURRENT`不支援在所有內容中的所有選項。 如果`CURRENT`失敗，請提供資料庫名稱。  
  
 **\<auto_option >:: =**  
  
 控制自動選項。  
  
 AUTO_CLOSE { ON | OFF }  
 ON  
 資料庫會完整關閉，而當最後一位使用者結束之後，便會將它的資源釋放出來。  
  
 當使用者試圖重新使用資料庫時，便會自動重新開啟資料庫。 例如，藉由發出`USE database_name`陳述式。 如果在 AUTO_CLOSE 設為 ON 時完整關閉資料庫，則要等到使用者嘗試在下次重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 時使用資料庫之後，才會重新開啟資料庫。  
  
 OFF  
 在最後一個使用者結束之後，資料庫仍保持開啟狀態。  
  
 對於桌面資料庫而言，AUTO_CLOSE 選項非常有用，因為它可讓您將資料庫檔案當做一般檔案來管理。 您可以移動它們、複製它們來建立備份，甚至可以用電子郵件將它們傳給其他使用者。 AUTO_CLOSE 處理序是非同步的；重複開啟和關閉資料庫不會降低效能。  
  
> [!NOTE]  
>  AUTO_CLOSE 選項不是可在自主資料庫，或在提供[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_auto_close_on 資料行或 DATABASEPROPERTYEX 函數的 IsAutoClose 屬性來判斷這個選項的狀態。  
  
> [!NOTE]  
>  當 AUTO_CLOSE 是 ON 時， [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 目錄檢視中的某些資料行及 DATABASEPROPERTYEX 函數會傳回 NULL，因為資料庫無法擷取資料。 若要解決這個問題，請執行 USE 陳述式來開啟資料庫。  
  
> [!NOTE]  
>  資料庫鏡像需要 AUTO_CLOSE OFF。  
  
 當資料庫設為 AUTOCLOSE = ON 時，起始自動資料庫關閉的作業會清除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的計畫快取。 清除計畫快取會導致重新編譯所有後續執行計畫，而且可能會導致查詢效能突然暫時下降。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 (含) 以上版本，針對計畫快取中每個已清除的快取存放區，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔會包含下列參考訊息：「由於某些資料庫維護或重新設定作業，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 '%s' 快取存放區 (計劃快取的一部分) 發生 %d 次快取存放區排清。」 只要在該時間間隔內快取發生排清，這個訊息就會每五分鐘記錄一次。  
  
 AUTO_CREATE_STATISTICS { ON | OFF }  
 ON  
 查詢最佳化工具會視需要針對查詢述詞中的單一資料行建立統計資料，以便改善查詢計劃和查詢效能。 這些單一資料行統計資料是在查詢最佳化工具編譯查詢時所建立的。 它只會針對尚未成為現有統計資料物件之第一個資料行的資料行建立單一資料行統計資料。  
  
 預設值是 ON。 我們建議您針對大部分資料庫使用預設設定。  
  
 OFF  
 查詢最佳化工具不會在編譯查詢時，針對單一資料行建立統計資料。 將這個選項設定為 OFF 可能會導致次佳查詢計劃並降低查詢效能。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_auto_create_stats_on 資料行或 DATABASEPROPERTYEX 函數的 IsAutoCreateStatistics 屬性來判斷這個選項的狀態。  
  
 如需詳細資訊，請參閱 < 使用資料庫範圍統計資料選項 > 一節中[統計資料](../../relational-databases/statistics/statistics.md)。  
  
 INCREMENTAL = ON | OFF  
 當 AUTO_CREATE_STATISTICS 為 ON，且 INCREMENTAL 設為 ON 時，會在每次支援累加統計資料時，以累加方式建立自動建立的統計資料。 預設值是 OFF。 如需詳細資訊，請參閱 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)。  
  
 **適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 AUTO_SHRINK { ON | OFF }  
 ON  
 資料庫檔案是定期壓縮的候選項。  
  
 資料檔案和記錄檔都可以自動壓縮。 只有在資料庫設為 SIMPLE 復原模式或備份記錄時，AUTO_SHRINK 才會縮減交易記錄的大小。 當設為 OFF 時，便不會在定期檢查未用空間時，自動壓縮資料庫檔案。  
  
 當超出 25% 的檔案包含未用空間時，AUTO_SHRINK 選項便會壓縮檔案。 檔案會壓縮成 25% 的檔案是未用空間的大小，或建立檔案時的檔案大小，兩者取其較大者。  
  
 您不能壓縮唯讀資料庫。  
  
 OFF  
 在定期檢查未用空間時，不自動壓縮資料庫檔案。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_auto_shrink_on 資料行或 DATABASEPROPERTYEX 函數的 IsAutoShrink 屬性來判斷這個選項的狀態。  
  
> [!NOTE]  
>  自主資料庫無法使用 AUTO_SHRINK 選項。  
  
 AUTO_UPDATE_STATISTICS { ON | OFF }  
 ON  
 指定當查詢使用統計資料而且這些統計資料可能已過期時，查詢最佳化工具就會更新這些統計資料。 當插入、更新、刪除或合併作業變更資料表或索引檢視表中的資料分佈之後，統計資料就會變成過期。 查詢最佳化工具會計算自從上次更新統計資料以來資料修改的次數，並且比較修改次數與臨界值，藉以判斷統計資料可能過期的時間。 此臨界值是以資料表或索引檢視表中的資料列數目為基礎。  
  
 在編譯查詢之前以及執行快取查詢計劃之前，查詢最佳化工具會檢查是否有過期的統計資料。 在編譯查詢之前，查詢最佳化工具會使用查詢述詞中的資料行、資料表和索引檢視表來判斷哪些統計資料可能已過期。 在執行快取查詢計劃之前， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會確認查詢計劃是否參考最新的統計資料。  
  
 AUTO_UPDATE_STATISTICS 選項會套用至針對索引所建立的統計資料、查詢述詞中的單一資料行，以及使用 CREATE STATISTICS 陳述式所建立的統計資料。 此外，這個選項也會套用至篩選的統計資料。  
  
 預設值是 ON。 我們建議您針對大部分資料庫使用預設設定。  
  
 您可以使用 AUTO_UPDATE_STATISTICS_ASYNC 選項來指定要以同步或非同步方式更新統計資料。  
  
 OFF  
 指定當查詢使用統計資料而且這些統計資料可能已過期時，查詢最佳化工具不會更新這些統計資料。 將這個選項設定為 OFF 可能會導致次佳查詢計劃並降低查詢效能。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_auto_update_stats_on 資料行或 DATABASEPROPERTYEX 函數的 IsAutoUpdateStatistics 屬性來判斷這個選項的狀態。  
  
 如需詳細資訊，請參閱 < 使用資料庫範圍統計資料選項 > 一節中[統計資料](../../relational-databases/statistics/statistics.md)。  
  
 AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
 ON  
 指定 AUTO_UPDATE_STATISTICS 選項的統計資料更新是非同步的。 在查詢最佳化工具編譯查詢之前，它不會等候統計資料更新完成。  
  
 除非 AUTO_UPDATE_STATISTICS 設為 ON，否則將這個選項設為 ON 沒有作用。  
  
 根據預設，AUTO_UPDATE_STATISTICS_ASYNC 選項設定為 OFF，而且查詢最佳化工具會以同步方式更新統計資料。  
  
 OFF  
 指定 AUTO_UPDATE_STATISTICS 選項的統計資料更新是同步的。 在查詢最佳化工具編譯查詢之前，它會先等候統計資料更新完成。  
  
 除非 AUTO_UPDATE_STATISTICS 設為 ON，否則將這個選項設為 OFF 沒有作用。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_auto_update_stats_async_on 資料行來判斷這個選項的狀態。  
  
 描述何時使用同步或非同步統計資料更新的詳細資訊，請參閱 < 使用資料庫範圍統計資料選項 > 一節，在[統計資料](../../relational-databases/statistics/statistics.md)。  
  
 **\<automatic_tuning_option >:: =**  
 **適用於**： [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]。  

 啟用或停用`FORCE_LAST_GOOD_PLAN`[自動微調](../../relational-databases/automatic-tuning/automatic-tuning.md)選項。  
  
 FORCE_LAST_GOOD_PLAN = {ON |OFF}  
 ON  
 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]自動強制執行的最後一個已知的良好計畫[!INCLUDE[tsql_md](../../includes/tsql_md.md)]其中新的 SQL 計畫會讓效能衰退的查詢。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]進行持續監視查詢效能[!INCLUDE[tsql_md](../../includes/tsql_md.md)]與強制的計劃的查詢。 如果沒有進一步提升效能，[!INCLUDE[ssde_md](../../includes/ssde_md.md)]會繼續使用最後一個已知的良好計畫。 如果未偵測到的效能提升，[!INCLUDE[ssde_md](../../includes/ssde_md.md)]會產生新的 SQL 計劃。 陳述式會失敗，如果未啟用查詢存放區，或不在*讀寫*模式。   

 OFF  
 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]報告中的 SQL 計劃變更所造成的可能查詢效能衰退[sys.dm_db_tuning_recommendations](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)檢視。 不過，這些建議不會自動套用。 使用者可以藉由套用監視使用中的建議和修復識別問題[!INCLUDE[tsql_md](../../includes/tsql_md.md)]顯示的檢視中的指令碼。 這是預設值。

 **\<change_tracking_option >:: =**  
  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 控制變更追蹤選項。 您可以啟用變更追蹤、設定選項、變更選項，以及停用變更追蹤。 如需範例，請參閱本主題稍後的「範例」一節。  
  
 ON  
 啟用資料庫的變更追蹤。 當您啟用變更追蹤時，也可以設定 AUTO CLEANUP 和 CHANGE RETENTION 選項。  
  
 AUTO_CLEANUP = { ON | OFF }  
 ON  
 在經過了指定的保留週期後，將會自動移除變更追蹤資訊。  
  
 OFF  
 不會從資料庫中移除變更追蹤資料。  
  
 CHANGE_RETENTION =*retention_period* {天 |小時 |分鐘}  
 指定在資料庫中保存變更追蹤資訊的最小週期。 只有當 AUTO_CLEANUP 值為 ON 時，才會移除資料。  
  
 *retention_period*是一個整數，指定保留週期的數值元件。  
  
 預設保留週期為 2 天。 最小保留週期是 1 分鐘。 預設保留型別為天。  
  
 OFF  
 停用資料庫的變更追蹤。 在您可以停用資料庫的變更追蹤以前，必須先在所有資料表上停用變更追蹤。  
  
 **\<containment_option >:: =**  
  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 控制資料庫內含項目選項。  
  
 內含項目 = {NONE |部分}  
 無  
 資料庫不是自主資料庫。  
  
 PARTIAL  
 資料庫是自主資料庫。 如果資料庫已啟用複寫、變更資料擷取或變更追蹤，無法將資料庫內含項目設為部分。 在一次失敗之後錯誤檢查會停止。 如需自主資料庫的詳細資訊，請參閱 [自主資料庫](../../relational-databases/databases/contained-databases.md)。  
  
> [!NOTE]  
>  無法在中設定內含項目[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。 內含項目未明確指定，但[!INCLUDE[ssSDS](../../includes/sssds-md.md)]可以使用包含的功能，例如包含資料庫使用者。  
  
 **\<cursor_option >:: =**  
  
 控制資料指標選項。  
  
 CURSOR_CLOSE_ON_COMMIT { ON | OFF }  
 ON  
 關閉認可或回復交易時在開啟狀態的任何資料指標。  
  
 OFF  
 當認可交易時，資料指標維持開啟狀態；回復交易會關閉任何資料指標，但定義為 INSENSITIVE 或 STATIC 的資料指標除外。  
  
 利用 SET 陳述式來設定的連接層級設定會覆寫 CURSOR_CLOSE_ON_COMMIT 的預設資料庫設定。 根據預設，當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，ODBC 和 OLE DB 用戶端會發出連接層級的 SET 陳述式，將工作階段的 CURSOR_CLOSE_ON_COMMIT 設為 OFF。 如需詳細資訊，請參閱 [SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_cursor_close_on_commit_on 資料行，或 DATABASEPROPERTYEX 函數的 IsCloseCursorsOnCommitEnabled 屬性來判斷這個選項的狀態。  
  
 CURSOR_DEFAULT { LOCAL | GLOBAL }  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 控制資料指標範圍是使用 LOCAL 還是 GLOBAL。  
  
 LOCAL  
 當指定 LOCAL，而且資料指標並未在建立時定義為 GLOBAL 時，資料指標的範圍僅限於資料指標建立時所在之批次、預存程序或觸發程序的本機範圍。 資料指標名稱只在這個範圍內有效。 批次、預存程序或觸發程序內的區域資料指標變數或是預存程序 OUTPUT 參數可以參考資料指標。 當批次、預存程序或觸發程序結束時，除非在 OUTPUT 參數中傳回資料指標，否則會隱含地取消配置資料指標。 如果在 OUTPUT 參數中傳回資料指標，當最後一個參考資料指標的變數取消配置或離開範圍時，便會取消配置資料指標。  
  
 GLOBAL  
 當指定 GLOBAL，而且資料指標並未在建立時定義為 LOCAL 時，資料指標的範圍便是連接的全域範圍。 連接所執行的任何預存程序或批次內都可以參考資料指標名稱。  
  
 只有在中斷連接時，才會隱含地取消配置資料指標。 如需詳細資訊，請參閱[DECLARE CURSOR &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md).  
  
 您可以檢查 sys.databases 目錄檢視中的 is_local_cursor_default 資料行或 DATABASEPROPERTYEX 函數的 IsLocalCursorsDefault 屬性來判斷這個選項的狀態。  
  
 **\<database_mirroring >**  
  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 引數的描述，請參閱[ALTER DATABASE 資料庫鏡像 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md).  
  
 **\<date_correlation_optimization_option >:: =**  
  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 控制 date_correlation_optimization 選項。  
  
 DATE_CORRELATION_OPTIMIZATION { ON | OFF }  
 ON  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]維護資料庫中由 FOREIGN KEY 條件約束所連結且具有任何兩個資料表之間的相互關聯統計資料**datetime**資料行。  
  
 OFF  
 不維護相互關聯統計資料。  
  
 若要將 DATE_CORRELATION_OPTIMIZATION 設定為 ON，則除了正在執行 ALTER DATABASE 陳述式的連接外，資料庫都不可以有使用中的連接。 之後就可以支援多個連接。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_date_correlation_on 資料行來判斷這個選項目前的設定。  
  
 **\<db_encryption_option >:: =**  
  
 控制資料庫加密狀態。  
  
 ENCRYPTION {ON | OFF}  
 設定資料庫要加密 (ON) 或是不要加密 (OFF)。 如需有關資料庫加密的詳細資訊，請參閱[透明資料加密 &#40;TDE &#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)，和[Azure SQL Database 的透明資料加密](../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)。  
  
 在資料庫層級啟用加密時，所有的檔案群組都會加密。 任何新的檔案群組都會繼承加密的屬性。 如果資料庫內有任何檔案群組設定為 **READ ONLY**，則資料庫加密作業將會失敗。  
  
 您可以看到資料庫的加密狀態使用[sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)動態管理檢視。  
  
 **\<db_state_option >:: =**  
  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 控制資料庫的狀態。  
  
 OFFLINE  
 關閉資料庫，並將它完整關機，再標示為離線。 資料庫在離線狀態時，無法修改。  
  
 ONLINE  
 資料庫在開啟狀態，可供使用。  
  
 EMERGENCY  
 資料庫是標示為 READ_ONLY、記錄已停用並限定只有系統管理員 (sysadmin) 固定伺服器角色的成員才可存取。 EMERGENCY 主要是做為疑難排解的用途。 例如，由於記錄檔損毀而被標示有疑問的資料庫可以設為 EMERGENCY 狀態。 在這個情況下，系統管理員可以進行資料庫的唯讀存取。 只有系統管理員 (sysadmin) 固定伺服器角色的成員，可以將資料庫設定為 EMERGENCY 狀態。  
  
> [!NOTE]  
>  **權限：**主旨資料庫的 ALTER DATABASE 權限，才能將資料庫變更為離線或緊急狀態狀態。 若要將資料庫從離線狀態移到連線狀態，需要伺服器層級的 ALTER ANY DATABASE 權限。  
  
 可以檢查中的 state 和 state_desc 資料行來判斷這個選項的狀態[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視或的 Status 屬性[DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)函式。 如需詳細資訊，請參閱 [Database States](../../relational-databases/databases/database-states.md)。  
  
 標示為 RESTORING 的資料庫不能設為 OFFLINE、ONLINE 或 EMERGENCY。 在使用中的還原作業期間，或是由於備份檔損毀導致資料庫或記錄檔的還原作業失敗時，資料庫都有可能處於 RESTORING 狀態。  
  
 **\<db_update_option >:: =**  
  
 控制是否允許更新資料庫。  
  
 READ_ONLY  
 使用者可以從資料庫中讀取資料，但無法加以修改。  
  
> [!NOTE]  
>  如果要提高查詢的效能，請先更新統計資料，再將資料庫設為 READ_ONLY。 如果資料庫設為 READ_ONLY 之後，還需要其他的統計資料，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 將會在 tempdb 中建立統計資料。 如需有關唯讀資料庫的統計資料的詳細資訊，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。  
  
 READ_WRITE  
 資料庫可以執行讀寫作業。  
  
 若要變更這個狀態，您必須具有資料庫的獨佔存取權。 如需詳細資訊，請參閱 SINGLE_USER 子句。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]同盟資料庫上，SET { READ_ONLY | READ_WRITE } 會停用。  
  
 **\<db_user_access_option >:: =**  
  
 控制使用者對資料庫的存取權。  
  
 SINGLE_USER  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 指定每次只能有一位使用者存取資料庫。 如果指定了 SINGLE_USER，且沒有其他使用者連接到資料庫，就會封鎖 ALTER DATABASE 陳述式，直到所有使用者都中斷連接指定的資料庫為止。 若要覆寫這個行為，請參閱 WITH\<終止 > 子句。  
  
 資料庫會保留在 SINGLE_USER 模式中，即使是將選項記錄設為關閉的使用者也是如此。 此時其他使用者可以連接到這個資料庫，但只能有一位。  
  
 將資料庫設為 SINGLE_USER 之前，請先確定 AUTO_UPDATE_STATISTICS_ASYNC 選項是否設為 OFF。 當設為 ON 時，更新統計資料的背景執行緒會取得資料庫連接，而您就無法以單一使用者模式存取資料庫。 若要檢視這個選項的狀態，查詢中的 is_auto_update_stats_async_on 資料行[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視。 如果選項設為 ON，請執行下列工作：  
  
1.  將 AUTO_UPDATE_STATISTICS_ASYNC 設為 OFF。  
  
2.  檢查是否有作用中的非同步統計資料工作，藉由查詢[sys.dm_exec_background_job_queue](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md)動態管理檢視。  
  
 如果沒有使用中的工作，允許的作業完成，或手動予以終止使用[KILL STATS JOB](../../t-sql/language-elements/kill-stats-job-transact-sql.md)。  
  
RESTRICTED_USER  
 RESTRICTED_USER 只允許 db_owner 固定資料庫角色以及資料庫建立者 (dbcreator) 和系統管理員 (sysadmin) 固定伺服器角色的成員連接到資料庫，但並不限制他們的數目。 在 ALTER DATABASE 陳述式的 termination 子句所指定的時間範圍中，會中斷資料庫的所有連接。 在資料庫進入 RESTRICTED_USER 狀態之後，不合格使用者的連接嘗試都會遭到拒絕。  
  
MULTI_USER  
 允許所有具備適當權限來連接資料庫的使用者。  
  
 您可以檢查 sys.databases 目錄檢視中的 user_access 資料行或 DATABASEPROPERTYEX 函數的 UserAccess 屬性來判斷這個選項的狀態。  
  
 **\<delayed_durability_option >:: =**  
  
 **適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 控制交易是否認可完全持久或延遲的持久。  
  
 DISABLED  
 接在 SET DISABLED 後面的所有交易都是完全持久。 在不可部分完成的區塊或 Commit 陳述式中設定的任何持久性選項都會被忽略。  
  
 ALLOWED  
 接在 SET ALLOWED 後面的所有交易都是完全持久或延遲的持久，視不可部分完成的區塊或 Commit 陳述式中設定的持久性選項而定。  
  
 FORCED  
 接在 SET FORCED 後面的所有交易都是延遲的持久。 在不可部分完成的區塊或 Commit 陳述式中設定的任何持久性選項都會被忽略。  
  
 **\<external_access_option >:: =**  
  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 控制外部資源 (如另一個資料庫的物件) 是否能夠存取資料庫。  
  
 DB_CHAINING { ON | OFF }  
 ON  
 資料庫可以是跨資料庫擁有權鏈結的來源或目標。  
  
 OFF  
 資料庫無法參與跨資料庫擁有權鏈結。  
  
> [!IMPORTANT]  
>  當 cross db ownership chaining 伺服器選項為 0 (OFF) 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體可以辨識這項設定。 當 cross db ownership chaining 為 1 (ON) 時，不論這個選項的值為何，所有使用者資料庫都可以參與跨資料庫擁有權鏈結。 使用此選項設定[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
 若要設定此選項時，需要在資料庫上的 CONTROL SERVER 權限。  
  
 下列系統資料庫不能設定 DB_CHAINING 選項：master、model 和 tempdb。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_db_chaining_on 資料行來判斷這個選項的狀態。  
  
 TRUSTWORTHY { ON | OFF }  
 ON  
 使用模擬內容的資料庫模組 (如使用者定義函數或預存程序) 能夠在資料庫之外存取資源。  
  
 OFF  
 模擬內容中的資料庫模組無法存取資料庫之外的資源。  
  
 每當附加資料庫時，TRUSTWORTHY 都設為 OFF。  
  
 依預設，除了 msdb 資料庫以外，所有的系統資料庫都會將 TRUSTWORTHY 設為 OFF。 model 和 tempdb 資料庫的這個值不可變更。 建議您絕對不要將 master 資料庫的 TRUSTWORTHY 選項設為 ON。  
  
 若要設定此選項時，需要在資料庫上的 CONTROL SERVER 權限。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_trustworthy_on 資料行來判斷這個選項的狀態。  
  
 DEFAULT_FULLTEXT_LANGUAGE  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定全文檢索索引資料行的預設語言值。  
  
> [!IMPORTANT]  
>  只有當 CONTAINMENT 已經設為 PARTIAL 時，才允許這個選項。 如果 CONTAINMENT 設定為 NONE，便會發生錯誤。  
  
 DEFAULT_LANGUAGE  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定所有新建立之登入的預設語言。 可藉由提供地區設定識別碼 (LCID)、語言名稱或語言別名來指定語言。 如需可接受的語言名稱和別名的清單，請參閱[sys.syslanguages &#40;TRANSACT-SQL &#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md). 只有當 CONTAINMENT 已經設為 PARTIAL 時，才允許這個選項。 如果 CONTAINMENT 設定為 NONE，便會發生錯誤。  
  
 NESTED_TRIGGERS  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定 AFTER 觸發程序是否可以重疊顯示；亦即，執行起始另一個觸發程序的動作，後者再起始另一個觸發程序等。 只有當 CONTAINMENT 已經設為 PARTIAL 時，才允許這個選項。 如果 CONTAINMENT 設定為 NONE，便會發生錯誤。  
  
 TRANSFORM_NOISE_WORDS  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 如果非搜尋字或停用字詞造成全文檢索查詢的布林運算失敗，用來隱藏錯誤訊息。 只有當 CONTAINMENT 已經設為 PARTIAL 時，才允許這個選項。 如果 CONTAINMENT 設定為 NONE，便會發生錯誤。  
  
 TWO_DIGIT_YEAR_CUTOFF  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 從 1753 到 9999 中指定一個整數來表示截止年份，以便將兩位數年份解譯為四位數年份。 只有當 CONTAINMENT 已經設為 PARTIAL 時，才允許這個選項。 如果 CONTAINMENT 設定為 NONE，便會發生錯誤。  
  
 **\<FILESTREAM_option >:: =**  
  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 控制 FileTable 的設定。  
  
 NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }  
 OFF  
 已停用 FileTable 資料的非交易式存取。  
  
 READ_ONLY  
 非交易式處理序可以讀取此資料庫中 FileTable 的 FILESTREAM 資料。  
  
 FULL  
 已啟用 FileTable 中 FILESTREAM 資料的完整非交易式存取。  
  
 DIRECTORY_NAME =  *\<directory_name >*  
 Windows 相容的目錄名稱。 此名稱在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的所有資料庫層級目錄名稱之間必須是唯一的。 無論定序設定為何，唯一性比較皆不會區分大小寫。 在此資料庫中建立 FileTable 之前，必須先設定這個選項。  
  
 **\<HADR_options >:: =**  
  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 請參閱[ALTER DATABASE SET HADR &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md).  
  
 **\<mixed_page_allocation_option >:: =**  
  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。 不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 MIXED_PAGE_ALLOCATION {關閉 |是否在} 控制項資料庫可建立的混合的範圍使用資料表或索引的前八個頁面的初始頁面。  
  
 OFF  
 此外，資料庫一律會建立使用統一範圍的初始頁面。 這是預設值。  
  
 ON  
 資料庫可以建立使用混合的範圍的起始頁面。  
  
 這項設定是 ON，所有系統資料庫。 **tempdb**是唯一的系統資料庫，支援 OFF。  
  
 **\<PARAMETERIZATION_option >:: =**  
  
 控制參數化選項。  
  
 PARAMETERIZATION { SIMPLE | FORCED }  
 SIMPLE  
 根據資料庫的預設行為，將查詢參數化。  
  
 FORCED  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將資料庫中的所有查詢參數化。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_parameterization_forced 資料行來判斷這個選項目前的設定。  
  
 **\<query_store_options >:: =**  
  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))、 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 ON | OFF | CLEAR [ ALL ]  
 控制是否在此資料庫中啟用查詢存放區，並且控制查詢存放區內容的移除。  
  
ON  
 啟用查詢存放區。  
  
OFF  
 停用查詢存放區。  這是預設值。   
  
CLEAR  
 移除查詢存放區的內容。  
  
OPERATION_MODE  
 描述查詢存放區的作業模式。 有效值為 READ_ONLY 和 READ_WRITE。 在 READ_WRITE 模式中，查詢存放區會收集並保存查詢計劃和執行階段執行統計資料資訊。 在 READ_ONLY 模式中，可以從查詢存放區讀取資訊，但不會加入新資訊。 如果查詢存放區配置的空間的最大值已用盡，查詢存放區會將操作模式變更為 READ_ONLY。  
  
 CLEANUP_POLICY  
 描述查詢存放區的資料保留原則。 STALE_QUERY_THRESHOLD_DAYS 決定查詢存放區中查詢的資訊保留的天數。 STALE_QUERY_THRESHOLD_DAYS 的類型**bigint**。  
  
 DATA_FLUSH_INTERVAL_SECONDS  
 決定將寫入查詢存放區的資料保存到磁碟的頻率。 為了獲得最佳效能，查詢存放區所收集的資料會以非同步方式寫入磁碟。 此非同步傳輸發生的頻率是使用 DATA_FLUSH_INTERVAL_SECONDS 引數所設定。 DATA_FLUSH_INTERVAL_SECONDS 的類型**bigint**。  
  
 MAX_STORAGE_SIZE_MB  
 判斷配置給查詢存放區的空間。 到達了 MAX_STORAGE_SIZE_MB 是型別**bigint**。  
  
 INTERVAL_LENGTH_MINUTES  
 決定執行階段執行統計資料彙總至查詢存放區的時間間隔。 若要將空間使用量最佳化，在執行階段統計資料存放區中的執行階段執行統計資料會透過固定的時段彙總。 這個固定的時段是使用 INTERVAL_LENGTH_MINUTES 引數所設定。 INTERVAL_LENGTH_MINUTES 的類型**bigint**。  
  
 SIZE_BASED_CLEANUP_MODE  
 控制是否清除要自動啟用當總資料量接近大小上限：  
  
 OFF  
 將不會自動啟用大小基礎清除。 
  
 AUTO  
 當大小在磁碟上自動啟動基礎的清除的大小達到 90%的**到達了 max_storage_size_mb**。 大小基礎清除先移除最高和最舊的查詢。 會在大約 80%的停止**到達了 max_storage_size_mb**。  這是預設組態值。  
  
 SIZE_BASED_CLEANUP_MODE 是型別**nvarchar**。  
  
 QUERY_CAPTURE_MODE  
 指定目前使用中的查詢擷取模式：  
  
 會擷取所有的所有查詢。 這是預設組態值。  這是預設組態值[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]
  
 自動擷取相關的查詢執行計數和資源耗用量為基礎。  這是預設組態值[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 無停止擷取新的查詢。 查詢存放區將會繼續收集已擷取的查詢編譯和執行階段統計資料。 因為您可能會遺失擷取重要的查詢，請小心使用此設定。  
  
 QUERY_CAPTURE_MODE 是型別**nvarchar**。  
  
 max_plans_per_query  
 表示維護每個查詢計劃的大數目的整數。 預設值為 200。  
  
 **\<recovery_option >:: =**  
  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 控制資料庫復原選項及磁碟 I/O 錯誤檢查。  
  
 FULL  
 在媒體失敗之後，利用交易記錄備份來提供完整復原。 如果資料檔案損毀，媒體復原可以還原所有已認可的交易。 如需詳細資訊，請參閱[復原模式 &#40;SQL Server &#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)。  
  
 BULK_LOGGED  
 結合某些大規模或大量作業之最佳效能與最少記錄使用空間的優點，提供媒體失敗之後的復原功能。 如需哪些作業可以進行最低限度記錄的資訊，請參閱[交易記錄 &#40;SQL Server &#41;](../../relational-databases/logs/the-transaction-log-sql-server.md). 在 BULK_LOGGED 復原模式之下，這些作業的只會記錄基本資訊。 如需詳細資訊，請參閱[復原模式 &#40;SQL Server &#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)。  
  
 SIMPLE  
 提供使用最少記錄空間的簡單備份策略。 當伺服器失敗復原不再需要記錄空間，會自動重複使用這個記錄空間。 如需詳細資訊，請參閱[復原模式 &#40;SQL Server &#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)。  
  
> [!IMPORTANT]  
>  簡單復原模式比另兩種模式更容易管理，但在資料檔案損毀時，遺失資料的風險比較大。 在最近的資料庫或差異資料庫備份之後進行的所有變更都會遺失，必須以手動方式重新輸入。  
  
 預設復原模式取決於 **model** 資料庫的復原模式。 如需有關如何選擇適當復原模式的詳細資訊，請參閱[復原模式 &#40;SQL Server &#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
 可以檢查來判斷這個選項的狀態**recovery_model**和**recovery_model_desc** sys.databases 目錄檢視或 DATABASEPROPERTYEX 的 Recovery 屬性中資料行函式。  
  
 TORN_PAGE_DETECTION { ON | OFF }  
 ON  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 能夠偵測出不完整的頁面。  
  
 OFF  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 無法偵測到不完整的頁面。  
  
> [!IMPORTANT]  
>  在未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中，將移除 TORN_PAGE_DETECTION ON | OFF 語法結構。 請避免在新的開發工作中使用這項語法結構，並規劃修改目前使用這項語法結構的應用程式。 請改用 PAGE_VERIFY 選項。  
  
 PAGE_VERIFY { CHECKSUM | TORN_PAGE_DETECTION | NONE }  
 探索 I/O 路徑錯誤所造成的損毀資料庫頁面。 磁碟 I/O 路徑錯誤可能是資料庫損毀問題的原因，這通常是因為電源故障或頁面寫入磁碟時磁碟硬體故障所造成。  
  
 CHECKSUM  
 計算整個頁面內容的總和檢查碼，當頁面寫入磁碟時，將值儲存在頁首。 從磁碟讀取頁面時，總和檢查碼會重新計算並與頁首所儲存的總和檢查碼值做比較。 如果值都不符，便會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔和 Windows 事件記錄檔中，報告錯誤訊息 824 (表示總和檢查碼失敗)。 總和檢查碼失敗表示 I/O 路徑發生問題。 判斷主要原因時，需要調查硬體、韌體驅動程式、BIOS、篩選驅動程式 (例如，病毒軟體) 和其他 I/O 路徑元件。  
  
 TORN_PAGE_DETECTION  
 將每個 512 位元組磁區的 2 位元模式儲存在 8 KB 資料庫頁面上，當頁面寫入磁碟時，便將它儲存在資料庫頁首。 當從磁碟中讀取頁面時，會比較頁首中所儲存的損毀位元和實際的頁面磁區資訊。 值不符合表示該頁面只有一部分寫入磁碟中。 在這個狀況下，會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔和 Windows 事件記錄檔中，報告錯誤訊息 824 (表示發生損毀頁的錯誤)。 如果真的是頁面寫入不完整，通常會由資料庫復原作業來偵測出損毀頁。 不過，其他 I/O 路徑失敗也可能隨時造成損毀頁。  
  
 無  
 資料庫頁面寫入不會產生 CHECKSUM 或 TORN_PAGE_DETECTION 值。 在讀取期間，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 即使頁首包含 CHECKSUM 或 TORN_PAGE_DETECTION 值，亦不會驗證總和檢查碼或損毀頁。  
  
 當您使用 PAGE_VERIFY 選項時，請考慮下列要點：  
  
-   預設值是 CHECKSUM。  
  
-   將使用者或系統資料庫升級為 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本時，都會保留 PAGE_VERIFY 值 (NONE 或 TORN_PAGE_DETECTION)。 我們建議您使用 CHECKSUM。  
  
    > [!NOTE]  
    >  在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，tempdb 資料庫的 PAGE_VERIFY 資料庫選項設定為 NONE 而且無法修改。 在[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]和更新版本，tempdb 資料庫的預設值是總和檢查碼的全新安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝時，預設值仍然維持 NONE。 此選項可以進行修改。 我們建議您針對 tempdb 資料庫使用 CHECKSUM。  
  
-   TORN_PAGE_DETECTION 可以使用較少資源，但所提供的 CHECKSUM 保護最少。  
  
-   在資料庫不離線、不鎖定，或不妨礙資料庫並行作業的情況下，可以設定 PAGE_VERIFY。  
  
-   CHECKSUM 與 TORN_PAGE_DETECTION 互斥。 這兩個選項無法同時啟用。  
  
 當偵測到損毀頁或總和檢查碼失敗時，您可以還原資料來加以復原，如果失敗只限於索引頁面，您可以重建索引。 如果您發現總和檢查碼失敗，且要判斷受影響的資料庫頁面類型，請執行 DBCC CHECKDB。 如需有關還原選項的詳細資訊，請參閱[RESTORE 引數 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md). 雖然還原資料可以解決資料損毀問題，但您仍應診斷主要原因 (如磁碟硬體故障)，並盡快更正，以防止繼續發生錯誤。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會重試任何因總和檢查碼、損毀頁或其他 I/O 錯誤而失敗的讀取作業四次。 如果任何一次重試讀取成功，都會將訊息寫入錯誤記錄檔中，且會繼續觸發讀取作業的命令。 如果重試失敗，此命令便會失敗，且會出現錯誤訊息 824。  
  
 如需總和檢查碼、 損毀的頁、 讀取重試的詳細資訊，錯誤訊息 823 和 824，以及其他[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]I/O 稽核功能，請參閱 < [Microsoft 寍鯚](http://go.microsoft.com/fwlink/?LinkId=47160)。  
  
 可以檢查 page_verify_option 資料行來判斷這個選項的目前設定[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視或的 IsTornPageDetectionEnabled 屬性[DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)函式。  
  
**\<remote_data_archive_option >:: =**  
  
 **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 啟用或停用 Stretch Database 的資料庫。 如需詳細資訊，請參閱 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)。  
  
REMOTE_DATA_ARCHIVE = {ON (SERVER =\<伺服器名稱 >，{認證 = \<db_scoped_credential_name > |FEDERATED_SERVICE_ACCOUNT = ON |OFF}) |關閉 ON  
 為資料庫啟用 Stretch Database。 如需詳細資訊，包括其他必要條件，請參閱[針對資料庫啟用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)。  
  
 **權限**。 資料庫或資料表啟用 Stretch Database 需要 db_owner 權限。 針對資料庫啟用 Stretch Database 也需要 CONTROL DATABASE 權限。  
  
SERVER =\<伺服器名稱 >  
 指定 Azure 伺服器的位址。 包含`.database.windows.net`名稱部分。 例如， `MyStretchDatabaseServer.database.windows.net`。  
  
認證 = \<db_scoped_credential_name >  
 指定資料庫範圍認證的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用來連接到 Azure 的伺服器。 請確定認證存在，然後再執行此命令。 如需詳細資訊，請參閱[CREATE DATABASE SCOPED CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
FEDERATED_SERVICE_ACCOUNT = ON |關閉  
 您可以使用針對在內部部署 SQL Server 的同盟的服務帳戶，當下列條件成立時，與遠端 Azure 伺服器通訊。  
  
-   正在執行之 SQL Server 執行個體下的服務帳戶是網域帳戶。  
  
-   網域帳戶所屬的網域，其 Active Directory 與 Azure Active Directory 同盟。  
  
-   遠端 Azure 伺服器已設定支援 Azure Active Directory 驗證。  
  
-   正在執行之 SQL Server 執行個體下的服務帳戶必須設定為遠端 Azure 伺服器上的 dbmanager 或 sysadmin 帳戶。  
  
 如果您指定 ON 時，您也無法指定 CREDENTIAL 引數。 如果您指定 OFF 時，您必須提供 CREDENTIAL 引數。  
  
 OFF  
 停用 Stretch Database 的資料庫。 如需詳細資訊，請參閱 [停用 Stretch Database 並帶回遠端資料](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)。  
  
 您可以只後停用 Stretch Database 資料庫的資料庫不再包含任何已啟用 Stretch Database 的資料表。 停用 Stretch Database 後，資料移轉停駐點和查詢結果不再包含來自遠端資料表的結果。  
  
 停用 Stretch，並不會移除遠端資料庫。 若您想要刪除遠端資料庫，則必須使用 Azure 管理入口網站將其卸除。  
  
**\<service_broker_option >:: =**  
  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 控制下列[!INCLUDE[ssSB](../../includes/sssb-md.md)]選項： 啟用或停用訊息傳遞、 設定新[!INCLUDE[ssSB](../../includes/sssb-md.md)]識別碼或將交談優先權設定為 ON 或 OFF。  
  
 ENABLE_BROKER  
 指定啟用指定之資料庫的 [!INCLUDE[ssSB](../../includes/sssb-md.md)]。 啟動訊息傳遞，且 sys.databases 目錄檢視中的 is_broker_enabled 旗標會設為 true。 資料庫會保留現有的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 識別碼。 當資料庫是資料庫鏡像組態中的主體時，無法啟用 Service Broker。  
  
> [!NOTE]  
>  ENABLE_BROKER 需要獨佔式資料庫鎖定。 如果其他工作階段已鎖定資料庫內的資源，ENABLE_BROKER 將會等候到其他工作階段釋放其鎖定為止。 若要在使用者資料庫內啟用 [!INCLUDE[ssSB](../../includes/sssb-md.md)]，請確定在您執行 ALTER DATABASE SET ENABLE_BROKER 陳述式之前，沒有其他工作階段正在使用此資料庫，例如將資料庫置於單一使用者模式。 若要在 msdb 資料庫中啟用 [!INCLUDE[ssSB](../../includes/sssb-md.md)]，請先停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent，使 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 可以取得必要的鎖定。  
  
 DISABLE_BROKER  
 指定針對指定的資料庫停用 [!INCLUDE[ssSB](../../includes/sssb-md.md)]。 停止訊息傳遞，而且 sys.databases 目錄檢視中的 is_broker_enabled 旗標會設為 false。 資料庫會保留現有的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 識別碼。  
  
 NEW_BROKER   
 指定資料庫應該接收新的 Broker 識別碼。 由於資料庫會被視為新的 Service Broker，因此，系統會立即移除資料庫中所有現有的交談，不會產生結束對話訊息。 您必須使用新的識別碼來重新建立參考舊 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 識別碼的任何路由。  
  
 ERROR_BROKER_CONVERSATIONS  
 指定 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 訊息傳遞已啟用。 這會保留現有[!INCLUDE[ssSB](../../includes/sssb-md.md)]資料庫識別項。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會結束資料庫中的所有交談，並產生錯誤。 這可讓應用程式執行現有交談的正規清除工作。  
  
 HONOR_BROKER_PRIORITY {ON | OFF}  
 ON  
 傳送作業會將指派給交談的優先權等級列入考量。 具有高優先權等級之交談的訊息會在被指派低優先權等級之交談的訊息之前傳送。  
  
 OFF  
 傳送作業的執行方式，就像是所有交談都有預設優先權等級一樣。  
  
 HONOR_BROKER_PRIORITY 選項的變更對於沒有等候要傳送之訊息的新對話或對話將會立即生效。 執行 ALTER DATABASE 時具有等候要傳送之訊息的對話要等到對話的某些訊息傳送以後，才會收取新的設定。 所有對話開始使用新設定之前的時間長短可能會有很大的變化。  
  
 這個屬性的目前設定會在中的 is_broker_priority_honored 資料行中報告[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視。  
  
 **\<snapshot_option >:: =**  
  
 決定交易隔離等級。  
  
 ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
 ON  
 在資料庫層級啟用快照集選項。 啟用時，即使沒有交易使用快照集隔離，DML 陳述式也會開始產生資料列版本。 啟用此選項之後，交易可以指定 SNAPSHOT 交易隔離等級。 當交易執行的隔離等級是 SNAPSHOT 時，所有陳述式都會見到在交易開頭便存在的資料快照集。 如果執行 SNAPSHOT 隔離等級的交易存取多個資料庫中的資料，此時所有資料庫中的 ALLOW_SNAPSHOT_ISOLATION 都必須設為 ON，或是每當 FROM 子句參考 ALLOW_SNAPSHOT_ISOLATION 是 OFF 的資料庫中的資料表時，交易中的每個陳述式都必須使用鎖定提示。  
  
 OFF  
 在資料庫層級關閉快照集選項。 交易無法指定 SNAPSHOT 交易隔離等級。  
  
 當您將 ALLOW_SNAPSHOT_ISOLATION 設為新狀態 (從 ON 設成 OFF，或從 OFF 設成 ON)，認可資料庫中的所有現有交易之前，ALTER DATABASE 並不會將控制權傳回呼叫端。 如果資料庫已在 ALTER DATABASE 陳述式所指定的狀態中，控制權會立即傳回呼叫端。 如果 ALTER DATABASE 陳述式沒有很快傳回，請使用[sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md)以判斷是否有長時間執行的交易。 如果取消了 ALTER DATABASE 陳述式，資料庫會保留在 ALTER DATABASE 啟動時的狀態中。 [Sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視指出資料庫中的快照集隔離交易的狀態。 如果**snapshot_isolation_state_desc** = IN_TRANSITION_TO_ON，ALTER DATABASE ALLOW_SNAPSHOT_ISOLATION OFF 會暫停六秒然後重試此作業。  
  
 如果資料庫是 OFFLINE，您不能變更 ALLOW_SNAPSHOT_ISOLATION 的狀態。  
  
 如果您在 READ_ONLY 資料庫中設定 ALLOW_SNAPSHOT_ISOLATION，資料庫後來又設為 READ_WRITE，這個設定會保留下來。  
  
 您可以變更 master、model、msdb 和 tempdb 等資料庫的 ALLOW_SNAPSHOT_ISOLATION 設定。 如果您變更了 tempdb 的設定，每次停止和重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體時，這個設定會保留下來。 如果您變更模型的設定，除了 tempdb 以外，任何新建資料庫都會以這個設定為預設值。  
  
 依預設，master 和 msdb 資料庫的這個選項是 ON。  
  
 您可以檢查 sys.databases 目錄檢視中的 snapshot_isolation_state 資料行來判斷這個選項目前的設定。  
  
 READ_COMMITTED_SNAPSHOT { ON | OFF }  
 ON  
 在資料庫層級啟用讀取認可快照集選項。 啟用時，即使沒有交易使用快照集隔離，DML 陳述式也會開始產生資料列版本。 啟用此選項之後，指定讀取認可隔離等級的交易即會使用資料列版本設定，而不是鎖定。 在讀取認可之隔離等級執行交易時，所有的陳述式都會看到資料的快照集，就與陳述式開始時所存在的資料一樣。  
  
 OFF  
 在資料庫層級關閉讀取認可快照集選項。 指定 READ COMMITTED 隔離等級的交易會使用鎖定。  
  
 若要設定 READ_COMMITTED_SNAPSHOT ON 或 OFF，除了執行 ALTER DATABASE 命令的連接之外，不能有任何使用中的資料庫連接。 不過，資料庫不一定要處於單一使用者模式。 當資料庫是 OFFLINE 時，您便不能變更這個選項的狀態。  
  
 如果您在 READ_ONLY 資料庫中設定 READ_COMMITTED_SNAPSHOT，當資料庫後來又設為 READ_WRITE 時，這個設定會保留下來。  
  
 master、tempdb 或 msdb 系統資料庫的 READ_COMMITTED_SNAPSHOT 不能設為 ON。 如果您變更 model 的設定，除了 tempdb 以外，這項設定會成為任何新建資料庫的預設值。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_read_committed_snapshot_on 資料行來判斷這個選項目前的設定。  
  
> [!WARNING]  
>  與建立資料表時**DURABILITY = SCHEMA_ONLY**，和**READ_COMMITTED_SNAPSHOT**使用後續變更**ALTER DATABASE**，資料表中的資料將會遺失。  
  
 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT { ON | OFF }  
 **適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 ON  
 當交易隔離等級設為 SNAPSHOT 以下的任何隔離等級時 (例如 READ COMMITTED 或 READ UNCOMMITTED)，記憶體最佳化資料表上之所有解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業都會在 SNAPSHOT 隔離下執行。 不論是在工作階段層級明確設定交易隔離等級，或隱含使用預設值，都會這樣做。  
  
 OFF  
 不會為記憶體最佳化資料表之解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業提高交易隔離等級。  
  
 如果資料庫是 OFFLINE，您不能變更 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT 的狀態。  
  
 此選項預設為 OFF。  
  
 可以檢查來判斷這個選項的目前設定**is_memory_optimized_elevate_to_snapshot_on**中的資料行[sys.databases &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視。  
  
 **\<sql_option >:: =**  
  
 控制資料庫層級的 ANSI 合規性選項。  
  
 ANSI_NULL_DEFAULT { ON | OFF }  
 決定預設值為 NULL 或 NOT NULL 資料行或[CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)的 null 屬性不明確地定義在 CREATE TABLE 或 ALTER TABLE 陳述式。 條件約束所定義的資料行會遵照條件約束規則，不論這個設定為何。  
  
 ON  
 預設值是 NULL。  
  
 OFF  
 預設值是 NOT NULL。  
  
 利用 SET 陳述式來設定的連接層級設定會覆寫 ANSI_NULL_DEFAULT 的預設資料庫層級設定。 根據預設，當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，ODBC 和 OLE DB 用戶端會將工作階段的 ANSI_NULL_DEFAULT 設為 ON 來發出連接層級的 SET 陳述式。 如需詳細資訊，請參閱[SET ANSI_NULL_DFLT_ON &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md).  
  
 對於 ANSI 相容性而言，將資料庫選項 ANSI_NULL_DEFAULT 設為 ON 會將資料庫預設值改成 NULL。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_ansi_null_default_on 資料行或 DATABASEPROPERTYEX 函數的 IsAnsiNullDefault 屬性來判斷這個選項的狀態。  
  
 ANSI_NULLS { ON | OFF }  
 ON  
 所有對於 Null 值的比較，都會得出 UNKNOWN。  
  
 OFF  
 比較非 UNICODE 值和 Null 值，如果兩個值都是 NULL，便會得出 TRUE。  
  
> [!IMPORTANT]  
>  在未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中，ANSI_NULLS 一律為 ON，而且明確將此選項設定為 OFF 的任何應用程式都會產生錯誤。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。  
  
 利用 SET 陳述式來設定的連接層級設定會覆寫 ANSI_NULLS 的預設資料庫設定。 根據預設，當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，ODBC 和 OLE DB 用戶端會將工作階段的 ANSI_NULLS 設為 ON 來發出連接層級的 SET 陳述式。 如需詳細資訊，請參閱 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)。  
  
 當您建立或變更計算資料行索引或索引檢視表時，SET ANSI_NULLS 也必須設為 ON。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_ansi_nulls_on 資料行或 DATABASEPROPERTYEX 函數的 IsAnsiNullsEnabled 屬性來判斷這個選項的狀態。  
  
 ANSI_PADDING { ON | OFF }  
 ON  
 會將字串填補至相同的長度轉換或插入到前**varchar**或**nvarchar**資料型別。  
  
 不會修剪插入 **varchar** 或 **nvarchar** 資料行中的字元值尾端空格及插入 **varbinary** 資料行的二進位值尾端零。 值不會填補到資料行的長度。  
  
 OFF  
 尾端空格**varchar**或**nvarchar**和零**varbinary**會修剪。  
  
 當指定 OFF 時，這個設定只會影響新資料行的定義。  
  
> [!IMPORTANT]  
>  在未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中，ANSI_PADDING 一律為 ON，而且明確將此選項設定為 OFF 的應用程式將會產生錯誤。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 我們建議您一律將 ANSI_PADDING 設為 ON。 當您建立或操作計算資料行索引或索引檢視表時，ANSI_PADDING 也必須是 ON。  
  
 **char (*n*) * * 和**二進位 (*n*) * *，允許當 ANSI_PADDING 設定，將會填補到資料行長度的 null 資料行設為 ON，但當 ANSI_PADDING 是 OFF 時修剪尾端的空格和零。 **char (*n*) * * 和**二進位 (*n*) * * 不允許 null 值的資料行一律會填補到資料行的長度。  
  
 利用 SET 陳述式來設定的連接層級設定會覆寫 ANSI_PADDING 的預設資料庫層級設定。 根據預設，當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，ODBC 和 OLE DB 用戶端會發出連接層級的 SET 陳述式，將工作階段的 ANSI_PADDING 設為 ON。 如需詳細資訊，請參閱 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_ansi_padding_on 資料行或 DATABASEPROPERTYEX 函數的 IsAnsiPaddingEnabled 屬性來判斷這個選項的狀態。  
  
 ANSI_WARNINGS { ON | OFF }  
 ON  
 當發生除以零之類的狀況，或彙總函式中出現 NULL 值時，便會發出錯誤或警告。  
  
 OFF  
 當發生除以零之類的情況時，不會產生警告，但會傳回 NULL 值。  
  
 當您建立或變更計算資料行索引或索引檢視表時，SET ANSI_WARNINGS 必須設為 ON。  
  
 利用 SET 陳述式來設定的連接層級設定會覆寫 ANSI_WARNINGS 的預設資料庫設定。 根據預設，當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，ODBC 和 OLE DB 用戶端會發出連接層級的 SET 陳述式，將工作階段的 ANSI_WARNINGS 設為 ON。 如需詳細資訊，請參閱 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_ansi_warnings_on 資料行或 DATABASEPROPERTYEX 函數的 IsAnsiWarningsEnabled 屬性來判斷這個選項的狀態。  
  
 ARITHABORT { ON | OFF }  
 ON  
 在查詢執行期間，當發生溢位或除以零的錯誤時，查詢會結束。  
  
 OFF  
 當發生這些錯誤之一時，警告訊息會顯示但查詢、批次或交易會繼續處理，如同未發生任何錯誤一樣。  
  
 當您建立或變更計算資料行索引或索引檢視表時，SET ARITHABORT 必須設為 ON。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_arithabort_on 資料行或 DATABASEPROPERTYEX 函數的 IsArithmeticAbortEnabled 屬性來判斷這個選項的狀態。  
  
 COMPATIBILITY_LEVEL { 90 | 100 | 110 | 120}  
 如需詳細資訊，請參閱 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
 CONCAT_NULL_YIELDS_NULL { ON | OFF }   
 ON  
 當任何一個運算元是 NULL 時，串連作業的結果都會是 NULL。 例如，串連字元字串 "This is" 和 NULL 會得出 NULL 值，而不是 "This is" 值。  
  
 OFF  
 將 Null 值當做空的字元字串來處理。  
  
 當您建立或變更計算資料行索引或索引檢視表時，CONCAT_NULL_YIELDS_NULL 也必須設為 ON。  
  
> [!IMPORTANT]  
>  在未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中，CONCAT_NULL_YIELDS_NULL 一律為 ON，而且明確將此選項設定為 OFF 的應用程式將會產生錯誤。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。  
  
 利用 SET 陳述式來設定的連接層級設定會覆寫 CONCAT_NULL_YIELDS_NULL 的預設資料庫設定。 根據預設，當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，ODBC 和 OLE DB 用戶端會發出連接層級的 SET 陳述式，將工作階段的 CONCAT_NULL_YIELDS_NULL 設為 ON。 如需詳細資訊，請參閱 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_concat_null_yields_null_on 資料行，或 DATABASEPROPERTYEX 函數的 IsNullConcat 屬性來判斷這個選項的狀態。  
  
 QUOTED_IDENTIFIER { ON | OFF }   
 ON  
 可以利用雙引號來含括分隔識別碼。  
  
 用雙引號來分隔的所有字串都會解譯為物件識別碼。 附加引號的識別碼不需要遵照 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的識別碼規則。 它們可以是關鍵字，也可以包括 [!INCLUDE[tsql](../../includes/tsql-md.md)] 識別碼通常不接受的字元。 如果單引號 (') 是文字字串的一部分，您可以用雙引號 (") 來表示它。  
  
 OFF  
 識別碼不能放在引號中，且必須遵照所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 識別碼規則。 文字可以用單引號或雙引號來分隔。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也允許用方括號 ([ ]) 來分隔識別碼。 不論 QUOTED_IDENTIFIER 設定為何，用方括號括住的識別項永遠可以使用。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
 當建立資料表時，一律會在資料表的中繼資料中，將 QUOTED IDENTIFIER 選項儲存成 ON，即使建立資料表時將選項設成 OFF，也是如此。  
  
 利用 SET 陳述式來設定的連接層級設定會覆寫 QUOTED_IDENTIFIER 的預設資料庫設定。 根據預設，當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，ODBC 和 OLE DB 用戶端會發出連接層級的 SET 陳述式，將 QUOTED_IDENTIFIER 設為 ON。 如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_quoted_identifier_on 資料行或 DATABASEPROPERTYEX 函數的 IsQuotedIdentifiersEnabled 屬性來判斷這個選項的狀態。  
  
 NUMERIC_ROUNDABORT { ON | OFF }  
 ON  
 當運算式中遺失有效位數時，系統會產生錯誤。  
  
 OFF  
 遺失有效位數並不會產生錯誤訊息，而且結果會捨入到用於儲存結果的資料行或變數的有效位數。  
  
 當您建立或變更計算資料行索引或索引檢視表時，NUMERIC_ROUNDABORT 必須設為 OFF。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_numeric_roundabort_on 資料行或 DATABASEPROPERTYEX 函數的 IsNumericRoundAbortEnabled 屬性來判斷這個選項的狀態。  
  
 RECURSIVE_TRIGGERS { ON | OFF }  
 ON  
 允許遞迴引發 AFTER 觸發程序。  
  
 OFF  
 只禁止直接遞迴引發 AFTER 觸發程序。 AFTER 觸發程序，也停用間接遞迴，請設定 nested 的 triggers 伺服器選項為**0**使用**sp_configure**。  
  
> [!NOTE]  
>  當 RECURSIVE_TRIGGERS 設為 OFF 時，只防止直接遞迴。 若要停用間接遞迴，您也必須將巢狀觸發程序伺服器選項設為 0。  
  
 您可以檢查 sys.databases 目錄檢視中的 is_recursive_triggers_on 資料行或 DATABASEPROPERTYEX 函數的 IsRecursiveTriggersEnabled 屬性來判斷這個選項的狀態。  
  
 **\<target_recovery_time_option >:: =**  
  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 不適用於[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 為每個資料庫指定間接檢查點的頻率。 開頭為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]新資料庫的預設值為 1 分鐘，指示資料庫將會使用間接檢查點。 較舊版本的預設值是 0，表示資料庫將使用自動檢查點，其頻率取決於伺服器執行個體的復原間隔設定。 [!INCLUDE[msCoName](../../includes/msconame-md.md)]建議大多數系統的 1 分鐘。  
  
 TARGET_RECOVERY_TIME **=***target_recovery_time* { SECONDS | MINUTES }  
 *目標復原時間*  
 指定萬一發生損毀時，復原指定之資料庫的時間上限。  
  
 SECONDS  
 指出 *target_recovery_time* 應以秒數表示。  
  
 MINUTES  
 指出 *target_recovery_time* 應以分鐘數表示。  
  
 如需有關間接檢查點的詳細資訊，請參閱[資料庫檢查點 &#40;SQL Server &#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 **與\<終止 >:: =**  
  
 指定資料庫狀態轉換時，何時回復不完整的交易。 如果省略 termination 子句，且資料庫有任何鎖定，ALTER DATABASE 陳述式會無限等待。 只能指定一個 termination 子句，它在 SET 子句之後。  
  
> [!NOTE]  
>  並非所有的資料庫選項都會使用 WITH\<終止 > 子句。 如需詳細資訊，請參閱本主題＜備註＞一節中[設定選項](#SettingOptions) 下的表格。  
  
 ROLLBACK AFTER*整數*[SECONDS] |立即復原  
 指定在指定的秒數之後回復，或是立即回復。  
  
 NO_WAIT  
 指定如果要求的資料庫狀態或選項變更必須等待交易自行認可或回復才可以立即完成，要求將會失敗。  
  
##  <a name="SettingOptions"></a>設定選項  
 若要擷取資料庫選項目前的設定，請使用[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視或[DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)  
  
 設好資料庫選項之後，修改會立即生效。  
  
 若要變更新建資料庫之任何資料庫選項的預設值，請變更 model 資料庫中的適當資料庫選項。  
  
 並非所有的資料庫選項都會使用 WITH\<終止 > 子句，或者指定在結合其他選項。 下表列出這些選項及其選項和終止狀態。  
  
|選項類別目錄|可以搭配其他選項指定|可以使用 WITH\<終止 > 子句|  
|----------------------|-----------------------------------------|---------------------------------------------|  
|\<db_state_option >|是|是|  
|\<db_user_access_option >|是|是|  
|\<db_update_option >|是|是|  
|\<delayed_durability_option >|是|是|  
|\<external_access_option >|是|否|  
|\<cursor_option >|是|否|  
|\<auto_option >|是|否|  
|\<sql_option >|是|否|  
|\<recovery_option >|是|否|  
|\<target_recovery_time_option >|否|是|  
|\<database_mirroring_option >|否|否|  
|ALLOW_SNAPSHOT_ISOLATION|否|否|  
|READ_COMMITTED_SNAPSHOT|否|是|  
|MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT|是|是|  
|\<service_broker_option >|是|否|  
|DATE_CORRELATION_OPTIMIZATION|是|是|  
|\<parameterization_option >|是|是|  
|\<change_tracking_option >|是|是|  
|\<db_encryption >|是|否|  
  
 設定下列其中一個選項，以清除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的計畫快取：  
  
|||  
|-|-|  
|OFFLINE|READ_WRITE|  
|ONLINE|MODIFY FILEGROUP DEFAULT|  
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|  
|COLLATE|MODIFY FILEGROUP READ_ONLY|  
|READ_ONLY||  
  
 在下列情況下也會排清程序快取。  
  
-   資料庫將 AUTO_CLOSE 資料庫選項設定為 ON。 當沒有任何使用者連接參考或使用資料庫時，背景工作嘗試關閉並自動關閉資料庫。  
  
-   您針對有預設選項的資料庫執行幾個查詢。 然後卸除資料庫。  
  
-   卸除來源資料庫的資料庫快照集。  
  
-   您已成功重建資料庫的交易記錄。  
  
-   您還原資料庫備份。  
  
-   您卸離資料庫。  
  
 清除計畫快取會導致重新編譯所有後續執行計畫，而且可能會導致查詢效能突然暫時下降。 針對每次清除計畫快取的快取存放區，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔會包含下列參考訊息：「由於某些資料庫維護或重新設定作業，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 '%s' 快取存放區 (計畫快取的一部分) 發生 %d 次快取存放區排清」。 只要在該時間間隔內快取發生排清，這個訊息就會每五分鐘記錄一次。  
  
## <a name="examples"></a>範例  
  
### <a name="a-setting-options-on-a-database"></a>A. 設定資料庫的選項  
 下列範例會設定 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫的復原模式和資料頁面驗證選項。  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL PAGE_VERIFY CHECKSUM;  
GO  
  
```  
  
### <a name="b-setting-the-database-to-readonly"></a>B. 將資料庫設為 READ_ONLY  
 將資料庫或檔案群組的狀態改成 READ_ONLY 或 READ_WRITE 時，需要資料庫的獨佔存取權。 下列範例會將資料庫設成 `SINGLE_USER` 模式來取得獨佔存取。 之後，範例會將 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的狀態設成 `READ_ONLY`，並將資料庫的存取權還給所有使用者。  
  
> [!NOTE]  
>  這個範例在第一個 `WITH ROLLBACK IMMEDIATE` 陳述式中，使用終止選項 `ALTER DATABASE` 。 所有未完成的交易都會回復，而且 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的任何其他連接都會立即中斷。  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER  
WITH ROLLBACK IMMEDIATE;  
GO  
ALTER DATABASE AdventureWorks2012  
SET READ_ONLY  
GO  
ALTER DATABASE AdventureWorks2012  
SET MULTI_USER;  
GO  
  
```  
  
### <a name="c-enabling-snapshot-isolation-on-a-database"></a>C. 啟用資料庫的快照集隔離  
 下列範例會啟用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的快照集隔離架構選項。  
  
```  
USE AdventureWorks2012;  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
-- Check the state of the snapshot_isolation_framework  
-- in the database.  
SELECT name, snapshot_isolation_state,   
    snapshot_isolation_state_desc AS description  
FROM sys.databases  
WHERE name = N'AdventureWorks2012';  
GO  
  
```  
  
 結果集顯示啟用快照集隔離架構。  
  
 |name |snapshot_isolation_state |description|  
 |-------------------- |------------------------  |----------|  
 |AdventureWorks2012   |1                        | ON |  
  
### <a name="d-enabling-modifying-and-disabling-change-tracking"></a>D. 啟用、修改及停用變更追蹤  
 下列範例會啟用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的變更追蹤，並將保留週期設定為 `2` 天。  
  
```  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(AUTO_CLEANUP = ON, CHANGE_RETENTION = 2 DAYS);  
```  
  
 下列範例會示範如何將保留週期變更為 `3` 天。  
  
```  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING (CHANGE_RETENTION = 3 DAYS);  
```  
  
 下列範例會示範如何停用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的變更追蹤。  
  
```  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF;  
```  
  
### <a name="e-enabling-the-query-store"></a>E. 啟用查詢存放區  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 下列範例會啟用查詢存放區，並設定查詢存放區參數。  
  
```  
ALTER DATABASE AdventureWorks2012  
SET QUERY_STORE = ON   
    (  
      OPERATION_MODE = READ_ONLY   
    , CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 5 )  
    , DATA_FLUSH_INTERVAL_SECONDS = 2000   
    , MAX_STORAGE_SIZE_MB = 10   
    , INTERVAL_LENGTH_MINUTES = 10   
    );  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [ALTER DATABASE 資料庫鏡像 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [統計資料](../../relational-databases/statistics/statistics.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [啟用和停用變更追蹤 &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.data_spaces &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)  
  
  

