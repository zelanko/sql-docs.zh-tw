---
title: tempdb 資料庫 | Microsoft Docs
description: 本主題提供有關在 SQL Server 和 Azure SQL Database 中設定和使用 tempdb 資料庫的詳細資料
ms.custom: P360
ms.date: 08/21/2019
ms.prod: sql
ms.prod_service: database-engine
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
ms.reviewer: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 76fb1dcfaab16e560b67f92d7bc3a6203f93037b
ms.sourcegitcommit: 4c7151f9f3f341f8eae70cb2945f3732ddba54af
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/27/2019
ms.locfileid: "71326111"
---
# <a name="tempdb-database"></a>tempdb 資料庫

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

**tempdb** 系統資料庫是全域資源，適用於所有連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體或 SQL Database 的使用者。 Tempdb 用以保留：  
  
- 明確建立的暫存「使用者物件」  (例如：全域或本機暫存資料表與索引、暫存預存程序、資料表變數、資料表值函式中傳回的資料表，或資料指標)。  
- 資料庫引擎建立的**內部物件**。 其中包括：
  - 用來儲存多工緩衝處理、資料指標、排序和暫存大型物件 (LOB) 儲存體中繼結果的工作資料表。
  - 用於雜湊聯結或雜湊彙總作業的工作檔案。
  - 如建立或重建索引之類的作業 (若有指定 SORT_IN_TEMPDB) 或特定 GROUP BY、ORDER BY 或 UNION 查詢的中繼排序結果。

  > [!NOTE]
  > 每個內部物件至少使用 9 頁、一個 IAM 頁面和一個八頁的範圍。 如需分頁與範圍的詳細資訊，請參閱[分頁與範圍](../../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents)。
  > [!IMPORTANT]
  > Azure SQL Database 單一資料庫和彈性集區支援儲存在 tempdb 中，只限於資料庫層級的全域暫存資料表和全域暫存預存程序。 在同一 Azure SQL 資料庫中的所有使用者工作階段，會共用全域暫存資料表和全域暫存預存程序。 其他 Azure SQL 資料庫的使用者工作階段無法存取全域暫存資料表。 如需詳細資訊，請參閱[限定資料庫範圍的全域暫存資料表 (Azure SQL Database)](../../t-sql/statements/create-table-transact-sql.md#database-scoped-global-temporary-tables-azure-sql-database)。 [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) 與 SQL Server 支援相同的暫存物件。
  > 針對 Azure SQL Database 單一資料庫和彈性集區，只會套用 master 資料庫和 tempdb 資料庫。 如需詳細資訊，請參閱[什麼是 Azure SQL Database 伺服器](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-database-server)。 如需 Azure SQL Database 單一資料庫和彈性集區內容中 tempdb 的討論，請參閱 [Azure SQL Database 單一資料庫和彈性集區中的 tempdb 資料庫](#tempdb-database-in-sql-database)。 針對 Azure SQL Database 受控執行個體，則會套用所有系統資料庫。

- 「版本存放區」  是保存資料列的資料頁集合；這些資料列是支援使用資料列版本設定功能的必要項目。 版本存放區有兩個：一個是一般版本存放區，一個是線上索引建立版本存放區。 版本存放區包含：
  - 由資料庫中的資料修改交易所產生的資料列版本，該資料庫採用使用資料列版本設定隔離的讀取認可或快照集隔離交易。  
  - 由以下這類功能的資料修改交易所產生的資料列版本：線上索引作業、Multiple Active Result Set (MARS) 和 AFTER 觸發程序。  
  
至少會記錄 **tempdb** 內的作業，以便回復交易。 每次啟動**時都會重新建立** tempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，這樣系統永遠會以乾淨的資料庫複本啟動。 連接中斷時會自動卸除暫存資料表與預存程序，且系統關閉時所有連接都會停止。 因此， **tempdb** 中的任何資料都不會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一個工作階段儲存到其他的工作階段。 **tempdb**不允許進行備份和還原作業。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="physical-properties-of-tempdb-in-sql-server"></a>SQL Server 中的 tempdb 實體屬性

下表列出 SQL Server 中的 **tempdb** 資料和記錄檔的初始設定值，其是以 Model 資料庫的預設值為依據。 對於不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這些檔案的大小稍有不同。  
  
|檔案|邏輯名稱|實體名稱|初始大小|檔案成長|  
|----------|------------------|-------------------|------------------|-----------------|  
|主要資料|tempdev|tempdb.mdf|8 MB|自動成長 64 KB，直到磁碟滿了為止|  
|次要資料檔*|temp#|tempdb_mssql_#.ndf|8 MB|自動成長 64 KB，直到磁碟滿了為止|  
|Log|templog|templog.ldf|8 MB|自動成長 64 MB，最大至 2 TB。|  
  
\* 檔案數目取決於電腦上 (邏輯) 處理器的數量。 一般而言，如果邏輯處理器的數目小於或等於 8，請使用與邏輯處理器數目相同的資料檔案數目。 如果邏輯處理器的數目大於 8，請使用 8 個資料檔案，要是競爭的情況仍持續發生，請以 4 的倍數增加資料檔案數目，直到競爭縮減到可接受的程度；或是對工作負載/程式碼進行變更。

> [!NOTE]
> 資料檔案數目預設值取決於 [KB 2154845](https://support.microsoft.com/kb/2154845/)內的一般指導方針。  
  
### <a name="moving-the-tempdb-data-and-log-files-in-sql-server"></a>移動 SQL Server 中的 tempdb 資料和記錄檔

若要移動 **tempdb** 資料和記錄檔，請參閱 [移動系統資料庫](../../relational-databases/databases/move-system-databases.md)。  
  
### <a name="database-options-for-tempdb-in-sql-server"></a>SQL Server 中的 tempdb 資料庫選項

下表列出 **tempdb** 資料庫中每個資料庫選項的預設值，以及這些選項是否可以修改。 若要檢視這些選項目前的設定，請參閱 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 目錄檢視。  
  
|資料庫選項|預設值|可以修改|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|是|  
|ANSI_NULL_DEFAULT|OFF|是|  
|ANSI_NULLS|OFF|是|  
|ANSI_PADDING|OFF|是|  
|ANSI_WARNINGS|OFF|是|  
|ARITHABORT|OFF|是|  
|AUTO_CLOSE|OFF|否|  
|AUTO_CREATE_STATISTICS|ON|是|  
|AUTO_SHRINK|OFF|否|  
|AUTO_UPDATE_STATISTICS|ON|是|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|是|  
|CHANGE_TRACKING|OFF|否|  
|CONCAT_NULL_YIELDS_NULL|OFF|是|  
|CURSOR_CLOSE_ON_COMMIT|OFF|是|  
|CURSOR_DEFAULT|GLOBAL|是|  
|資料庫可用性選項|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|否<br /><br /> 否<br /><br /> 否|  
|DATE_CORRELATION_OPTIMIZATION|OFF|是|  
|DB_CHAINING|ON|否|  
|ENCRYPTION|OFF|否|  
|MIXED_PAGE_ALLOCATION|OFF|否|  
|NUMERIC_ROUNDABORT|OFF|是|  
|PAGE_VERIFY|CHECKSUM (新安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。<br /><br /> NONE (升級的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。|是|  
|PARAMETERIZATION|SIMPLE|是|  
|QUOTED_IDENTIFIER|OFF|是|  
|READ_COMMITTED_SNAPSHOT|OFF|否|  
|RECOVERY|SIMPLE|否|  
|RECURSIVE_TRIGGERS|OFF|是|  
|Service Broker 選項|ENABLE_BROKER|是|  
|TRUSTWORTHY|OFF|否|  
  
如需這些資料庫選項的描述，請參閱 [ALTER DATABASE SET 選項 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)。  
  
## <a name="tempdb-database-in-sql-database"></a>SQL Database 中的 tempdb 資料庫

### <a name="tempdb-sizes-for-dtu-based-service-tiers"></a>以 DTU 為基礎的服務層 tempdb 大小

|SLO|Tempdb 資料檔案大小上限 (GB)|Tempdb資料檔案數|Tempdb 資料檔案大小上限 (GB)|
|---|---:|---:|---:|
|[基本]|13|1|13|
|S0|13|1|13|
|S1|13|1|13|
|S2|13|1|13|
|S3|32|1|32
|S4|32|2|64|
|S6|32|3|96|
|S7|32|6|192|
|S9|32|12|384|
|S12|32|12|384|
|P1|13|12|156|
|P2|13|12|156|
|P4|13|12|156|
|P6|13|12|156|
|P11|13|12|156|
|P15|13|12|156|
|Premium 彈性集區 (所有 DTU 設定)|13|12|156|
|標準彈性集區 (S0-S2)|13|12|156|
|標準彈性集區 (S3 以上) |32|12|384|
|基本彈性集區 (所有 DTU 設定)|13|12|156|
||||

### <a name="tempdb-sizes-for-vcore-based-service-tiers"></a>以 vCore 為基礎的服務層 tempdb 大小

請參閱[以 vCore 為基礎的資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits)

## <a name="restrictions"></a>限制

下列作業不能在 **tempdb** 資料庫上執行：  
  
- 新增檔案群組
- 備份或還原資料庫
- 變更定序。 預設定序是伺服器定序
- 變更資料庫擁有者。 **tempdb** 是由 **sa** 所擁有
- 建立資料庫快照集
- 卸除資料庫
- 從資料庫卸除 **guest** 使用者
- 啟用異動資料擷取
- 參與資料庫鏡像
- 移除主要檔案群組、主要資料檔案或記錄檔
- 重新命名資料庫或主要檔案群組
- 執行 DBCC CHECKALLOC
- 執行 DBCC CHECKCATALOG
- 將資料庫設定為 OFFLINE
- 將資料庫或主要檔案群組設定為 READ_ONLY
  
## <a name="permissions"></a>權限

任何使用者都可以在 tempdb 中建立暫時物件。 除非收到其他權限，否則使用者只能存取自己的物件。 您可以撤銷 tempdb 的連線權限來阻止使用者使用 tempdb，不過不建議您這樣做，因為有些常式作業需要使用 tempdb。  

## <a name="optimizing-tempdb-performance-in-sql-server"></a>最佳化 SQL Server 中的 tempdb 效能

tempdb 資料庫的大小和實體位置會影響系統效能。 例如，如果為 tempdb 定義的大小太小，每次您重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時，部分系統處理負載可能會開始將 tempdb 自動成長到支援工作負載所需的大小。

可能的話，請使用[資料庫檔案立即初始化](../../relational-databases/databases/database-instant-file-initialization.md)來改善資料檔案成長作業的效能。

您可將檔案大小設定為夠大的值來容納環境中的典型工作負載，藉此為所有 tempdb 檔案預先配置空間。 預先配置可防止 tempdb 擴充過於頻繁而影響效能。 tempdb 資料庫應該設為自動成長，但這應該用來增加非計畫中例外狀況的磁碟空間。

由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的比例填入演算法較偏好可用空間多的檔案配置，因此每個[檔案群組](../../relational-databases/databases/database-files-and-filegroups.md#filegroups)內的資料檔應該大小相同。 將 tempdb 分割成相同大小的多個資料檔案時，可讓使用 tempdb 的作業具有較高的平行效率。

將檔案成長增量設成合理的大小，可避免 tempdb 資料庫檔案每次成長量的值太小。 如果檔案的成長比寫入 tempdb 的資料量少太多，那麼 tempdb 可能必須經常擴大並影響效能。

若要檢查目前的 tempdb 大小和成長參數，請使用下列查詢：

```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeInMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
        ELSE 'Log file grows to a maximum size of 2 TB.'
    END,
    growth AS 'GrowthValue',
    'GrowthIncrement' =
        CASE
            WHEN growth = 0 THEN 'Size is fixed.'
            WHEN growth > 0 AND is_percent_growth = 0
                THEN 'Growth value is in 8-KB pages.'
            ELSE 'Growth value is a percentage.'
        END
FROM tempdb.sys.database_files;
GO
```

將 tempdb 資料庫放在快速的 I/O 子系統上。 如果有許多直接連接的磁碟，請使用磁碟條狀配置。 除非您發生 I/O 瓶頸，否則一或多個 tempdb 資料檔案不一定要在不同的磁碟或主軸上。

將 tempdb 資料庫放在不同於使用者資料庫所使用的磁碟上。

## <a name="performance-improvements-in-tempdb-for-sql-server"></a>SQL Server 中的 tempdb 效能改善

從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 開始，**tempdb** 效能已針對下列各方面進一步最佳化：  
  
- 系統會快取暫存資料表和資料表變數。 快取允許卸除和建立暫存物件以極快速度執行的作業，並減少頁面配置競爭。  
- 已改善配置頁面閂鎖通訊協定，減少所使用的 UP (更新) 閂鎖數量。  
- **tempdb** 的記錄負荷已縮減，以降低 **tempdb** 記錄檔的磁碟 I/O 頻寬耗用量。  
- 安裝程式會在新的執行個體安裝期間加入多個 tempdb 資料檔案。 可使用 [資料庫引擎設定]  區段上的新 UI 輸入控制項和命令列參數 /SQLTEMPDBFILECOUNT 完成此工作。 根據預設，安裝程式會新增與邏輯處理器計數一樣多的 tempdb 資料檔案 (或是 8 個)，以較低者為準。  
- 如果有多個 **tempdb** 資料檔案，則視成長設定而定，所有的檔案會都同時以相同數量自動成長。 不再需要追蹤旗標 1117。  
- **tempdb** 中的所有配置都使用統一範圍。 不再需要[追蹤旗標 1118](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。  
- 主要檔案群組中，已開啟 AUTOGROW_ALL_FILES 屬性而且此屬性無法修改。

如需 tempdb 中效能改進的詳細資訊，請參閱下列部落格文章：

[TEMPDB - 檔案與追蹤旗標及更新，太棒了！](https://blogs.msdn.microsoft.com/sql_server_team/tempdb-files-and-trace-flags-and-updates-oh-my/)

## <a name="memory-optimized-tempdb-metadata"></a>記憶體最佳化的 TempDB 中繼資料

TempDB 中繼資料競爭一直以來都是在 SQL Server 上執行之許多工作負載的延展性瓶頸。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 引進的新功能是[記憶體內部資料庫](../in-memory-database.md)功能系列的一部分，記憶體最佳化的 tempdb 中繼資料能有效移除此瓶頸，並解除鎖定大量 tempdb 工作負載的新層級延展性。 在 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 中，涉及管理暫存資料表中繼資料的系統資料表，可以移至不需閂鎖之非持久性經記憶體最佳化的資料表。  [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 引進的新功能是[記憶體內部資料庫](../in-memory-database.md)功能系列的一部分，記憶體最佳化的 tempdb 中繼資料能有效移除此瓶頸，並解除鎖定大量 tempdb 工作負載的新層級延展性。 在 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 中，涉及管理暫存資料表中繼資料的系統資料表，可以移至不需閂鎖之非持久性經記憶體最佳化的資料表。若要選擇加入此功能，請使用下列指令碼：

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON 
```

這項設定變更需要重新啟動服務才會生效。

此實作有些限制請務必注意：

1. 功能開關切換不是動態的。 因為內部變更需要作用於 tempdb 的結構，所以啟用或停用此功能都必須重新開機。
2. 單筆交易不一定會存取多個資料庫中經記憶體最佳化的資料表。  這表示任何牽涉到使用者資料庫中經記憶體最佳化之資料表的交易，都不能存取相同交易中的 TempDB 系統檢視表。  如果您嘗試存取和使用者資料庫中經記憶體最佳化的資料表同一交易中的 TempDB 系統檢視表，您會收到下列錯誤：
    ```
    A user transaction that accesses memory optimized tables or natively compiled modules cannot access more than one user database or databases model and msdb, and it cannot write to master.
    ```
    範例
    ```
    BEGIN TRAN
    SELECT *
    FROM tempdb.sys.tables  -----> Creates a user In-Memory OLTP Transaction on Tempdb
    INSERT INTO <user database>.<schema>.<mem-optimized table>
    VALUES (1)  ----> Attempts to create user In-Memory OLTP transaction but will fail
    COMMIT TRAN
    ```
3. 針對經記憶體最佳化之資料表的查詢不支援鎖定和隔離提示，因此針對經記憶體最佳化之 TempDB 目錄檢視的查詢不支援鎖定和隔離提示。 至於 SQL Server 中的其他系統目錄檢視，針對系統檢視表的所有交易都會是 READ COMMITTED 隔離 (或在本例中為 READ COMMITTED SNAPSHOT)。
4. 啟用經記憶體最佳化的 tempdb 中繼資料時，無法在暫存資料表上建立[資料行存放區索引](../indexes/columnstore-indexes-overview.md)。

> [!NOTE] 
> 這些限制僅適用於參考 TempDB 系統檢視表時，如有需要，您可在存取使用者資料庫中經記憶體最佳化的資料表時，在相同的交易中建立暫存資料表。

您可以使用下列 T-SQL 命令驗證 TempDB 是否經記憶體最佳化：
```
SELECT SERVERPROPERTY('IsTempdbMetadataMemoryOptimized')
```

若伺服器在啟用經記憶體最佳化的 TempDB 中繼資料後因為任何原因而無法啟動，您可以使用 **-f** 啟動選項，以[最小組態](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md)啟動 SQL Server 來略過功能。 這可以讓您停用功能，然後以一般模式重新啟動 SQL Server。

## <a name="capacity-planning-for-tempdb-in-sql-server"></a>SQL Server 中的 tempdb 容量規劃

在決定 SQL Server 生產環境中的 tempdb 適當大小時，您需要考量許多因素。 如本文先前所述，這些因素包括現有的工作負載和使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 我們建議您在 SQL Server 測試環境中執行下列工作來分析現有的工作負載：

- 將 tempdb 的自動成長設為開啟。
- 執行個別查詢或工作負載追蹤檔案，並監視 tempdb 空間使用量。
- 執行索引維護作業 (例如重建索引)，並監視 tempdb 空間。
- 使用先前步驟中的空間使用值來預測總工作負載使用量；針對預定的並行活動調整此值，然後據此設定 tempdb 的大小。

## <a name="how-to-monitor-tempdb-use"></a>如何監視 tempdb 使用量

一旦 tempdb 的磁碟空間用完，會造成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生產環境嚴重中斷，並使執行中的應用程式無法完成作業。 您可以使用 [sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) 動態管理檢視來監視 tempdb 檔案中所使用的磁碟空間：

```sql
 -- Determining the Amount of Free Space in tempdb
SELECT SUM(unallocated_extent_page_count) AS [free pages],
  (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount Space Used by the Version Store
SELECT SUM(version_store_reserved_page_count) AS [version store pages used],
  (SUM(version_store_reserved_page_count)*1.0/128) AS [version store space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by Internal Objects
SELECT SUM(internal_object_reserved_page_count) AS [internal object pages used],
  (SUM(internal_object_reserved_page_count)*1.0/128) AS [internal object space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by User Objects
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],
  (SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]
FROM sys.dm_db_file_space_usage;
 ```

此外，若要在工作階段或工作層級監視 tempdb 中的頁面配置或取消配置活動，您可以使用 [sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) 和 [sys.dm_db_task_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md) 動態管理檢視。 這些檢視可用來識別大量佔用 tempdb 磁碟空間的大型查詢、暫存資料表或資料表變數。 您還可以使用若干計數器來監視 tempdb 可用的空間以及有哪些資源正在使用 tempdb。 如需詳細資訊，請參閱下一節。

```sql
-- Obtaining the space consumed by internal objects in all currently running tasks in each session
SELECT session_id,
  SUM(internal_objects_alloc_page_count) AS task_internal_objects_alloc_page_count,
  SUM(internal_objects_dealloc_page_count) AS task_internal_objects_dealloc_page_count
FROM sys.dm_db_task_space_usage
GROUP BY session_id;

-- Obtaining the space consumed by internal objects in the current session for both running and completed tasks
SELECT R2.session_id,
  R1.internal_objects_alloc_page_count
  + SUM(R2.internal_objects_alloc_page_count) AS session_internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count
  + SUM(R2.internal_objects_dealloc_page_count) AS session_internal_objects_dealloc_page_count
FROM sys.dm_db_session_space_usage AS R1
INNER JOIN sys.dm_db_task_space_usage AS R2 ON R1.session_id = R2.session_id
GROUP BY R2.session_id, R1.internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count;;
```

## <a name="related-content"></a>相關內容

- [索引的 SORT_IN_TEMPDB 選項](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)  
- [系統資料庫](../../relational-databases/databases/system-databases.md)  
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
- [移動資料庫檔案](../../relational-databases/databases/move-database-files.md)  
  
