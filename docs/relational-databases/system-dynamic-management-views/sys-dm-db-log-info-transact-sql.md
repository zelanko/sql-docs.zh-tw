---
title: "sys.dm_db_log_info (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
caps.latest.revision: "4"
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: b7250943f4e92d60888a75d9e577388f3cc6b1ed
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbloginfo-transact-sql"></a>sys.dm_db_log_info (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

傳回`VLF`交易記錄檔的資訊。 （所有記錄檔會都併入資料表輸出）。 在輸出中的每個資料列都代表`VLF`交易記錄檔中，並提供該記錄檔中的 VLF 的相關資訊。

## <a name="syntax"></a>語法  
  
```  
sys.dm_db_log_info ( database_id )  
```  
## <a name="arguments"></a>引數  
 *database_id* |NULL |預設值  
 資料庫的識別碼。 *database_id*是**int**。有效輸入如下的資料庫、 NULL 或預設的識別碼。 預設值是 NULL。 NULL 和 DEFAULT 是目前資料庫內容中的對等值。
 
 指定 NULL 來傳回`VLF`目前資料庫的資訊。

 內建函式[DB_ID](../../t-sql/functions/db-id-transact-sql.md)可以指定。 在不指定資料庫名稱的情況下使用 DB_ID 時，目前資料庫的相容性層級必須是 90 或 90 以上。  

## <a name="table-returned"></a>傳回的資料表  

|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|資料庫識別碼。|
|file_id|**smallint**|交易記錄檔的檔案識別碼。|  
|vlf_begin_offset|**bigint** |位移位置的`VLF`從交易記錄檔的開頭。|
|vlf_size_mb |**float** |`VLF`以 mb 為單位的大小會四捨五入為 2 的小數位數。|     
|vlf_sequence_number|**bigint** |`VLF`建立順序的序號。 用來唯一識別`VLFs`記錄檔中。|
|vlf_active|**bit** |指出是否 VLF 是否使用中。 <br />0-vlf 不在使用中。<br />1-`VLF`為作用中。|
|vlf_status|**int** |狀態`VLF`。 可能值包括： <br />0-`VLF`非使用中 <br />1-vlf 已初始化但未使用 <br /> 2-`VLF`為作用中。|
|vlf_parity|**tinyint** |同位檢查的`VLF`。在內部用來判斷內記錄的結尾`VLF`。|
|vlf_first_lsn|**nvarchar(48)** |中的第一筆記錄的 LSN `VLF`。|
|vlf_create_lsn|**nvarchar(48)** |LSN 的記錄檔記錄，建立`VLF`。|

## <a name="remarks"></a>備註
 `sys.dm_db_log_info`動態管理函數會取代`DBCC LOGINFO`陳述式。 
 
## <a name="permissions"></a>Permissions  
 需要`VIEW DATABASE STATE`資料庫的權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. 判斷 tempdb 資料庫中的數量太多的 SQL Server 執行個體`VLFs`
下列查詢會判斷資料庫有超過 100`VLFs`在記錄檔中，這可能會影響資料庫啟動、 還原及復原時間。

```sql
SELECT name,count(l.database_id) as 'vlf_count' from sys.databases s
cross apply sys.dm_db_log_info(s.database_id) l
group by name
having count(l.database_id)> 100
```

### <a name="b-determing-the-status-of-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. 判斷 tempdb 的最後一個狀態`VLF`之前記錄檔壓縮交易記錄檔中

下列查詢可用來判斷上次狀態`VLF`交易記錄檔，以判斷是否可以壓縮交易記錄檔上執行 shrinkfile 之前。

```sql
USE <database name>
GO

SELECT top 1 DB_NAME(database_id) as "Database Name",file_id,vlf_size_mb,vlf_sequence_number, vlf_active, vlf_status
from sys.dm_db_log_info(DEFAULT)
order by vlf_sequence_number desc
```


## <a name="see-also"></a>請參閱＜  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [資料庫相關動態管理檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)    
  



