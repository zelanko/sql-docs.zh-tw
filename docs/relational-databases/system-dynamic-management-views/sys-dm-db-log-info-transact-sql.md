---
description: 'sys.dm_db_log_info (Transact-sql) '
title: sys.dm_db_log_info (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
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
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 12fe1e95cbb1c7ad26025ee52ce111cb3f835704
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440823"
---
# <a name="sysdm_db_log_info-transact-sql"></a>sys.dm_db_log_info (Transact-sql) 
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

傳回交易記錄檔 [ (VLF) 資訊的虛擬記錄 ](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 檔。 請注意，所有交易記錄檔都會合並在資料表輸出中。 輸出中的每個資料列都代表交易記錄中的 VLF，並在記錄檔中提供與該 VLF 相關的資訊。

## <a name="syntax"></a>語法  
  
```  
sys.dm_db_log_info ( database_id )  
``` 

## <a name="arguments"></a>引數  
 *database_id* |Null |預設  
 資料庫的識別碼。 *database_id* 為 **int**。有效的輸入為資料庫的識別碼、Null 或預設值。 預設值是 NULL。 Null 和預設值在目前資料庫的內容中是相等的值。
 
 請指定 Null 來傳回目前資料庫的 VLF 資訊。

 可以指定內建函數 [DB_ID](../../t-sql/functions/db-id-transact-sql.md)。 使用 `DB_ID` 但未指定資料庫名稱時，目前資料庫的相容性層級必須為90或更高。  

## <a name="table-returned"></a>傳回的資料表  

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id|**int**|資料庫識別碼。|
|file_id|**smallint**|交易記錄檔的檔案識別碼。|  
|vlf_begin_offset|**bigint** |從交易記錄檔的開頭 [ (VLF) 的虛擬記錄 ](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 檔位移位置。|
|vlf_size_mb |**float** |[虛擬記錄檔 (VLF) ](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 大小（以 MB 為單位），舍入為2個小數位數。|     
|vlf_sequence_number|**bigint** |[虛擬記錄檔 (](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 以建立的順序 VLF) 序號。 用來唯一識別記錄檔中的 Vlf。|
|vlf_active|**bit** |指出 [ (VLF) 的虛擬記錄 ](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 檔是否正在使用中。 <br />0-VLF 不在使用中。<br />1-VLF 為作用中。|
|vlf_status|**int** |虛擬記錄檔的狀態 [ (VLF) ](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。 可能的值包括 <br />0-VLF 非使用中 <br />1-VLF 已初始化但未使用 <br /> 2-VLF 為作用中。|
|vlf_parity|**tinyint** |[虛擬記錄檔 (VLF) ](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)的同位檢查。在內部用來判斷 VLF 中的記錄結尾。|
|vlf_first_lsn|**Nvarchar (48)** |[ () ](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 虛擬記錄檔中第一筆記錄的記錄序號， [ (VLF) ](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。|
|vlf_create_lsn|**Nvarchar (48)** |[ (VLF) 建立虛擬記錄](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)檔之記錄檔記錄[ (LSN) ](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)的記錄序號。|
|vlf_encryptor_thumbprint|**varbinary(20)**| **適用對象：** [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] <br><br> 如果使用 [透明資料加密](../../relational-databases/security/encryption/transparent-data-encryption.md)加密 VLF，則顯示 VLF 的加密程式指紋，否則為 Null。 |

## <a name="remarks"></a>備註
`sys.dm_db_log_info`動態管理函數會取代 `DBCC LOGINFO` 語句。    
 
## <a name="permissions"></a>權限  
需要 `VIEW DATABASE STATE` 資料庫中的許可權。  
  
## <a name="examples"></a>範例  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. 在具有大量 Vlf 的 SQL Server 實例中判斷資料庫
下列查詢會在記錄檔中判斷具有 100 Vlf 以上的資料庫，這可能會影響資料庫啟動、還原和復原時間。

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-position-of-the-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. 判斷 `VLF` 壓縮記錄檔之前，在交易記錄中最後一個位置

下列查詢可用來判斷上一個使用中 VLF 在交易記錄上執行 shrinkfile 之前的位置，以判斷交易記錄是否可壓縮。

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
[資料庫相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

