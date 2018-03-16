---
title: sys.dm_db_log_info (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/11/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
caps.latest.revision: 
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: 56064f19713bf3e5da29109520045762474d4539
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2018
---
# <a name="sysdmdbloginfo-transact-sql"></a>sys.dm_db_log_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

傳回[虛擬記錄檔 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)交易記錄的資訊。 請注意，所有交易記錄檔會都併入資料表輸出。 在輸出中的每個資料列代表 VLF 中的交易記錄檔，並提供該記錄檔中的 VLF 的相關資訊。

## <a name="syntax"></a>語法  
  
```  
sys.dm_db_log_info ( database_id )  
```  
## <a name="arguments"></a>引數  
 *database_id* |NULL |預設值  
 資料庫的識別碼。 *database_id*是**int**。有效輸入如下的資料庫、 NULL 或預設的識別碼。 預設值是 NULL。 NULL 和 DEFAULT 是目前資料庫內容中的對等值。
 
 請指定 NULL 來傳回目前資料庫的 VLF 資訊。

 內建函式[DB_ID](../../t-sql/functions/db-id-transact-sql.md)可以指定。 當使用`DB_ID`如果不指定資料庫名稱，在目前資料庫的相容性層級必須是 90 或更高。  

## <a name="table-returned"></a>傳回的資料表  

|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|資料庫識別碼。|
|file_id|**smallint**|交易記錄檔的檔案識別碼。|  
|vlf_begin_offset|**bigint** |位移位置的[虛擬記錄檔 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)從交易記錄檔的開頭。|
|vlf_size_mb |**float** |[虛擬記錄檔 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)大小以 mb 為單位，四捨五入為 2 的小數位數。|     
|vlf_sequence_number|**bigint** |[虛擬記錄檔 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)建立順序的序號。 用來唯一識別記錄檔中的 Vlf。|
|vlf_active|**bit** |指出是否[虛擬記錄檔 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)是否為使用中。 <br />0-VLF 不在使用中。<br />1-VLF 為作用中。|
|vlf_status|**int** |狀態[虛擬記錄檔 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。 可能值包括： <br />0-VLF 為非使用中 <br />1-VLF 已初始化但未使用 <br /> 2-VLF 為作用中。|
|vlf_parity|**tinyint** |同位檢查的[虛擬記錄檔 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。內部用來判斷 VLF 中的記錄檔的結尾。|
|vlf_first_lsn|**nvarchar(48)** |[記錄序號 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)中的第一筆記錄的[虛擬記錄檔 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。|
|vlf_create_lsn|**nvarchar(48)** |[記錄序號 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)記錄檔的記錄建立[虛擬記錄檔 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。|

## <a name="remarks"></a>備註
 `sys.dm_db_log_info`動態管理函數會取代`DBCC LOGINFO`陳述式。 
 
## <a name="permissions"></a>Permissions  
 需要`VIEW DATABASE STATE`資料庫的權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. 判斷 tempdb 資料庫中有大量的 Vlf 的 SQL Server 執行個體
下列查詢會判斷資料庫有超過 100 個 Vlf 中的記錄檔，這可能會影響資料庫啟動、 還原及復原時間。

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-position-of-the-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. 判斷 tempdb 的最後位置`VLF`之前記錄檔壓縮交易記錄檔中

下列查詢可用來判斷交易記錄，以判斷是否可以壓縮交易記錄檔上執行 shrinkfile 之前的最後一個使用中的 VLF 的位置。

```sql
USE AdventureWorks2016
GO

;WITH cte_vlf AS (
SELECT ROW_NUMBER() OVER(ORDER BY vlf_begin_offset) AS vlfid, DB_NAME(database_id) AS [Database Name], vlf_sequence_number, vlf_active, vlf_begin_offset, vlf_size_mb
    FROM sys.dm_db_log_info(DEFAULT)),
cte_vlf_cnt AS (SELECT [Database Name], COUNT(vlf_sequence_number) AS vlf_count,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 0) AS vlf_count_inactive,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS vlf_count_active,
    (SELECT MIN(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_min_vlf_active,
    (SELECT MIN(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS min_vlf_active,
    (SELECT MAX(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_max_vlf_active,
    (SELECT MAX(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS max_vlf_active
    FROM cte_vlf
    GROUP BY [Database Name])
SELECT [Database Name], vlf_count, min_vlf_active, ordinal_min_vlf_active, max_vlf_active, ordinal_max_vlf_active,
((ordinal_min_vlf_active-1)*100.00/vlf_count) AS free_log_pct_before_active_log,
((ordinal_max_vlf_active-(ordinal_min_vlf_active-1))*100.00/vlf_count) AS active_log_pct,
((vlf_count-ordinal_max_vlf_active)*100.00/vlf_count) AS free_log_pct_after_active_log
FROM cte_vlf_cnt
GO
```

## <a name="see-also"></a>另請參閱  
[動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

