---
title: 監視和針對使用量進行記憶體疑難排解 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 7a458b9c-3423-4e24-823d-99573544c877
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 17819c4c2a1d74c8ca4cc5d4875a67c6fb236639
ms.sourcegitcommit: 85a7a532f35b8ea1b45e9a83bfc8529a0abed264
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/11/2019
ms.locfileid: "59480274"
---
# <a name="monitor-and-troubleshoot-memory-usage"></a>監視與疑難排解記憶體使用量
  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] 耗用記憶體的模式與磁碟資料表不同。 您可以使用針對記憶體和記憶體回收子系統提供的 DMV 或效能計數器，監視資料庫中記憶體最佳化資料表和索引所配置和使用的記憶體數量。  如此就能讓您同時深入查看系統和資料庫層級，並且讓您防止因記憶體耗盡而發生問題。  
  
 本主題將涵蓋監視您的 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 記憶體使用量。  
  
  
##  <a name="bkmk_CreateDB"></a> 建立含有記憶體最佳化資料表的範例資料庫  
 如果您的資料庫已包含記憶體最佳化資料表，則可略過本節。  
  
 下列步驟將建立有三個記憶體最佳化資料表的資料庫，方便您在本主題其餘部分中使用。 在此範例中，我們將資料庫對應至資源集區，以便控制記憶體最佳化資料表可以取用的記憶體。  
  
1.  啟動 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]。  
  
2.  按一下 **[新增查詢]**。  
  
3.  將此程式碼貼入新查詢視窗，並執行每一個區段。  
  
    ```  
    -- create a database to be used  
    CREATE DATABASE IMOLTP_DB  
    GO  
  
    ALTER DATABASE IMOLTP_DB ADD FILEGROUP IMOLTP_DB_xtp_fg CONTAINS MEMORY_OPTIMIZED_DATA  
    ALTER DATABASE IMOLTP_DB ADD FILE( NAME = 'IMOLTP_DB_xtp' , FILENAME = 'C:\Data\IMOLTP_DB_xtp') TO FILEGROUP IMOLTP_DB_xtp_fg;  
    GO  
  
    USE IMOLTP_DB  
    GO  
  
    -- create the resoure pool  
    CREATE RESOURCE POOL PoolIMOLTP WITH (MAX_MEMORY_PERCENT = 60);  
    ALTER RESOURCE GOVERNOR RECONFIGURE;  
    GO  
  
    -- bind the database to a resource pool  
    EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'PoolIMOLTP'  
  
    -- you can query the binding using the catalog view as described here  
    SELECT d.database_id  
         , d.name  
         , d.resource_pool_id  
    FROM sys.databases d  
    GO  
  
    -- take database offline/online to finalize the binding to the resource pool  
    USE master  
    GO  
  
    ALTER DATABASE IMOLTP_DB SET OFFLINE  
    GO  
    ALTER DATABASE IMOLTP_DB SET ONLINE  
    GO  
  
    -- create some tables  
    USE IMOLTP_DB  
    GO  
  
    -- create table t1  
    CREATE TABLE dbo.t1 (  
           c1 int NOT NULL CONSTRAINT [pk_t1_c1] PRIMARY KEY NONCLUSTERED  
         , c2 char(40) NOT NULL  
         , c3 char(8000) NOT NULL  
         ) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
    GO  
  
    -- load t1 150K rows  
    DECLARE @i int = 0  
    BEGIN TRAN  
    WHILE (@i <= 150000)  
       BEGIN  
          INSERT t1 VALUES (@i, 'a', replicate ('b', 8000))  
          SET @i += 1;  
       END  
    Commit  
    GO  
  
    -- Create another table, t2  
    CREATE TABLE dbo.t2 (  
           c1 int NOT NULL CONSTRAINT [pk_t2_c1] PRIMARY KEY NONCLUSTERED  
         , c2 char(40) NOT NULL  
         , c3 char(8000) NOT NULL  
         ) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
    GO  
  
    -- Create another table, t3   
    CREATE TABLE dbo.t3 (  
           c1 int NOT NULL CONSTRAINT [pk_t3_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 1000000)  
         , c2 char(40) NOT NULL  
         , c3 char(8000) NOT NULL  
         ) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
    GO  
    ```  
  
##  <a name="monitoring-memory-usage"></a>監視記憶體使用狀況  
  
###  <a name="using-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 隨附內建的標準報表，可用來監視記憶體中資料表耗用的記憶體。 您可以使用物件總管存取這些報表，如 [此處](https://blogs.msdn.com/b/managingsql/archive/2006/05/16/ssms-reports-1.aspx)所述。 您也可以使用物件總管監視個別記憶體最佳化資料表耗用的記憶體。  
  
#### <a name="consumption-at-the-database-level"></a>資料庫層級的耗用量  
 您可以監視資料庫層級的記憶體使用量，如下所述。  
  
1.  啟動 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 並連接到伺服器。  
  
2.  在 [物件總管] 中，以滑鼠右鍵按一下要產生報表的資料庫。  
  
3.  在操作功能表中，依序選取 [報表] -> [標準報表] -> [記憶體最佳化物件的記憶體使用量]  
  
 ![HK_MM_SSMS](../../database-engine/media/hk-mm-ssms-stdrpt-memuse.gif "HK_MM_SSMS")  
  
 此報表會顯示上面所建立資料庫的記憶體耗用量。  
  
 ![HK_MM_SSMS](../../database-engine/media/hk-mm-ssms-stdrpt-memuserpt.gif "HK_MM_SSMS")  
  
###  <a name="using-dmvs"></a>使用 DMVs  
 有許多 DMV 可用來監視記憶體最佳化資料表、索引、系統物件及執行階段結構所耗用的記憶體。  
  
#### <a name="memory-consumption-by-memory-optimized-tables-and-indexes"></a>記憶體最佳化資料表和索引的記憶體耗用量  
 您可以藉由查詢 `sys.dm_db_xtp_table_memory_stats` 找到所有使用者資料表、索引和系統物件的記憶體耗用量，如此處所示。  
  
```sql  
SELECT object_name(object_id) AS Name  
     , *  
   FROM sys.dm_db_xtp_table_memory_stats  
```  
  
 **範例輸出**  
  
```  
Name       object_id   memory_allocated_for_table_kb memory_used_by_table_kb memory_allocated_for_indexes_kb memory_used_by_indexes_kb  
---------- ----------- ----------------------------- ----------------------- ------------------------------- -------------------------  
t3         629577281   0                             0                       128                             0  
t1         565577053   1372928                       1200008                 7872                            1942  
t2         597577167   0                             0                       128                             0  
NULL       -6          0                             0                       2                               2  
NULL       -5          0                             0                       24                              24  
NULL       -4          0                             0                       2                               2  
NULL       -3          0                             0                       2                               2  
NULL       -2          192                           25                      16                              16  
```  
  
 如需詳細資訊，請參閱 < [sys.dm_db_xtp_table_memory_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql?view=sql-server-2016)。  
  
#### <a name="memory-consumption-by-internal-system-structures"></a>內部系統結構的記憶體耗用量  
 系統物件也會耗用記憶體，這些系統物件包括交易式結構、資料和差異檔案的緩衝區、記憶體回收結構等。 您可以藉由查詢 `sys.dm_xtp_system_memory_consumers` 找到這些系統物件所使用的記憶體，如此處所示。  
  
```sql  
SELECT memory_consumer_desc  
     , allocated_bytes/1024 AS allocated_bytes_kb  
     , used_bytes/1024 AS used_bytes_kb  
     , allocation_count  
   FROM sys.dm_xtp_system_memory_consumers  
```  
  
 **範例輸出**  
  
```  
memory_consumer_ desc allocated_bytes_kb   used_bytes_kb        allocation_count  
------------------------- -------------------- -------------------- ----------------  
VARHEAP                   0                    0                    0  
VARHEAP                   384                  0                    0  
DBG_GC_OUTSTANDING_T      64                   64                   910  
ACTIVE_TX_MAP_LOOKAS      0                    0                    0  
RECOVERY_TABLE_CACHE      0                    0                    0  
RECENTLY_USED_ROWS_L      192                  192                  261  
RANGE_CURSOR_LOOKSID      0                    0                    0  
HASH_CURSOR_LOOKASID      128                  128                  455  
SAVEPOINT_LOOKASIDE       0                    0                    0  
PARTIAL_INSERT_SET_L      192                  192                  351  
CONSTRAINT_SET_LOOKA      192                  192                  646  
SAVEPOINT_SET_LOOKAS      0                    0                    0  
WRITE_SET_LOOKASIDE       192                  192                  183  
SCAN_SET_LOOKASIDE        64                   64                   31  
READ_SET_LOOKASIDE        0                    0                    0  
TRANSACTION_LOOKASID      448                  448                  156  
PGPOOL:256K               768                  768                  3  
PGPOOL: 64K               0                    0                    0  
PGPOOL:  4K               0                    0                    0  
```  

 如需詳細資訊，請參閱 [sys.dm_xtp_system_memory_consumers &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md)。  

  
#### <a name="memory-consumption-at-run-time-when-accessing-memory-optimized-tables"></a>存取記憶體最佳化資料表時的執行階段記憶體耗用量  
 您可以使用下列查詢判斷執行階段結構 (例如程序快取) 所耗用的記憶體：執行此查詢可取得執行階段結構 (例如程序快取) 所使用的記憶體。 所有執行階段結構都會加上 XTP 標記。  
  
```sql  
SELECT memory_object_address  
     , pages_in_bytes  
     , bytes_used  
     , type  
   FROM sys.dm_os_memory_objects WHERE type LIKE '%xtp%'  
```  
  
 **範例輸出**  
  
```  
memory_object_address pages_ in_bytes bytes_used type  
--------------------- ------------------- ---------- ----  
0x00000001F1EA8040    507904              NULL       MEMOBJ_XTPDB  
0x00000001F1EAA040    68337664            NULL       MEMOBJ_XTPDB  
0x00000001FD67A040    16384               NULL       MEMOBJ_XTPPROCCACHE  
0x00000001FD68C040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD284040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD302040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD382040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD402040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD482040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD502040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001FD67E040    16384               NULL       MEMOBJ_XTPPROCPARTITIONEDHEAP  
0x00000001F813C040    8192                NULL       MEMOBJ_XTPBLOCKALLOC  
0x00000001F813E040    16842752            NULL       MEMOBJ_XTPBLOCKALLOC  
```  
  
 如需詳細資訊，請參閱 < [sys.dm_os_memory_objects (TRANSACT-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql)。  
  
#### <a name="memory-consumed-by-includehek2includeshek-2-mdmd-engine-across-the-instance"></a>[!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 引擎跨執行個體所耗用的記憶體  
 管理配置給 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 引擎和記憶體最佳化物件之記憶體的方式，與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中其他任何記憶體取用者的管理方式相同。 MEMORYCLERK_XTP 類型的 Clerk 會考量所有配置給 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 引擎的記憶體。 使用下列查詢可找出 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 引擎所使用的所有記憶體。  
  
```sql  
-- this DMV accounts for all memory used by the hek_2 engine  
SELECT type  
     , name  
     , memory_node_id  
     , pages_kb/1024 AS pages_MB   
   FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
 此範例輸出顯示，在配置的總記憶體中，18 MB 為系統層級記憶體耗用量，1358 MB 則配置給資料庫識別碼 5。 由於此資料庫對應至專用資源集區，因此該記憶體會佔用資源集區。  
  
 **範例輸出**  
  
```  
type                 name       memory_node_id pages_MB  
-------------------- ---------- -------------- --------------------  
MEMORYCLERK_XTP      Default    0              18  
MEMORYCLERK_XTP      DB_ID_5    0              1358  
MEMORYCLERK_XTP      Default    64             0  
```  
  
 如需詳細資訊，請參閱 < [sys.dm_os_memory_clerks (TRANSACT-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql)。  
  
##   <a name="managing-memory-consumed-by-memory-optimized-objects"></a>管理記憶體最佳化物件耗用的記憶體  
 您可以藉由將記憶體最佳化資料表繫結至具名資源集區的方式，控制資料表耗用的總記憶體，如 [將包含記憶體最佳化資料表的資料庫繫結至資源集區](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)主題中所述。  
  
##  <a name="troubleshooting-memory-issues"></a>進行記憶體問題疑難排解  
 對記憶體問題進行疑難排解是包含三個步驟的程序：  
  
1.  識別資料庫或執行個體中物件所耗用的記憶體數量。 您可以使用可供記憶體最佳化資料表使用的各種不同監視工具，如前文所述。  例如， `sys.dm_db_xtp_table_memory_stats` 或 `sys.dm_os_memory_clerks`這兩種 DMV。  
  
2.  判斷記憶體耗用量增加的情況，以及您所剩的預留空間。 透過定期監視記憶體耗用量，就可以得知記憶體使用量成長的情況。 例如，如果您已將資料庫對應至具名資源集區，就可以監視效能計數器 Used Memory (KB)，查看記憶體使用量成長的情況。  
  
3.  採取動作消除可能發生的記憶體問題。 如需詳細資訊，請參閱 <<c0> [ 解決記憶體不足問題](resolve-out-of-memory-issues.md)。  
  
## <a name="see-also"></a>另請參閱  
 [將包含記憶體最佳化資料表的資料庫繫結至資源集區](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [變更現有集區上的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#change-min-memory-percent-and-max-memory-percent-on-an-existing-pool)
  
  
