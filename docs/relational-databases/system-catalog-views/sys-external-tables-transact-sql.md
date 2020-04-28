---
title: sys.databases external_tables （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: fac4720c-b679-4ab2-864b-ff7810a9b559
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c26dbafb76ecf318fa497e11ccac09e800691900
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68054309"
---
# <a name="sysexternal_tables-transact-sql"></a>sys.databases external_tables （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  針對目前資料庫中的每個外部資料表，各包含一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|\<繼承的資料行>||如需此視圖所繼承之資料行的清單，請參閱[sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。||  
|max_column_id_used|**int**|此資料表過去使用的最大資料行識別碼。||  
|uses_ansi_nulls|**bit**|資料表是在 SET ANSI_NULLS 資料庫選項為 ON 的情況下加以建立。||  
|data_source_id|**int**|外部資料源的物件識別碼。||  
|file_format_id|**int**|針對 HADOOP 外部資料源的外部資料表，這是外部檔案格式的物件識別碼。||  
|location|**nvarchar(4000)**|針對 HADOOP 外部資料源的外部資料表，這是 HDFS 中外部資料的路徑。||  
|reject_type|**tinyint**|若是透過 HADOOP 外部資料源的外部資料表，這就是在查詢外部資料時，拒絕的資料列計數的方式。|VALUE-拒絕的資料列數目。<br /><br /> 百分比-拒絕的資料列百分比。|  
|reject_value|**float**|針對 HADOOP 外部資料源的外部資料表：<br /><br /> 針對*reject_type =* value，這是在查詢失敗前允許的資料列拒絕次數。<br /><br /> 針對*reject_type* = 百分比，這是在查詢失敗前允許的資料列拒絕百分比。||  
|reject_sample_value|**int**|針對*reject_type* = 百分比，這是要在計算已拒絕的資料列百分比之前，成功或未成功載入的資料列數目。|如果 reject_type = 值，則為 Null。|  
|distribution_type|**int**|若是透過 SHARD_MAP_MANAGER 外部資料源的外部資料表，這就是跨基礎基表的資料列資料散發。|0-分區化<br /><br /> 1-已複寫<br /><br /> 2-迴圈配置資源|  
|distribution_desc|**nvarchar(120)**|若是透過 SHARD_MAP_MANAGER 外部資料源的外部資料表，這是顯示為字串的散發類型。||  
|sharding_column_id|**int**|對於透過 SHARD_MAP_MANAGER 外部資料源和分區化散發的外部資料表，這是包含分區化索引鍵值之資料行的資料行識別碼。||  
|remote_schema_name|**sysname**|若是透過 SHARD_MAP_MANAGER 外部資料源的外部資料表，這就是基表所在的架構（如果不同于定義外部資料表的架構）。||  
|remote_object_name|**sysname**|若是透過 SHARD_MAP_MANAGER 外部資料源的外部資料表，這就是遠端資料庫上的基表名稱（如果不同于外部資料表的名稱）。||  
  
## <a name="permissions"></a>權限  
 目錄檢視內中繼資料的可見性會限制在使用者所擁有的安全性實體，或已授與使用者某些權限的安全性實體。  如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [external_file_formats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [external_data_sources &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  
