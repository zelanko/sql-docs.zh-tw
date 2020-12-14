---
description: 'sys.pdw_nodes_tables (Transact-sql) '
title: sys.pdw_nodes_tables (Transact-sql) |Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: aeaa545dd0658900b6cca8f17ec153ac1b6f25bb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97404408"
---
# <a name="syspdw_nodes_tables-transact-sql"></a>sys.pdw_nodes_tables (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  針對主體所擁有的每個資料表物件，以及已授與主體某些許可權的資料表物件，各包含一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|\<inherited columns>||如需此視圖所繼承之資料行的清單，請參閱 [sys. objects](../system-catalog-views/sys-objects-transact-sql.md)。||  
|lob_data_space_id|**int**||一律是 0。|  
|filestream_data_space_id|**int**|FILESTREAM 檔案群組或的資料空間識別碼 [!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|NULL|  
|max_column_id_used|**int**|此資料表所使用的最大資料行識別碼。||  
|lock_on_bulk_load|**bit**|資料表在大量載入時會予以鎖定。|TBD|  
|uses_ansi_nulls|**bit**|資料表是在 SET ANSI_NULLS 資料庫選項為 ON 的情況下加以建立。|1|  
|is_replicated|**bit**|1 = 使用複寫發行資料表。|0不支援複寫。|  
|has_replication_filter|**bit**|1 = 資料表有一項複寫篩選。|0|  
|is_merge_published|**bit**|1 = 資料表是利用合併式複寫來發行。|0不支援。|  
|is_sync_tran_subscribed|**bit**|1 = 資料表是利用立即更新訂閱來訂閱。|0不支援。|  
|has_unchecked_assembly_data|**bit**|1 = 資料表包含保存資料，這些保存資料會隨著上次 ALTER ASSEMBLY 期間變更定義的組件而不同。 在下次 DBCC CHECKDB 或 DBCC CHECKTABLE 順利完成之後，將重設為 0。|0沒有 CLR 支援。|  
|text_in_row_limit|**int**|0 = 未設定 "text in row" 選項。|一律是 0。|  
|large_value_types_out_of_row|**bit**|1 = 大數值類型是以 out-of-row 的方式來儲存。|一律是 0。|  
|is_tracked_by_cdc|**bit**|1 = 資料表已啟用變更資料捕獲|一律為 0;沒有 CDC 支援。|  
|lock_escalation|**tinyint**|資料表的 LOCK_ESCALATION 選項值： 2 = AUTO|一律為2。|  
|lock_escalation_desc|**nvarchar(60)**|Lock_escalation 選項的文字描述。|一律ꞌ自動ꞌ。|  
|pdw_node_id|**int**|節點的唯一識別碼 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。|NOT NULL|  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
