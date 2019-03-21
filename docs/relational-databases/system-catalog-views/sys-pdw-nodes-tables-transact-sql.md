---
title: sys.pdw_nodes_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 473b5d14-171b-4a16-9195-acf36d3f786c
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: fcef927616bf90dcbf66639553d34ceaa78bb9e9
ms.sourcegitcommit: 7d4a3fc0f2622cbc6930d792be4a9b3fcac4c4b6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2019
ms.locfileid: "58305926"
---
# <a name="syspdwnodestables-transact-sql"></a>sys.pdw_nodes_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含主體所擁有，或已授與主體某些權限的每個資料表物件的資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|\<繼承資料行 >||如需這個檢視所繼承的資料行的清單，請參閱 < [sys.objects](../system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。||  
|lob_data_space_id|**int**||一律是 0。|  
|filestream_data_space_id|**int**|資料空間識別碼是 FILESTREAM 檔案群組或 [!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|NULL|  
|max_column_id_used|**int**|此資料表所使用的最大資料行識別碼。||  
|lock_on_bulk_load|**bit**|資料表在大量載入時會予以鎖定。|TBD|  
|uses_ansi_nulls|**bit**|資料表是在 SET ANSI_NULLS 資料庫選項為 ON 的情況下加以建立。|1|  
|is_replicated|**bit**|1 = 資料表使用複寫發行。|0;不支援複寫。|  
|has_replication_filter|**bit**|1 = 資料表有一項複寫篩選。|0|  
|is_merge_published|**bit**|1 = 資料表是利用合併式複寫來發行。|0;不支援。|  
|is_sync_tran_subscribed|**bit**|1 = 資料表是利用立即更新訂閱來訂閱。|0;不支援。|  
|has_unchecked_assembly_data|**bit**|1 = 資料表包含保存資料，這些保存資料會隨著上次 ALTER ASSEMBLY 期間變更定義的組件而不同。 在下次 DBCC CHECKDB 或 DBCC CHECKTABLE 順利完成之後，將重設為 0。|0;不是支援的 CLR。|  
|text_in_row_limit|**int**|0 = 未設定 "text in row" 選項。|一律是 0。|  
|large_value_types_out_of_row|**bit**|1 = 大數值類型是以 out-of-row 的方式來儲存。|一律是 0。|  
|is_tracked_by_cdc|**bit**|1 = 資料表啟用異動資料擷取|永遠為 0;沒有 CDC 的支援。|  
|lock_escalation|**tinyint**|資料表之 LOCK_ESCALATION 選項的值：2 = AUTO|一律是 2。|  
|lock_escalation_desc|**nvarchar(60)**|Lock_escalation 選項的文字描述。|一律 ꞌAUTOꞌ。|  
|pdw_node_id|**int**|唯一識別碼[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]節點。|NOT NULL|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
