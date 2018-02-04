---
title: "sys.external_tables (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: fac4720c-b679-4ab2-864b-ff7810a9b559
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c261068e68503ff01429c3b215261dffcb48053
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysexternaltables-transact-sql"></a>sys.external_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  包含目前資料庫中每個外部資料表的資料列。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|\<繼承資料行 >||如需這個檢視所繼承的資料行的清單，請參閱[sys.objects &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).||  
|max_column_id_used|**int**|此資料表用過的最大資料行識別碼。||  
|uses_ansi_nulls|**bit**|資料表是在 SET ANSI_NULLS 資料庫選項為 ON 的情況下加以建立。||  
|data_source_id|**int**|外部資料來源的物件識別碼。||  
|file_format_id|**int**|HADOOP 的外部資料來源的外部資料表，這是外部檔案格式的物件識別碼。||  
|location|**nvarchar(4000)**|透過 HADOOP 的外部資料來源的外部資料表，這是在 HDFS 中的外部資料的路徑。||  
|reject_type|**tinyint**|對於透過 HADOOP 的外部資料來源的外部資料表，這是查詢外部資料時，會計算已拒絕的資料列的方式。|值 – 已拒絕的資料列數目。<br /><br /> 百分比 – 已拒絕的資料列百分比。|  
|reject_value|**float**|透過 HADOOP 的外部資料來源的外部資料表：<br /><br /> 如*reject_type =*值，這是資料列之拒絕的查詢失敗之前，先允許的數目。<br /><br /> 如*reject_type* = 百分比，這是查詢失敗之前，先允許的資料列之拒絕的百分比。||  
|reject_sample_value|**int**|如*reject_type* = 百分比，這是要載入，成功或失敗，然後再計算已拒絕的資料列百分比的資料列數目。|如果 reject_type = VALUE。|  
|distribution_type|**int**|透過對包含 SHARD_MAP_MANAGER 外部資料來源的外部資料表，這是基底資料表的資料列的資料分佈。|0 – Sharded<br /><br /> 1 – 複寫<br /><br /> 2 – 循環配置資源|  
|distribution_desc|**nvarchar(120)**|透過對包含 SHARD_MAP_MANAGER 外部資料來源的外部資料表，這是顯示為字串的散發類型。||  
|sharding_column_id|**int**|透過對包含 SHARD_MAP_MANAGER 外部資料來源和分區化分佈的外部資料表，這是包含分區化索引鍵值的資料行的資料行識別碼。||  
|remote_schema_name|**sysname**|透過對包含 SHARD_MAP_MANAGER 外部資料來源的外部資料表，這是遠端的資料庫 （如果不同於其中定義外部資料表的結構描述） 的基底資料表所在的結構描述。||  
|remote_object_name|**sysname**|透過對包含 SHARD_MAP_MANAGER 外部資料來源的外部資料表，這是遠端的資料庫 （如果與外部資料表的名稱不同） 的基底資料表的名稱。||  
  
## <a name="permissions"></a>Permissions  
 目錄檢視內中繼資料的可見性會限制在使用者所擁有的安全性實體，或已授與使用者某些權限的安全性實體。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [sys.external_data_sources &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  
