---
title: "SQL Server vNext 的新功能 (Database Engine) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 42f45b23-6509-45e8-8ee7-76a78f99a920
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# SQL Server vNext 的新功能 (Database Engine)
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

**注意：**SQL Server vNext 也包含 SQL Server 2016 Service Pack 中加入的功能。 如需這些項目，請參閱 [SQL Server 2016 (Database Engine) 的新功能](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md)。

## <a name="sql-server-database-engine-ctp-13"></a>SQL Server Database Engine (CTP 1.3)
- 間接檢查點效能的改進。
- 新增無叢集可用性群組的支援。
- 新增最小複本認可可用性群組的設定。
- 可用性群組現在可於 Windows 和 Linux 運作，以進行跨作業系統移轉及測試。
- 新增時態表保留原則的支援，
- 新的 DMV SYS.DM_DB_STATS_HISTOGRAM
- 新增建置及重建線上非叢集資料行存放區索引的支援
- 5 種可傳回 Linux 處理序相關資訊的新動態管理檢視。 如需詳細資訊，請參閱 [Linux 處理序動態管理檢視](../../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md)。   
- 新增 [sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)，以供檢查統計資料。

## <a name="sql-server-database-engine-ctp-12"></a>SQL Server Database Engine (CTP 1.2)

- 隨 SQL Server Management Studio 16.4 版發行的 Database Tuning Advisor (DTA)，在分析 SQL Server 2016 和更新版本時會有額外選項。    
   - 提升效能。 如需詳細資訊，請參閱[使用 Database Engine Tuning Advisor (DTA) 的建議改進效能](../../relational-databases/performance/performance-improvements-using-dta-recommendations.md)。
   - `-fc` 選項可允許資料行存放區索引的建議。 如需詳細資訊，請參閱 [DTA 公用程式](../../tools/dta/dta-utility.md)和 [Database Engine Tuning Advisor (DTA) 中的資料行存放區索引建議](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)。  
   - `-iq` 選項可允許 DTA 檢閱查詢存放區的工作負載。 如需詳細資訊，請參閱[使用查詢存放區的工作負載調整資料庫](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md)。
   

## <a name="sql-server-database-engine-ctp-11"></a>SQL Server Database Engine (CTP 1.1)

<a name="InMemoryBulletsCtp11"/>
- 針對記憶體內功能，記憶體最佳化資料表和原生編譯函式的其他改進如下所列，程式碼範例則可以在[後續段落](#InMemory_CodeSamples)取得：
    - 支援記憶體最佳化資料表中的計算資料行，包括計算資料行的索引。
    - 完整支援原生編譯模組及 CHECK 條件約束中的 JSON 函數。
    - 原生編譯模組中的 `CROSS APPLY` 運算子。   
- 新增了字串函數 [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md)、[TRANSLATE](../../t-sql/functions/translate-transact-sql.md) 及 [TRIM](../../t-sql/functions/trim-transact-sql.md)。   
- [STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md) 函數現在支援 `WITHIN GROUP` 子句。
- 新增了兩種新的日文定序系列 (Japanese_Bushu_Kakusu_140 和 Japanese_XJIS_140)，並新增區分變體選取器 (_VSS) 定序選項供日文定序使用。 如需詳細資料，請參閱[定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)   
- 新的大量存取選項 ([BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 和 [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) ) 能夠從指定為 CSV 格式的檔案直接存取資料，也能透過 [EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) 的新 `BLOB_STORAGE` 選項從儲存在 Azure Blob 儲存體的檔案直接存取資料。


## <a name="sql-server-database-engine-ctp-10"></a>SQL Server Database Engine (CTP 1.0)

- 已加入資料庫 **COMPATIBILITY_LEVEL** 140。   在此層級中執行的客戶會取得最新的語言功能及查詢最佳化工具行為。 這包括每個 Microsoft 發行的發行前版本變更。
- 計算累加統計資料更新臨界值的改善方式 (需要&140; 相容性模式)。
- 已加入 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)。
- 記憶體內部資料表中已加入許多效能和語言增強功能︰
    - 記憶體內部資料表現在支援 `sp_spaceused`。
    - 原生模組現在支援 `sp_rename`。
    - 原生模組現在支援 `CASE` 陳述式。
    - 已移除記憶體內部資料表的 8 個索引限制。
    - 原生模組現在支援 `TOP (N) WITH TIES`。
    - 針對記憶體內部資料表的 `ALTER TABLE` 現在在某些情況下速度大幅提升。
    - 交易重做記憶體內部資料表現在可以平行方式完成。 這可大幅減少執行容錯移轉的時間，或在某些情況下重新啟動。
    - 記憶體內部檢查點檔案現在可以儲存在 Azure 儲存體。 與 LDF 檔案相較，這相當於將功能提供予已有此功能的 MDF。
- 叢集資料行存放區索引現在支援 LOB 資料行 (nvarchar(max)、varchar(max)、varbinary(max))。
- 已新增 [STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md) 彙總函式。  
- 新的權限︰`DATABASE SCOPED CREDENTIAL` 現在是一種安全性實體類別，支援 `CONTROL`、`ALTER`、`REFERENCES`、`TAKE OWNERSHIP` 和 `VIEW DEFINITION` 權限。 限制為 SQL Database 的 `ADMINISTER DATABASE BULK OPERATIONS` 現在可在 `sys.fn_builtin_permissions` 中顯示。   
- 已加入 [Sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md) DMV 以提供 Windows 和 Linux 作業系統資訊。   
- 資料庫角色是使用 R 服務建立，以管理與套件相關聯的權限。 如需詳細資訊，請參閱 [SQL Server 的 R 封裝管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。
 
<a name="InMemory_CodeSamples"/> 
## <a name="code-samples-for-new-in-memory-enhancements"></a>新的記憶體內部改進的程式碼範例

以下子節提供在本文先前段落中，以項目符號列出之記憶體內部新功能的 Transact-SQL 程式碼範例。

記憶體內部的 CTP 1.1 項目符號清單在[這裡](#InMemoryBulletsCtp11)。

#### <a name="computed-column-in-a-memory-optimized-table"></a>記憶體最佳化資料表中的計算資料行

此 CREATE TABLE 陳述式說明先前段落中提到的下列 CTP 1.1 相關功能：

- 資料行上的 JSON 檢查條件約束。
- 新的計算資料行。
- 計算資料行上的索引。

```tsql
CREATE TABLE Product(
    ProductID  int            PRIMARY KEY NONCLUSTERED,
    Name       nvarchar(400)  NOT NULL,
    Price      float,

    Data      nvarchar(4000)  CONSTRAINT [Data contains JSON]  CHECK (ISJSON(Data)=1),

    MadeIn  AS CAST(JSON_VALUE(Data, '$.MadeIn')            as NVARCHAR(50)) PERSISTED,
    Cost    AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float       ),

    INDEX [idx_Product_MadeIn] NONCLUSTERED (MadeIn)
)
        WITH (MEMORY_OPTIMIZED=ON);
```

#### <a name="cross-apply-and-json-functions"></a>CROSS APPLY 和 JSON 函數

此 CREATE PROCEDURE 陳述式 (針對原生編譯預存程序) 說明先前段落中提到的下列 CTP 1.1 相關功能：

- CROSS APPLY 運算子。
- JSON 函數。

```tsql
CREATE OR ALTER PROCEDURE ProductList()
    WITH SCHEMABINDING, NATIVE_COMPILATION
as begin
    atomic with (transaction isolation level = snapshot,  language = N'English')

    SELECT
            ProductID, Name, Price, Tags,
            Data,
            JSON_VALUE(Data,'$.MadeIn') AS MadeIn,
            value
        FROM Product
        CROSS APPLY OPENJSON(Data, '$.SalesReasons')
        FOR JSON PATH
end;
```
