---
title: sys.index_resumable_operations (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 07/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: ''
caps.latest.revision: 1
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0d0da28f06dc079d468b2b8862855e1e2f957540
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43076945"
---
# <a name="indexresumableoperations-transact-sql"></a>index_resumable_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**sys.index_resumable_operations**檢視由系統監視，並檢查目前的執行狀態，可繼續索引重建。  
**適用於**: SQL Server 2017 和 Azure SQL Database 
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|此索引所屬 (不可為 null) 的物件識別碼。|  
|**index_id**|**int**|(不可為 null) 索引的識別碼。 **index_id**只有在該物件是唯一。|
|**name**|**sysname**|索引的名稱。 **名稱**只有在該物件是唯一。|  
|**sql_text**|**nvarchar(max)**|DDL T-SQL 陳述式文字|
|**last_max_dop**|**smallint**|最後一個 max_dop 會固定使用 (預設 = 0)|
|**partition_number**|**int**|擁有索引或堆積內的資料分割編號。 非資料分割資料表和索引，或在案例中的所有磁碟分割正在重建這個資料行的值 NULL。|
|**state**|**tinyint**|可繼續索引作業的狀態：<br /><br />0 = 正在執行<br /><br />1 = 暫停|
|**state_desc**|**nvarchar(60)**|操作狀態 （執行或暫停） 的可繼續索引的描述|  
|**start_time**|**datetime**|索引作業開始時間 (不可為 null)|
|**last_pause_time**|**日期時間**| 索引作業 (可為 null) 的上次暫停時間。 如果作業執行，而且永遠不會暫停，則為 NULL。|
|**total_execution_time**|**int**|從以分鐘為單位 (不可為 null) 的開始時間的總執行時間|
|**percent_complete**|**real**|索引作業的進度完成，在 %(不可為 null)。|
|**page_count**|**bigint**|新的索引建立作業和 (不可為 null) 的對應索引配置的索引頁的總數。 

## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
   
## <a name="example"></a>範例  
 列出所有處於暫停狀態的可繼續索引重建作業。 
  
```  
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```  
  
## <a name="see-also"></a>另請參閱 
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)    
 [目錄檢視&#40;TRANSACT-SQL&#41; ](catalog-views-transact-sql.md) [物件目錄檢視&#40;-&#41; ](object-catalog-views-transact-sql.md) [sys.indexes &#40;-&#41; ](sys-xml-indexes-transact-sql.md) [sys.index_columns &#40;TRANSACT-SQL&#41;](sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40;Transact-SQL&#41;](sys-xml-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](sys-index-columns-transact-sql.md)   
 [sys.key_constraints &#40;-SQL&AMP;#41;&#41;](sys-key-constraints-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](sys-filegroups-transact-sql.md)   
 [sys.partition_schemes &#40;Transact-SQL&#41;](sys-partition-schemes-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](querying-the-sql-server-system-catalog-faq.md)   
  
