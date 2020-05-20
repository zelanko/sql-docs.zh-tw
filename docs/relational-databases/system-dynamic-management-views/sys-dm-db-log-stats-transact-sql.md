---
title: sys.databases dm_db_log_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 25488898f7f8c6fb56ea75bc62480aefea171b59
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829474"
---
# <a name="sysdm_db_log_stats-transact-sql"></a>sys.dm_db_log_stats (Transact-SQL)   
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

傳回資料庫交易記錄檔的摘要層級屬性和資訊。 使用這項資訊來監視和診斷交易記錄的健全狀況。   
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>引數  

*database_id* |Null |**預設值**

資料庫的識別碼。 `database_id` 為 `int`。 有效的輸入是資料庫、或的識別碼 `NULL` `DEFAULT` 。 預設值為 `NULL`。 `NULL`和在 `DEFAULT` 目前資料庫的內容中是對等的值。  
可以指定內建函數 [DB_ID](../../t-sql/functions/db-id-transact-sql.md)。 在 `DB_ID` 未指定資料庫名稱的情況下使用時，目前資料庫的相容性層級必須是90或更高。

  
## <a name="tables-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |資料庫識別碼 |  
|recovery_model |**nvarchar(60)**   |   資料庫的復原模式。 可能的值包括： <br /> 簡單<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   交易記錄檔中的目前起始[記錄序號（LSN）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 。|  
|log_end_lsn    |**nvarchar(24)**   |   交易記錄中最後一個記錄檔記錄的[記錄序號（LSN）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 。|  
|current_vlf_sequence_number    |**bigint** |   執行時的目前[虛擬記錄檔（VLF）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)序號。|  
|current_vlf_size_mb    |**float**  |   目前的[虛擬記錄檔（VLF）大小（](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)以 MB 為單位）。|   
|total_vlf_count    |**bigint** |   交易記錄檔中的[虛擬記錄檔（vlf）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)總數。 |  
|total_log_size_mb  |**float**  |   交易記錄檔大小總計（以 MB 為單位）。 |  
|active_vlf_count   |**bigint** |   交易記錄中的作用中[虛擬記錄檔（vlf）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)總數。|  
|active_log_size_mb |**float**  |   使用中交易記錄大小總計（以 MB 為單位）。|  
|log_truncation_holdup_reason   |**nvarchar(60)**   |   記錄截斷扣留原因。 值與 `log_reuse_wait_desc` 的資料行相同 `sys.databases` 。  （如需這些值的詳細說明，請參閱[交易記錄](../../relational-databases/logs/the-transaction-log-sql-server.md)）。 <br />可能的值包括： <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />複寫<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />其他暫時性 |  
|log_backup_time    |**datetime**   |   前次交易歷史記錄備份時間。|   
|log_backup_lsn |**nvarchar(24)**   |   前次交易歷史記錄備份[記錄序號（LSN）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|   
|log_since_last_log_backup_mb   |**float**  |   前次交易歷史記錄備份[記錄序號（LSN）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)後的記錄檔大小（以 MB 為單位）。|  
|log_checkpoint_lsn |**nvarchar(24)**   |   最後一個檢查點[記錄序號（LSN）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|  
|log_since_last_checkpoint_mb   |**float**  |   自上一個檢查點[記錄序號（LSN）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)起的記錄大小（以 MB 為單位）。|  
|log_recovery_lsn   |**nvarchar(24)**   |   資料庫的復原[記錄序號（LSN）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 。 如果在 `log_recovery_lsn` 檢查點 lsn 之前發生， `log_recovery_lsn` 則是最舊的使用中交易 LSN，否則 `log_recovery_lsn` 為檢查點 lsn。|  
|log_recovery_size_mb   |**float**  |   記錄檔恢復[記錄序號（LSN）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)後的記錄檔大小（MB）。|  
|recovery_vlf_count |**bigint** |   容錯移轉或伺服器重新開機時，要復原的[虛擬記錄檔（vlf）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)總數。 |  


## <a name="remarks"></a>備註
`sys.dm_db_log_stats`針對參與可用性群組做為次要複本的資料庫執行時，只會傳回上述欄位的子集。  目前， `database_id` `recovery_model` `log_backup_time` 針對次要資料庫執行時，只會傳回、和。   

## <a name="permissions"></a>權限  
需要 `VIEW DATABASE STATE` 資料庫中的許可權。   
  
## <a name="examples"></a>範例  

### <a name="a-determining-databases-in-a-ssnoversion-instance-with-high-number-of-vlfs"></a>A. 在具有大量 Vlf 的實例中判斷資料庫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]   
下列查詢會傳回記錄檔中具有 100 Vlf 以上的資料庫。 大量的 Vlf 可能會影響資料庫啟動、還原和復原時間。

```sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-ssnoversion-instance-with-transaction-log-backups-older-than-4-hours"></a>B. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用超過4小時的交易記錄備份來判斷實例中的資料庫   
下列查詢會決定實例中資料庫的最後一次記錄備份時間。

```sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>另請參閱  
[動態管理 Views 和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[資料庫相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[dm_db_log_space_usage &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
  
