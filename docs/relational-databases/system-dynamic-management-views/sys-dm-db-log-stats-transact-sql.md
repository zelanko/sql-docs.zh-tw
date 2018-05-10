---
title: sys.dm_db_log_stats (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_log_stats_TSQL
- sys.dm_db_log_stats
- sys.dm_db_log_stats_TSQL
- dm_db_log_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_stats dynamic management function
ms.assetid: ''
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 30885a40c1ccd3ca12b7517d377fb717c7dd6368
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmdblogstats-transact-sql"></a>sys.dm_db_log_stats (TRANSACT-SQL)   
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

傳回資料庫的交易記錄檔的摘要層級的屬性和資訊。 使用此資訊來監視和診斷的交易記錄檔的健全狀況。   
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>引數  

*database_id* |NULL |**預設**

資料庫的識別碼。 `database_id` 為 `int`。 有效輸入如下的資料庫，識別碼`NULL`，或`DEFAULT`。 預設值為 `NULL`。 `NULL` 和`DEFAULT`是目前資料庫內容中的對等值。  
內建函式[DB_ID](../../t-sql/functions/db-id-transact-sql.md)可以指定。 當使用`DB_ID`如果不指定資料庫名稱，在目前資料庫的相容性層級必須是 90 或更高。

  
## <a name="tables-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |資料庫識別碼 |  
|recovery_model |**nvarchar(60)**   |   資料庫的復原模式。 可能的值包括： <br /> SIMPLE<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   目前的開始時間[記錄序號 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)交易記錄檔中。|  
|log_end_lsn    |**nvarchar(24)**   |   [記錄序號 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)的交易記錄檔中的最後一筆記錄。|  
|current_vlf_sequence_number    |**bigint** |   目前[虛擬記錄檔 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)執行的時間點序號。|  
|current_vlf_size_mb    |**float**  |   目前[虛擬記錄檔 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)大小以 mb 為單位。|   
|total_vlf_count    |**bigint** |   總數[虛擬記錄檔 (Vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)交易記錄檔中。 |  
|total_log_size_mb  |**float**  |   交易記錄總大小 （mb）。 |  
|active_vlf_count   |**bigint** |   作用中的總數[虛擬記錄檔 (Vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)交易記錄檔中。|  
|active_log_size_mb |**float**  |   使用中交易記錄總大小 （mb）。|  
|log_truncation_holdup_reason   |**nvarchar(60)**   |   記錄截斷扣留的原因。 值是與相同`log_reuse_wait_desc`資料行`sys.databases`。  (如需詳細說明這些值，請參閱[交易記錄](../../relational-databases/logs/the-transaction-log-sql-server.md))。 <br />可能的值包括： <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />複寫<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />其他暫時性 |  
|log_backup_time    |**datetime**   |   上次交易記錄備份的時間。|   
|log_backup_lsn |**nvarchar(24)**   |   上次備份交易記錄[記錄序號 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|   
|log_since_last_log_backup_mb   |**float**  |   自上次備份交易記錄檔記錄檔大小 （mb）[記錄序號 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|  
|log_checkpoint_lsn |**nvarchar(24)**   |   最後一個檢查點[記錄序號 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|  
|log_since_last_checkpoint_mb   |**float**  |   自最後一個檢查點記錄檔大小 （mb）[記錄序號 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|  
|log_recovery_lsn   |**nvarchar(24)**   |   復原[記錄序號 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)的資料庫。 如果`log_recovery_lsn`發生前的檢查點 LSN，`log_recovery_lsn`否則是最舊的使用中交易的 LSN，`log_recovery_lsn`是檢查點 LSN。|  
|log_recovery_size_mb   |**float**  |   因為記錄檔的復原記錄檔大小 （mb）[記錄序號 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|  
|recovery_vlf_count |**bigint** |   總數[虛擬記錄檔 (Vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)復原，如果發生容錯移轉或伺服器重新啟動。 |  


## <a name="permissions"></a>Permissions  
需要`VIEW DATABASE STATE`資料庫的權限。   
  
## <a name="examples"></a>範例  

### <a name="a-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-high-number-of-vlfs"></a>A. 判斷資料庫中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有大量 Vlf 的執行個體   
下列查詢會傳回資料庫有超過 100 個 Vlf 的記錄檔中。 Vlf 的數目很大，可能會影響資料庫啟動、 還原及復原時間。

```sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-transaction-log-backups-older-than-4-hours"></a>B. 判斷資料庫中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]超過 4 小時內的交易記錄備份的執行個體。   
下列查詢決定最後一個記錄備份時間，執行個體中的資料庫。

```sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>另請參閱  
[動態管理檢視與函數 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
  
