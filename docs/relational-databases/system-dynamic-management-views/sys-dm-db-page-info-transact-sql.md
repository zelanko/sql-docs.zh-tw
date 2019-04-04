---
title: sys.dm_db_page_info (Transact-SQL) | Microsoft Docs
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
author: ''
ms.author: pamela
manager: amitban
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2246abe2343622f2aece785a31e1e31f7166822b
ms.sourcegitcommit: fc1739be9b2735b2bb469979936e76ca2a3830f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/03/2019
ms.locfileid: "58899714"
---
# <a name="sysdmdbpageinfo-transact-sql"></a>sys.dm_db_page_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在資料庫中傳回頁面的相關資訊。  此函數會傳回一個資料列包含標頭資訊 頁面上，從包括`object_id`， `index_id`，和`partition_id`。  在大部分情況下，有此函式就不需要使用 `DBCC PAGE`。

## <a name="syntax"></a>語法   
```  
sys.dm_db_page_info ( DatabaseId, FileId, PageId, Mode )  
``` 

## <a name="arguments"></a>引數  
*DatabaseId* |NULL |預設值     
資料庫的識別碼。 *DatabaseId*已**smallint**。 有效的輸入是資料庫的識別碼。 預設值是 NULL，但是傳送 NULL 值，這個參數會導致錯誤。
 
*FileId* |NULL |預設值   
檔案的識別碼。 *FileId*已**int**。有效的輸入是所指定的資料庫中的檔案的 ID 編號*DatabaseId*。 預設值是 NULL，但是傳送 NULL 值，這個參數會導致錯誤。

*採用*|NULL |預設值   
是頁面的識別碼。  *PageId*已**int**。有效的輸入是所指定的檔案中的頁面識別碼*FileId*。 預設值是 NULL，但是傳送 NULL 值，這個參數會導致錯誤。

*模式*|NULL |預設值   
判斷輸出中的函式的詳細程度。 '限制' 會傳回 NULL 值的所有描述資料行中，'詳細' 將會填入描述資料行。  預設值是 '限制'。

## <a name="table-returned"></a>傳回的資料表  

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id |ssNoversion |資料庫識別碼 |
|file_id |ssNoversion |檔案識別碼 |
|page_id |ssNoversion |頁面識別碼 |
|page_type |ssNoversion |頁面類型 |
|page_type_desc |nvarchar(64) |頁面類型的描述 |
|page_flag_bits |nvarchar(64) |頁面標頭中的旗標位元 |
|page_flag_bits_desc |nvarchar(256) |頁面標頭中的旗標位元描述 |
|page_type_flag_bits |nvarchar(64) |頁面標頭中的型別旗標位元 |
|page_type_flag_bits_desc |nvarchar(64) |頁面標頭中的型別旗標位元描述 |
|object_id |ssNoversion |擁有分頁的物件識別碼 |
|index_id |ssNoversion |索引 (堆積資料頁的 0) 的識別碼 |
|partition_id |BIGINT |資料分割識別碼 |
|alloc_unit_id |BIGINT |配置單位識別碼 |
|page_level |ssNoversion |在索引中頁面的層級 (分葉 = 0) |
|slot_count |SMALLINT |總數的位置 （使用和未使用） <br> 資料頁，這個號碼是相等的資料列數目。 |
|ghost_rec_count |SMALLINT |標示為在頁面上的準刪除記錄數目 <br> 準刪除的記錄是指已標示為刪除但尚未移除。 |
|torn_bits |ssNoversion |1 位元，每個偵測損毀的磁區寫入。 也可以用來儲存總和檢查碼 <br> 這個值用來偵測資料損毀 |
|is_iam_pg |bit |表示頁面為 IAM 頁面的位元  |
|is_mixed_ext |bit |位元來指示是否配置混合範圍 |
|pfs_file_id |SMALLINT |對應的 PFS 頁面檔案識別碼 |
|pfs_page_id |ssNoversion |對應的 PFS 頁面的頁面識別碼 |
|pfs_alloc_percent |ssNoversion |PFS 位元組所指定的配置百分比 |
|pfs_status |nvarchar(64) |PFS 位元組 |
|pfs_status_desc |nvarchar(64) |PFS 位元組的描述 |
|gam_file_id |SMALLINT |對應的 GAM 頁面檔案識別碼 |
|gam_page_id |ssNoversion |對應的 GAM 頁面的頁面識別碼 |
|gam_status |bit |位元來指示是否配置在 GAM |
|gam_status_desc |nvarchar(64) |GAM 葒鷑糔磢的描述 |
|sgam_file_id |SMALLINT |對應的 SGAM 頁面的檔案識別碼 |
|sgam_page_id |ssNoversion |對應的 SGAM 頁面的頁面識別碼 |
|sgam_status |bit |位元來指示是否配置 SGAM 中 |
|sgam_status_desc |nvarchar(64) |SGAM 葒鷑糔磢的描述 |
|diff_map_file_id |SMALLINT |對應的差異點陣圖頁面檔案識別碼 |
|diff_map_page_id |ssNoversion |對應的差異點陣圖頁面的頁面識別碼 |
|diff_status |bit |表示如果差異狀態已變更位元 |
|diff_status_desc |nvarchar(64) |Diff 葒鷑糔磢的描述 |
|ml_file_id |SMALLINT |對應的最低限度記錄的點陣圖頁面檔案識別碼 |
|ml_page_id |ssNoversion |對應的最低限度記錄的點陣圖頁面的頁面識別碼 |
|ml_status |bit |指出頁面是否會進行最低限度記錄的位元 |
|ml_status_desc |nvarchar(64) |位元的最低限度記錄狀態的描述 |
|free_bytes |SMALLINT |在頁面上的可用位元組數 |
|free_data_offset |ssNoversion |在資料區域的結尾的可用空間位移 |
|reserved_bytes |SMALLINT |所有交易所保留的可用位元組數目 (如果堆積) <br> 準刪除列 （如果索引分葉） 數 |
|reserved_xdes_id |SMALLINT |M_reservedCnt 的 m_xdesID 所提供的空間 <br> 偵錯之用 |
|xdes_id |nvarchar(64) |M_reserved 所提供的最新交易 <br> 偵錯之用 |
|prev_page_file_id |SMALLINT |先前的頁面檔案識別碼 |
|prev_page_page_id |ssNoversion |前一個頁面的頁面識別碼 |
|next_page_file_id |SMALLINT |下一個頁面檔案識別碼 |
|next_page_page_id |ssNoversion |下一步 頁面的頁面識別碼 |
|min_len |SMALLINT |固定的大小的資料列的長度 |
|lsn |nvarchar(64) |記錄序號 / 時間戳記 |
|header_version |ssNoversion |頁面標頭版本 |

## <a name="remarks"></a>備註
`sys.dm_db_page_info`動態管理函數會傳回類似的頁面資訊`page_id`， `file_id`， `index_id`，`object_id`等，會出現在頁面標頭。 這項資訊是用於疑難排解和偵錯各種效能 （鎖定和閂鎖爭用） 和損毀問題。

`sys.dm_db_page_info` 可用的位置`DBCC PAGE`陳述式，在許多情況下，但它只傳回頁面標頭資訊，頁面的主體。 `DBCC PAGE` 將仍需要其中頁面的整個內容所需的使用案例。

## <a name="using-in-conjunction-with-other-dmvs"></a>搭配使用與其他 Dmv
其中一個重要使用案例`sys.dm_db_page_info`是將它與其他公開頁面資訊的 Dmv 聯結。  若要加速此使用案例中，新的資料行稱為`page_resource`已公開為 8 個位元組的十六進位格式中的頁面資訊。 此資料行已新增至`sys.dm_exec_requests`和`sys.sysprocesses`，並將會加入未來所需的其他 Dmv。

新的函數`sys.fn_PageResCracker`，接受`page_resource`做為輸入和輸出，其中包含單一資料列`database_id`，`file_id`和`page_id`。  此函式可以再用來協助之間的聯結`sys.dm_exec_requests`或是`sys.sysprocesses`和`sys.dm_db_page_info`。

## <a name="permissions"></a>Permissions  
需要`VIEW DATABASE STATE`資料庫的權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-displaying-all-the-properties-of-a-page"></a>A. 顯示頁面的所有屬性
下列查詢會傳回一個資料列的所有頁面資訊與給定`database_id`， `file_id`，`page_id`搭配預設模式 （' 有限'）

```sql
SELECT *  
FROM sys.dm_db_page_info (5, 1, 15, DEFAULT)
```

### <a name="b-using-sysdmdbpageinfo-with-other-dmvs"></a>B. 使用 sys.dm_db_page_info 與其他 Dmv 

下列查詢會傳回每一個資料列`wait_resource`由`sys.dm_exec_requests`時的資料列包含非 null `page_resource`

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 'LIMITED') AS page_info
```

## <a name="see-also"></a>另請參閱  
[動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)     
[sys.fn_PageResCracker](../../relational-databases/system-functions/sys-fn-pagerescracker-transact-sql.md)


