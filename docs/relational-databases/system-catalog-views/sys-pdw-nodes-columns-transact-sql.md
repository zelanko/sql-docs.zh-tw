---
title: sys.pdw_nodes_columns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 268c77b7-1d71-4197-a2ed-5e2b2b8fc260
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3316f6325cda3ad7683337ef4d5929e1e5369fb2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="syspdwnodescolumns-transact-sql"></a>sys.pdw_nodes_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  顯示使用者定義的資料表和使用者定義的檢視表的資料行。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|這個資料行所屬的物件識別碼。||  
|name|**sysname**|資料行的名稱。 物件中是唯一的。||  
|column_id|**int**|資料行的識別碼。 物件中是唯一的。||  
|system_type_id|**tinyint**|資料行的系統類型識別碼。||  
|user_type_id|**int**|使用者所定義的資料行類型識別碼。||  
|max_length|**smallint**|資料行的最大長度 (以位元組為單位)。|包含傳回-1 （不正確） 不支援的資料行類型。|  
|有效位數|**tinyint**|如果是以數值為基礎，便是資料行的有效位數；否則，便是 0。||  
|scale|**tinyint**|如果是以數值為基礎，便是資料行的小數位數；否則，便是 0。||  
|collation_name|**sysname**|如果是以字元為基礎，便是資料行的定序名稱；否則，便是 NULL。||  
|is_nullable|**bit**|1 = 資料行可為 Null。||  
|is_ansi_padded|**bit**|1 = 如果是字元、二進位或變數，則資料行會使用 ANSI_PADDING ON 行為。|一律是 0。|  
|is_rowguidcol|**bit**|1 = 資料行是已宣告的 ROWGUIDCOL。|一律是 0。|  
|is_identity|**bit**|1 = 資料行有識別值。|一律是 0。|  
|is_computed|**bit**|1 = 資料行是一個計算資料行。|一律是 0。|  
|is_filestream|**bit**|1 = 資料行是 FILESTREAM 資料行。|一律是 0。|  
|is_replicated|**bit**|1 = 資料行已被複寫。|一律是 0。|  
|is_non_sql_subscribed|**bit**|1 = 資料行有非 SQL 訂閱者。|一律是 0。|  
|is_merge_published|**bit**|1 = 資料行已經合併發行。|一律是 0。|  
|is_dts_replicated|**bit**|1 = 使用 SSIS 來複寫資料行。|一律是 0。|  
|is_xml_document|**bit**|1 = 內容是完整的 XML 文件集。|一律是 0。|  
|xml_collection_id|**int**|0 = 沒有 XML 結構描述集合。|一律是 0。|  
|default_object_id|**int**|與預設物件的識別碼0 = 沒有預設值。|一律是 0。|  
|rule_object_id|**int**|獨立規則繫結至資料行的識別碼。 <br />0 = 沒有獨立規則。|一律是 0。|  
|is_sparse|**bit**|1 = 資料行是疏鬆資料行。|一律是 0。|  
|is_column_set|**bit**|1 = 資料行是資料行集。|一律是 0。|  
|pdw_node_id|**int**|唯一識別項[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]節點。|NOT NULL|  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 權限。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)  
  
  
