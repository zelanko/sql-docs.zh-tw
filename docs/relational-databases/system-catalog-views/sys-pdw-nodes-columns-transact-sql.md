---
title: sys.databases pdw_nodes_columns （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 268c77b7-1d71-4197-a2ed-5e2b2b8fc260
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 201af9001703bb8f1dfbdaf2c41151697b945df3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68059397"
---
# <a name="syspdw_nodes_columns-transact-sql"></a>sys.databases pdw_nodes_columns （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  顯示使用者定義資料表和使用者定義之視圖的資料行。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|這個資料行所屬的物件識別碼。||  
|NAME|**sysname**|資料行的名稱。 物件中唯一的。||  
|column_id|**int**|資料行的識別碼。 物件中唯一的。||  
|system_type_id|**tinyint**|資料行的系統類型識別碼。||  
|user_type_id|**int**|使用者所定義的資料行類型識別碼。||  
|max_length|**smallint**|資料行的最大長度 (以位元組為單位)。|針對不支援的資料行類型包含-1 （無效）。|  
|precision|**tinyint**|如果是以數值為基礎，便是資料行的有效位數；否則，便是 0。||  
|級別|**tinyint**|如果是以數值為基礎，便是資料行的小數位數；否則，便是 0。||  
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
|is_dts_replicated|**bit**|1 = 資料行是使用 SSIS 進行複寫。|一律是 0。|  
|is_xml_document|**bit**|1 = 內容是完整的 XML 文件集。|一律是 0。|  
|xml_collection_id|**int**|0 = 沒有 XML 結構描述集合。|一律是 0。|  
|default_object_id|**int**|預設物件的識別碼;0 = 沒有預設值。|一律是 0。|  
|rule_object_id|**int**|系結至資料行之獨立規則的識別碼。 <br />0 = 沒有獨立規則。|一律是 0。|  
|is_sparse|**bit**|1 = 資料行是疏鬆資料行。|一律是 0。|  
|is_column_set|**bit**|1 = 資料行是資料行集。|一律是 0。|  
|pdw_node_id|**int**|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]節點的唯一識別碼。|NOT NULL|  
  
## <a name="permissions"></a>權限  
 需要 CONTROL SERVER 權限。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [all_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)  
  
  
