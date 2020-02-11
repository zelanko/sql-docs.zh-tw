---
title: sys.databases dm_db_page_info （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_page_info
- sys.dm_db_page_info_TSQL
- dm_db_page_info
- dm_db_page_info_TSQL
- dbcc page
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_page_info dynamic management view
author: bluefooted
ms.author: pamela
manager: amitban
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0802f3013af11814586634f890bb8ddddeadeec6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68841602"
---
# <a name="sysdm_db_page_info-transact-sql"></a>sys.dm_db_page_info (Transact-SQL)

[!INCLUDE[tsql-appliesto-ssver15-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

傳回資料庫中頁面的相關資訊。  函數會傳回一個資料列，其中包含頁面的標頭資訊，包括`object_id`、 `index_id`和`partition_id`。  在大部分情況下，有此函式就不需要使用 `DBCC PAGE`。

> [!NOTE]
> `sys.dm_db_page_info`目前只有[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]和更新版本才支援。


## <a name="syntax"></a>語法   
```  
sys.dm_db_page_info ( DatabaseId, FileId, PageId, Mode )  
``` 

## <a name="arguments"></a>引數  
*DatabaseId* |Null |預設     
資料庫的識別碼。 *DatabaseId*為**Smallint**。 有效的輸入是資料庫的識別碼。 預設值為 Null，但傳送此參數的 Null 值將會導致錯誤。
 
*FileId* |Null |預設   
檔案的識別碼。 *FileId*為**int**。 有效的輸入是*DatabaseId*所指定之資料庫中的檔案識別碼。 預設值為 Null，但傳送此參數的 Null 值將會導致錯誤。

*PageId* |Null |預設   
這是頁面的識別碼。  *PageId*是**int**。 有效的輸入是*FileId*所指定之檔案中頁面的識別碼。 預設值為 Null，但傳送此參數的 Null 值將會導致錯誤。

*模式*|Null |預設   
判斷函數輸出中的詳細資料層級。 「有限」會針對所有描述資料行傳回 Null 值，「詳細」將會填入描述資料行。  預設值為「有限」。

## <a name="table-returned"></a>傳回的資料表  

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id |int |資料庫識別碼 |
|file_id |int |檔案識別碼 |
|page_id |int |頁面識別碼 |
|page_header_version |int |頁首版本 |
|page_type |int |頁面類型 |
|page_type_desc |Nvarchar （64） |頁面類型的描述 |
|page_type_flag_bits |Nvarchar （64） |在頁首中輸入旗標位 |
|page_type_flag_bits_desc |Nvarchar （64） |在頁首中輸入旗標位描述 |
|page_flag_bits |Nvarchar （64） |在頁首中旗標位 |
|page_flag_bits_desc |nvarchar(256) |頁首中的旗標位描述 |
|page_lsn |Nvarchar （64） |記錄序號/時間戳記 |
|page_level |int |索引中的頁面層級（分葉 = 0） |
|object_id |int |擁有該頁面之物件的識別碼 |
|index_id |int |索引的識別碼（若為堆積資料頁面，則為0） |
|partition_id |BIGINT |資料分割的識別碼 |
|alloc_unit_id |BIGINT |配置單位的識別碼 |
|is_encrypted |bit |指出頁面是否已加密的位 |
|has_checksum |bit |位，指出頁面是否有總和檢查碼值 |
|總和檢查碼 |int |儲存用來偵測資料損毀的總和檢查碼值 |
|is_iam_pg |bit |位，指出頁面是否為 IAM 頁面  |
|is_mixed_ext |bit |表示是否在混合範圍內配置的位 |
|has_ghost_records |bit |指出頁面是否包含准刪除記錄的位 <br> 准刪除記錄是指已標示為要刪除但尚未移除的記錄。|
|has_version_records |bit |位，指出頁面是否包含用於[加速資料庫](../backup-restore/restore-and-recovery-overview-sql-server.md#adr)復原的版本記錄 |
|pfs_page_id |int |對應 PFS 頁面的頁面識別碼 |
|pfs_is_allocated |bit |位，指出是否在對應的 PFS 頁面中將頁面標示為已配置 |
|pfs_alloc_percent |int |依對應的 PFS 位元組指示的配置百分比 |
|pfs_status |Nvarchar （64） |PFS 位元組 |
|pfs_status_desc |Nvarchar （64） |PFS 位元組的描述 |
|gam_page_id |int |對應 GAM 頁面的頁面識別碼 |
|gam_status |bit |要指出是否已在 GAM 中配置的位 |
|gam_status_desc |Nvarchar （64） |GAM 狀態位的描述 |
|sgam_page_id |int |對應 SGAM 頁面的頁面識別碼 |
|sgam_status |bit |要指出是否已在 SGAM 中配置的位 |
|sgam_status_desc |Nvarchar （64） |SGAM 狀態位的描述 |
|diff_map_page_id |int |對應差異點陣圖頁面的頁面識別碼 |
|diff_status |bit |表示差異狀態是否已變更的位 |
|diff_status_desc |Nvarchar （64） |差異狀態位的描述 |
|ml_map_page_id |int |對應最小記錄點陣圖頁面的頁面識別碼 |
|ml_status |bit |指出頁面是否為最低限度記錄的位 |
|ml_status_desc |Nvarchar （64） |最低記錄狀態位的描述 |
|prev_page_file_id |smallint |先前的分頁檔案識別碼 |
|prev_page_page_id |int |上一頁頁面識別碼 |
|next_page_file_id |smallint |下一個分頁檔案識別碼 |
|next_page_page_id |int |下一頁頁面識別碼 |
|fixed_length |smallint |固定大小資料列的長度 |
|slot_count |smallint |插槽總數（已使用和未使用） <br> 若為數據頁，這個數位就相當於資料列數目。 |
|ghost_rec_count |smallint |頁面上標示為幻影的記錄數目 <br> 准刪除記錄是指已標示為要刪除但尚未移除的記錄。 |
|free_bytes |smallint |頁面上的可用位元組數 |
|free_data_offset |int |資料區域結尾的可用空間位移 |
|reserved_bytes |smallint |所有交易保留的可用位元組數（如果堆積） <br> 幻影資料列數（如果是索引分葉） |
|reserved_bytes_by_xdes_id |smallint |M_xdesID 所貢獻的空間 m_reservedCnt <br> 僅供偵錯工具之用 |
|xdes_id |Nvarchar （64） |由 m_reserved 所貢獻的最新交易 <br> 僅供偵錯工具之用 |
||||

## <a name="remarks"></a>備註
`sys.dm_db_page_info`動態管理函數會傳回頁面標頭`page_id`中`file_id`出現`index_id`的`object_id`頁面資訊，例如、、等。 這種資訊有助於疑難排解和偵測各種效能（鎖定和閂鎖爭用）和損毀問題。

`sys.dm_db_page_info`在許多情況下，可以用`DBCC PAGE`來取代語句，但它只會傳回頁首資訊，而不會傳回頁面的主體。 `DBCC PAGE`在需要整個頁面內容的使用案例中，仍會需要。

## <a name="using-in-conjunction-with-other-dmvs"></a>搭配其他 Dmv 使用
的其中一個重要使用案例， `sys.dm_db_page_info`就是將它與公開頁面資訊的其他 dmv 聯結在一起。  為了方便此使用案例，已新增名`page_resource`為的新資料行，其會以8位元組十六進位格式公開頁面資訊。 此資料行已新增至`sys.dm_exec_requests`和`sys.sysprocesses` ，未來將會視需要新增至其他 dmv。

`sys.fn_PageResCracker`新的函式會採用`page_resource`做為輸入，並輸出包含`database_id`、 `file_id`和`page_id`的單一資料列。  然後，可以使用此函式來加速或`sys.dm_exec_requests` `sys.sysprocesses`與`sys.dm_db_page_info`之間的聯結。

## <a name="permissions"></a>權限  
需要資料庫`VIEW DATABASE STATE`中的許可權。  
  
## <a name="examples"></a>範例  
  
### <a name="a-displaying-all-the-properties-of-a-page"></a>A. 顯示頁面的所有屬性
下列查詢會傳回一個資料列，其中包含給定`database_id` `file_id`之的所有頁面資訊`page_id` 、與預設模式（「有限」）的組合

```sql
SELECT *  
FROM sys.dm_db_page_info (5, 1, 15, DEFAULT)
```

### <a name="b-using-sysdm_db_page_info-with-other-dmvs"></a>B. 搭配其他 Dmv 使用 sys.databases dm_db_page_info 

下列查詢會在資料列包含`wait_resource`非 null `sys.dm_exec_requests`時，針對每個公開的傳回一個資料列。`page_resource`

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 'LIMITED') AS page_info
```

## <a name="see-also"></a>另請參閱  
[動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[資料庫相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)     
[sys.fn_PageResCracker](../../relational-databases/system-functions/sys-fn-pagerescracker-transact-sql.md)


