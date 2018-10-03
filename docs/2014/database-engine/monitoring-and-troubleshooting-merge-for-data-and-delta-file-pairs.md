---
title: 監視和疑難排解合併資料和差異檔案組 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a8b0bacc-4d2c-42e4-84bf-1a97e0bd385b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1f5febee69483b5f1a2e8aa5b7b48fdde0a7ada2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075278"
---
# <a name="monitoring-and-troubleshooting-merge-for-data-and-delta-file-pairs"></a>對資料檔案和差異檔案組的合併進行監視和疑難排解
  記憶體中 OLTP 會使用合併原則自動合併相鄰資料及差異檔案組。 您無法停用合併活動。  
  
 您可以監視資料及差異檔案組，如下所示：  
  
-   比較記憶體中儲存體與整體儲存體的大小。 如果儲存體不成比例地大，可能是未觸發合併。 如需資訊  
  
-   看看使用的資料和差異檔案中使用的空間[sys.dm_db_xtp_checkpoint_files &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql)若要查看是否合併未觸發時應該。  
  
## <a name="performing-a-manual-merge"></a>執行手動合併  
 您可以使用[sys.sp_xtp_merge_checkpoint_files &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql)若要執行手動合併。  
  
 使用以下查詢擷取有關資料及差異檔案的資訊。  
  
```tsql  
select checkpoint_file_id, file_type_desc, internal_storage_slot, file_size_in_bytes, file_size_used_in_bytes,   
inserted_row_count, deleted_row_count, lower_bound_tsn, upper_bound_tsn   
from sys.dm_db_xtp_checkpoint_files  
where state = 1  
order by file_type_desc, upper_bound_tsn  
```  
  
 假設您發現三個未合併的資料檔案。 您可以使用第一個資料檔案的 `lower_bound_tsn` 值和最後一個資料檔案的 `upper_bound_tsn` 以發出下列命令：  
  
```tsql  
exec sys.sp_xtp_merge_checkpoint_files 'H_DB',  12345, 67890  
```  
  
 假設有三個資料和差異檔案組，每一組各有 15,836 個資料列及 5,279 個已刪除的資料列。 合併之後，新資料檔案的資料列數變為 31,872，已刪除的資料列變為 0。 新資料檔案的大小可能遠大於最初所配置的 128MB。 這是因為手動合併會覆寫合併原則，並強制合併所要求的檔案。  
  
 部落格[狀態轉換的檢查點檔案在資料庫中記憶體最佳化資料表搭配](http://blogs.technet.com/b/dataplatforminsider/archive/2014/01/23/state-transition-of-checkpoint-files-in-databases-with-memory-optimized-tables.aspx)描述狀態轉換的資料和差異檔案組從開始到記憶體回收。  
  
## <a name="see-also"></a>另請參閱  
 [建立及管理記憶體最佳化物件的儲存體](../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
