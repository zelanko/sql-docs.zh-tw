---
title: 資料行存放區索引 - 重組 | Microsoft 文件
ms.custom: ''
ms.date: 01/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d3efda1a-7bdb-47f5-80bf-f075329edee5
caps.latest.revision: 17
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: b6db5cb32bcde96a49981e76817a0948c19473fc
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39537198"
---
# <a name="columnstore-indexes---defragmentation"></a>資料行存放區索引 - 重組
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  重組資料行存放區索引的工作。  
  
## <a name="use-alter-index-reorganize-to-defragment-a-columnstore-index-online"></a>使用 ALTER INDEX REORGANIZE 線上重組資料行存放區索引  
 **適用於：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開頭為 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])、[!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
執行任何類型的負載後，您在差異存放區中可能有多個小型的資料列群組。 您可使用 `ALTER INDEX REORGANIZE` 強制將所有資料列群組存放至資料行存放區，然後再將資料列群組合併成較少資料列的資料列群組。  重新組織作業也會移除已從資料行存放區刪除的資料列。  
  
如需詳細資訊，請參閱以下 SQL Database 引擎小組部落格的部落格文章。  
-   [將資料行存放區索引中的索引片段最小化](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)  
-   [資料行存放區索引和適用於資料列群組的合併原則](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)  
  
### <a name="recommendations-for-reorganizing"></a>對重新組織的建議  
在一次或多次資料載入後重新組織資料行存放區索引，以便盡快獲得查詢效能的優勢。 進行重新組織一開始會需要額外的 CPU 資源來壓縮資料，這可能會拖慢整體系統效能。 不過，只要資料壓縮完成，查詢效能就能獲得改善。  
  
使用 [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md) 中的範例計算分散。 這可協助您判斷是否需要執行 REORGANIZE 作業。  
  
### <a name="example-how-reorganizing-works"></a>範例︰重新組織的運作方式  
 本範例展示 ALTER INDEX REORGANIZE 如何將所有差異存放區資料列群組強制放置於資料行存放區，然後再將資料列群組合併。  
  
1.  執行此 Transact-SQL，建立包含 300,000 個資料列的暫存表格。 我們將使用此暫存表格大量載入資料列至資料行存放區索引中。  
  
    ```sql  
    USE master;  
    GO  
  
    IF EXISTS (SELECT name FROM sys.databases  
        WHERE name = N'[columnstore]')  
        DROP DATABASE [columnstore];  
    GO  
  
    CREATE DATABASE [columnstore];  
    GO  
  
    IF EXISTS (SELECT name FROM sys.tables  
        WHERE name = N'staging'  
        AND object_id = OBJECT_ID (N'staging'))  
    DROP TABLE dbo.staging;  
    GO  
  
    CREATE TABLE [staging] (  
         AccountKey int NOT NULL,  
         AccountDescription nvarchar (50),  
         AccountType nvarchar(50),  
         AccountCodeAlternateKey int  
    );  
    GO  
  
    -- Load data  
    DECLARE @loop int;  
    DECLARE @AccountDescription varchar(50);  
    DECLARE @AccountKey int;  
    DECLARE @AccountType varchar(50);  
    DECLARE @AccountCode int;  
  
    SELECT @loop = 0;  
    BEGIN TRAN  
        WHILE (@loop < 300000)   
          BEGIN  
            SELECT @AccountKey = CAST (RAND()*10000000 AS int);  
            SELECT @AccountDescription = 'accountdesc ' + CONVERT(varchar(20), @AccountKey);  
            SELECT @AccountType = 'AccountType ' + CONVERT(varchar(20), @AccountKey);  
            SELECT @AccountCode =  CAST (RAND()*10000000 AS int);  
  
            INSERT INTO staging VALUES (  
               @AccountKey,   
               @AccountDescription,   
               @AccountType,   
               @AccountCode  
            );  
  
            SELECT @loop = @loop + 1;  
          END  
    COMMIT  
    ```  
  
2.  建立資料表儲存為資料行存放區。  
  
    ```sql  
    IF EXISTS (SELECT name FROM sys.tables  
        WHERE name = N'cci_target'  
        AND object_id = OBJECT_ID (N'cci_target'))  
    DROP TABLE dbo.cci_target;  
    GO  
  
    -- Create a table with a clustered columnstore index  
    -- and the same columns as the rowstore staging table.  
    CREATE TABLE cci_target (  
         AccountKey int NOT NULL,  
         AccountDescription nvarchar (50),  
         AccountType nvarchar(50),  
         AccountCodeAlternateKey int,  
         INDEX idx_cci_target CLUSTERED COLUMNSTORE  
    )  
    GO  
    ```  
  
3.  將暫存表格資料列大量插入至資料行存放區資料表。 `INSERT INTO ... SELECT` 執行大量插入。 `TABLOCK` 允許 `INSERT` 以平行處理原則執行。  
  
    ```sql  
    -- Insert rows in parallel  
    INSERT INTO cci_target WITH (TABLOCK)  
    SELECT TOP (300000) * FROM staging;  
    GO  
    ```  
  
4.  使用 *sys.dm_db_column_store_row_group_physical_stats* 動態管理檢視 (DMV) 檢視資料列群組。  
  
    ```sql  
    -- Run this dynamic management view (DMV) to see the OPEN rowgroups.   
    -- The number of rowgroups depends on the degree of parallelism.   
    -- You will see multiple OPEN rowgroups depending on the degree of parallelism.   
    -- This is because insert operation can run in parallel in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     在此範例中，結果會顯示 8 個 OPEN 資料列群組，其各有 37,500 個資料列。 OPEN 資料列群組的數目，取決於 *max_degree_of_parallelism* 設定。  
  
     ![OPEN 資料列群組](../../relational-databases/indexes/media/cci-openrowgroups.png "OPEN 資料列群組")  
  
5.  使用 `ALTER INDEX REORGANIZE` 搭配 `COMPRESS_ALL_ROW_GROUPS` 選項可強制將所有資料列群組壓縮至資料行存放區中。  
  
    ```sql  
    -- This command will force all CLOSED and OPEN rowgroups into the columnstore.  
    ALTER INDEX idx_cci_target ON cci_target   
    REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     結果會顯示 8 個 COMPRESSED 資料列群組以及 8 個 TOMBSTONE 資料列群組。 每個資料列群組皆會壓縮至資料行存放區而無關其大小。 系統將會移除 TOMBSTONE 資料列群組。  
  
     ![TOMBSTONE 和 COMPRESSED 資料列群組](../../relational-databases/indexes/media/cci-tombstone-compressed-rowgroups.png "TOMBSTONE 和 COMPRESSED 資料列群組")  
  
6.  針對查詢效能考量，建議您合併所有的小型資料列群組。 `ALTER INDEX REORGANIZE` 會將 `COMPRESSED` 資料列群組結合在一起。 將差異資料列群組壓縮至資料行存放區後，再次執行 ALTER INDEX REORGANIZE 以合併所有的小型 COMPRESSED 資料列群組。 此時，您不需要 `COMPRESS_ALL_ROW_GROUPS` 選項。  
  
    ```sql  
    -- Run this again and you will see that smaller rowgroups   
    -- combined into one compressed rowgroup with 300,000 rows  
    ALTER INDEX idx_cci_target ON cci_target REORGANIZE;  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     結果會顯示現已壓縮為單一 COMPRESSED 資料列群組的 8 個 COMPRESSED 資料列群組。  
  
     ![合併的資料列群組](../../relational-databases/indexes/media/cci-compressed-rowgroups.png "合併的資料列群組")  
  
## <a name="rebuild"></a> 使用 ALTER INDEX REBUILD 離線重組資料行存放區索引  
 若為 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 和更新版本，則通常無須重建資料行存放區索引，這是因為 `REORGANIZE` 會在背景以線上作業方式執行必要的重建作業。  
  
 重建資料行存放區索引會移除分散的片段，並將所有資料列移至資料行存放區。 使用 [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md) 或 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) 完整重建現有的叢集資料行存放區索引。 此外，您可以使用 ALTER INDEX... REBUILD 重建特定分割區。  
  
### <a name="rebuild-process"></a>重建程序  
 為了重建資料行存放區索引， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會進行以下作業：  
  
1.  在進行重建時，取得資料表或分割區上的獨佔鎖定。 在重建期間，資料處於「離線」狀態而且無法使用，即使使用 `NOLOCK`、RCSI 或 SI 亦然。  
  
2.  將所有資料重新壓縮到資料行存放區。 當重建進行時，有兩個資料行存放區索引複本存在。 當重建完成時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會刪除原始資料行存放區索引。  
  
### <a name="recommendations-for-rebuilding-a-columnstore-index"></a>重建資料行存放區索引的建議  
 重建資料行存放區索引對於移除片段以及將所有資料列移入資料行存放區而言相當實用。 以下是我們的建議：  
  
1.  重建分割區，而非整份資料表。  
    -   如果索引很大，重建整個資料表將花上很長的時間，而且需要足夠的磁碟空間來存放重建期間額外的索引副本。 通常只需要重建最近使用的分割區。  
    -   對於資料分割資料表，您不需要重建整個資料行存放區索引，因為片段可能只會出現在最近修改過的分割區中。 事實資料表和大型維度資料表通常會進行分割區，以便在資料表區塊上執行備份和管理作業。  

2.  在繁重的 DML 作業之後重建分割區。  
    -   重建分割區將會重組分割區並減少磁碟儲存體。 重建將會刪除資料行存放區中所有標示為刪除的資料列，並且將所有資料列群組從差異存放區移至資料行存放區。 請注意，在差異存放區中可能存有資料列數量小於 1 百萬個的多個資料列群組。  
  
3.  載入資料後重建分割區。  
    -   如此可確保所有資料都儲存在資料行存放區中。 同時處理將不到 100 萬個資料列載入至相同分割區的每項作業時，分割區最後會具有多個差異存放區。 重建會將所有差異存放區資料列移至資料行存放區。  

## <a name="automatic-index-and-statistics-management"></a>自動索引與統計資料管理

利用[自適性索引重組](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)等解決方案，為一或多個資料庫自動管理索引重組以及統計資料更新。 這項程序會根據索引分散程度與其他參數，自動選擇要進行重建或是重新組織索引，並以線性閾值更新統計資料。

## <a name="see-also"></a>另請參閱        
[資料行存放區索引 - 新功能](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)    
[資料行存放區索引效能](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
[開始使用資料行存放區進行即時作業分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
[資料倉儲的資料行存放區索引](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
[資料行存放區索引架構](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)    
[自適性索引重組](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)    
  
  
