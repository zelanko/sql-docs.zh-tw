---
title: sys.databases dm_db_log_info （Transact-sql） |Microsoft Docs
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
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7cb87d2d5677085edc8e6bd998f20c3c45013823
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68262084"
---
# <a name="sysdm_db_log_info-transact-sql"></a>sys.databases dm_db_log_info （Transact-sql）
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

傳回交易記錄檔的[虛擬記錄檔（VLF）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)資訊。 請注意，所有交易記錄檔都會合並在資料表輸出中。 輸出中的每個資料列都代表交易記錄中的 VLF，並在記錄檔中提供與該 VLF 相關的資訊。

## <a name="syntax"></a>語法  
  
```  
sys.dm_db_log_info ( database_id )  
``` 

## <a name="arguments"></a>引數  
 *database_id* |Null |預設  
 資料庫的識別碼。 *database_id*為**int**。有效的輸入為資料庫的識別碼、Null 或預設值。 預設值是 NULL。 Null 和 DEFAULT 在目前資料庫的內容中是對等的值。
 
 指定 Null 以傳回目前資料庫的 VLF 資訊。

 可以指定內建函數 [DB_ID](../../t-sql/functions/db-id-transact-sql.md)。 在未`DB_ID`指定資料庫名稱的情況下使用時，目前資料庫的相容性層級必須是90或更高。  

## <a name="table-returned"></a>傳回的資料表  

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id|**int**|資料庫識別碼。|
|file_id|**smallint**|交易記錄檔的檔案識別碼。|  
|vlf_begin_offset|**bigint** |從交易記錄檔開頭的[虛擬記錄檔（VLF）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)的位移位置。|
|vlf_size_mb |**float** |[虛擬記錄檔（VLF）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)大小，以 MB 為單位，四捨五入為2個小數位數。|     
|vlf_sequence_number|**bigint** |建立的順序中的[虛擬記錄檔（VLF）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)序號。 用來唯一識別記錄檔中的 Vlf。|
|vlf_active|**bit** |指出[虛擬記錄檔（VLF）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)是否正在使用中。 <br />0-VLF 不在使用中。<br />1-VLF 為使用中狀態。|
|vlf_status|**int** |[虛擬記錄檔（VLF）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)的狀態。 可能的值包括 <br />0-VLF 為非作用中 <br />1-VLF 已初始化但未使用 <br /> 2-VLF 為使用中狀態。|
|vlf_parity|**tinyint** |[虛擬記錄檔（VLF）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)的同位檢查。在內部用來判斷 VLF 內記錄檔的結尾。|
|vlf_first_lsn|**Nvarchar （48）** |虛擬記錄檔中第一筆記錄的記錄[序號（LSN）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) [（VLF）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)。|
|vlf_create_lsn|**Nvarchar （48）** |建立[虛擬記錄檔（VLF）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)之記錄檔記錄的[記錄序號（LSN）](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 。|
|vlf_encryptor_thumbprint|**varbinary(20)**| **適用於：** [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] <br><br> 如果使用[透明資料加密](../../relational-databases/security/encryption/transparent-data-encryption.md)加密 VLF，則顯示 VLF 的加密器指紋，否則為 Null。 |

## <a name="remarks"></a>備註
`sys.dm_db_log_info`動態管理函數會取代`DBCC LOGINFO`語句。    
 
## <a name="permissions"></a>權限  
需要資料庫`VIEW DATABASE STATE`中的許可權。  
  
## <a name="examples"></a>範例  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. 在具有大量 Vlf 的 SQL Server 實例中判斷資料庫
下列查詢會判斷記錄檔中有超過 100 Vlf 的資料庫，這可能會影響資料庫啟動、還原和復原時間。

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-position-of-the-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. 先判斷交易記錄中`VLF`最後一個位置，再壓縮記錄檔

下列查詢可用來判斷上次使用中 VLF 的位置，然後再于交易記錄檔上執行 shrinkfile，以判斷交易記錄檔是否可以壓縮。

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
[動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[資料庫相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[dm_db_log_space_usage &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

