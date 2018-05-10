---
title: 將包含記憶體最佳化資料表的資料庫繫結至資源集區 | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f222b1d5-d2fa-4269-8294-4575a0e78636
caps.latest.revision: 24
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6043007d25a6e8cfe692926f4dd7f08b1ad19c10
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="bind-a-database-with-memory-optimized-tables-to-a-resource-pool"></a>將包含記憶體最佳化資料表的資料庫繫結至資源集區
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  資源集區代表可受管制的實體資源子集。 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫會繫結至預設資源集區並取用其資源。 為了防止一個或多個記憶體最佳化資料表取用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有資源，以及避免其他記憶體使用者耗用記憶體最佳化資料表所需的記憶體，您應該針對具有記憶體最佳化資料表的資料庫建立另一個資源集區來管理記憶體耗用量。  
  
 一個資料庫只能繫結至一個資源集區。 不過，您可以將多個資料庫繫結至相同的集區。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許將不含記憶體最佳化資料表的資料庫繫結至資源集區，但是這樣沒有任何作用。 如果您日後想要在資料庫中建立記憶體最佳化資料表，就可以將該資料庫繫結至具名資源集區。  
  
 資料庫與資源集區都必須事先存在，然後您才能將資料庫繫結至資源集區。 繫結會在下一次資料庫重新上線時生效。 如需詳細資訊，請參閱 [資料庫狀態](../../relational-databases/databases/database-states.md) 。  
  
 如需有關資源集區的詳細資訊，請參閱 [Resource Governor 資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)。  
  
## <a name="steps-to-bind-a-database-to-a-resource-pool"></a>將資料庫繫結至資源集區的步驟  
  
1.  [建立資料庫和資源集區](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_CreatePool)  
  
    1.  [建立資料庫](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_CreateDatabase)  
  
    2.  [決定 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 的最小值](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_DeterminePercent)  
  
    3.  [建立資源集區和設定記憶體](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_CreateResourcePool)  
  
2.  [將資料庫繫結至集區](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_DefineBinding)  
  
3.  [確認繫結](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ConfirmBinding)  
  
4.  [使繫結生效](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_MakeBindingEffective)  
  
 本主題的其他內容  
  
-   [變更現有集區上的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)  
  
-   [可用於記憶體最佳化資料表和索引的記憶體百分比](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)  
  
##  <a name="bkmk_CreatePool"></a> 建立資料庫和資源集區  
 您可以按照任何順序建立資料庫和資源集區。 重點在於這兩者必須事先存在，才能將資料庫繫結至資源集區。  
  
###  <a name="bkmk_CreateDatabase"></a> 建立資料庫  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 會建立名為 IMOLTP_DB 的資料庫，其中將包含一個或多個記憶體最佳化資料表。 執行此命令之前，路徑 \<磁碟機和路徑> 必須存在。  
  
```sql  
CREATE DATABASE IMOLTP_DB  
GO  
ALTER DATABASE IMOLTP_DB ADD FILEGROUP IMOLTP_DB_fg CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP_DB ADD FILE( NAME = 'IMOLTP_DB_fg' , FILENAME = 'c:\data\IMOLTP_DB_fg') TO FILEGROUP IMOLTP_DB_fg;  
GO  
```  
  
###  <a name="bkmk_DeterminePercent"></a> 決定 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 的最小值  
 判斷出記憶體最佳化資料表的記憶體需求之後，您必須決定所需數量佔可用記憶體的百分比，並將記憶體百分比設定為該值或更高。  
  
 **範例：**   
此範例假設您經過計算後，判斷出記憶體最佳化資料表和索引需要 16 GB 的記憶體。 假設您已獲認可使用 32 GB 的記憶體。  
  
 乍看之下，您似乎必須將 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 設定為 50 (16 等於 32 乘以 50%)。  不過，這樣並不會使您的記憶體最佳化資料表擁有足夠的記憶體。 看看下面表格 ([記憶體最佳化資料表和索引可用的記憶體百分比](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)) 我們得知假設有 32 GB 的認可記憶體時，只有 80% 可用於記憶體最佳化資料表和索引。  因此，最小和最大百分比要依據可用的記憶體來計算，而不是依據認可的記憶體。  
  
 `memoryNeedeed = 16`   
 `memoryCommitted = 32`   
 `availablePercent = 0.8`   
 `memoryAvailable = memoryCommitted * availablePercent`   
 `percentNeeded = memoryNeeded / memoryAvailable`  
  
 代入實際數字：   
`percentNeeded = 16 / (32 * 0.8) = 16 / 25.6 = 0.625`  
  
 換言之，您至少需要 62.5% 的可用記憶體，才會符合記憶體最佳化資料表和索引的 16 GB 需求。  由於 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 的值必須是整數，您就要將兩者設定為至少佔 63%。  
  
###  <a name="bkmk_CreateResourcePool"></a> 建立資源集區和設定記憶體  
 設定記憶體最佳化資料表的記憶體時，應該依據 MIN_MEMORY_PERCENT 規劃容量，而不是依據 MAX_MEMORY_PERCENT。  如需有關 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 的詳細資訊，請參閱 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)。 這樣可以為記憶體最佳化資料提供更可預測的記憶體可用性，因為 MIN_MEMORY_PERCENT 會對其他資源集區造成記憶體壓力，以確保記憶體可被接受。 若要確保記憶體可用，並幫助避免記憶體不足狀況，MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 的值應相同。 如需以認可記憶體數量為基礎，可用於記憶體最佳化資料表的記憶體百分比，請參閱以下的 [可用記憶體最佳化資料表和索引的記憶體百分比](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable) 。  
  
 如需有關在 VM 環境下作業的詳細資訊，請參閱 [最佳做法：在 VM 環境使用記憶體內部 OLTP](http://msdn.microsoft.com/library/27ec7eb3-3a24-41db-aa65-2f206514c6f9) 。  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼會建立名為 Pool_IMOLTP 的資源集區，而且一半的記憶體可供它使用。  建立集區之後，資源管理員會重新設定為包含 Pool_IMOLTP。  
  
```sql  
-- set MIN_MEMORY_PERCENT and MAX_MEMORY_PERCENT to the same value  
CREATE RESOURCE POOL Pool_IMOLTP   
  WITH   
    ( MIN_MEMORY_PERCENT = 63,   
    MAX_MEMORY_PERCENT = 63 );  
GO  
  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
##  <a name="bkmk_DefineBinding"></a> 將資料庫繫結至集區  
 您可以使用系統函數 `sp_xtp_bind_db_resource_pool` ，將資料庫繫結至資源集區。 此函數會採用兩個參數：資料庫名稱和資源集區名稱。  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 會定義 IMOLTP_DB 資料庫與 Pool_IMOLTP 資源集區的繫結。 在您讓資料庫重新上線之前，此繫結不會生效。  
  
```sql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
 系統函數 sp_xtp_bind_db_resourece_pool 會採用兩個字串參數：database_name 和 pool_name。  
  
##  <a name="bkmk_ConfirmBinding"></a> 確認繫結  
 確認繫結，並記下 IMOLTP_DB 的資源集區識別碼。 它不應該是 NULL。  
  
```sql  
SELECT d.database_id, d.name, d.resource_pool_id  
FROM sys.databases d  
GO  
```  
  
##  <a name="bkmk_MakeBindingEffective"></a> 使繫結生效  
 將資料庫繫結至資源集區之後，您必須讓資料庫離線再恢復上線，以使繫結生效。 如果您的資料庫先前已繫結至不同的集區，這樣做便會從先前的資源集區移除已配置的記憶體，而且記憶體最佳化資料表和索引的記憶體配置現在將由最近剛與資料庫繫結的新資源集區提供。  
  
```sql  
USE master  
GO  
  
ALTER DATABASE IMOLTP_DB SET OFFLINE  
GO  
ALTER DATABASE IMOLTP_DB SET ONLINE  
GO  
  
USE IMOLTP_DB  
GO  
```  
  
 此時，資料庫已繫結至資源集區。  
  
##  <a name="bkmk_ChangeAllocation"></a> 變更現有集區上的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT  
 如果您為伺服器另外再加入記憶體，或是您的記憶體最佳化資料表所需的記憶體數量已變更，可能就必須更改 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 的值。 下列步驟將為您示範如何更改資源集區的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 值。 請參閱下一節提供的指引，以得知 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 應該使用哪些值。  如需詳細資訊，請參閱 [最佳做法：在 VM 環境使用記憶體內部 OLTP](http://msdn.microsoft.com/library/27ec7eb3-3a24-41db-aa65-2f206514c6f9) 主題。  
  
1.  使用 `ALTER RESOURCE POOL` 變更 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 的值。  
  
2.  使用 `ALTER RESURCE GOVERNOR` ，以新的值重新設定資源管理員。  
  
 **範例程式碼**  
  
```sql  
ALTER RESOURCE POOL Pool_IMOLTP  
WITH  
     ( MIN_MEMORY_PERCENT = 70,  
       MAX_MEMORY_PERCENT = 70 )   
GO  
  
-- reconfigure the Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
##  <a name="bkmk_PercentAvailable"></a> 可用於記憶體最佳化資料表和索引的記憶體百分比  
 如果您將具有記憶體最佳化資料表的資料庫和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作負載對應至相同的資源集區，資源管理員就會設定 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 使用的內部臨界值，避免集區的使用者在集區使用量上發生衝突。 一般而言， [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 使用的臨界值大約是 80% 的集區。 下表顯示各種記憶體大小的實際臨界值。  
  
 您為 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 資料庫建立專用資源集區時，在考量資料列版本和資料成長之後，需要估計記憶體中資料表所需的實體記憶體數量。 估計需要的記憶體之後，請建立資源集區，且其中有一定比例的認可目標記憶體可用於 SQL 執行個體，如 DMV `sys.dm_os_sys_info` 中的 'committed_target_kb' 資料行所反映 (請參閱 [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md))。 例如，您可以建立資源集區 P1，其中有 40% 的總記憶體可供執行個體使用。 在此 40% 之中， [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 引擎會取用較小的百分比來儲存 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 資料。  這樣做可確保 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 不會耗用此集區中的所有記憶體。  這個較小的百分比值取決於目標認可的記憶體。 下表描述在 OOM 錯誤引發之前，資源集區 (具名或預設) 中可供 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 資料庫使用的記憶體。  
  
|目標認可的記憶體|記憶體中資料表可用的百分比|  
|-----------------------------|---------------------------------------------|  
|<= 8 GB|70%|  
|<= 16 GB|75%|  
|<= 32 GB|80%|  
|\<= 96 GB|85%|  
|>96 GB|90%|  
  
 例如，如果您的「目標認可的記憶體」為 100 GB，而您估計記憶體最佳化資料表和索引需要 60GB 的記憶體，那麼您可以建立一個 MAX_MEMORY_PERCENT = 67 的資源集區 (需要 60GB / 0.90 = 66.667GB – 四捨五入為 67GB；已安裝 67GB / 100GB = 67%)，確保您的 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 物件擁有所需的 60GB。  
  
 資料庫繫結至具名的資源集區後，請使用下列查詢查看跨不同資源集區的記憶體配置。  
  
```sql  
SELECT pool_id  
     , Name  
     , min_memory_percent  
     , max_memory_percent  
     , max_memory_kb/1024 AS max_memory_mb  
     , used_memory_kb/1024 AS used_memory_mb   
     , target_memory_kb/1024 AS target_memory_mb  
   FROM sys.dm_resource_governor_resource_pools  
```  
  
 此範例輸出表示，記憶體最佳化物件在資源集區 PoolIMOLTP 中取用的記憶體為 1356 MB，上限為 2307 MB。 此上限可控制對應至此集區的使用者和系統記憶體最佳化物件能夠取用的記憶體總數。  
  
 **範例輸出**   
這個輸出來自前面所建立的資料庫和資料表。  
  
```  
pool_id     Name        min_memory_percent max_memory_percent max_memory_mb used_memory_mb target_memory_mb  
----------- ----------- ------------------ ------------------ ------------- -------------- ----------------   
1           internal    0                  100                3845          125            3845  
2           default     0                  100                3845          32             3845  
259         PoolIMOLTP 0                  100                3845          1356           2307  
```  
  
 如需詳細資訊，請參閱 [sys.dm_resource_governor_resource_pools (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)。  
  
 如果您無法將資料庫繫結至具名資源集區，則資料庫會繫結至「預設」集區。 由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在大多數其他配置中會使用預設資源集區，因此您將無法針對所需資料庫精確使用 DMV sys.dm_resource_governor_resource_pools 監視記憶體最佳化資料表所耗用的記憶體。  
  
## <a name="see-also"></a>另請參閱  
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)   
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)   
 [[資源管理員]](../../relational-databases/resource-governor/resource-governor.md)   
 [Resource Governor 資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [建立資源集區](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [變更資源集區設定](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [刪除資源集區](../../relational-databases/resource-governor/delete-a-resource-pool.md)  
  
  
