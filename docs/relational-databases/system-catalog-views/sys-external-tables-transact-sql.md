---
title: sys.external_tables (TRANSACT-SQL) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054309"
---
# <a name="sysexternaltables-transact-sql"></a>sys.external_tables & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  包含針對目前資料庫中每個外部資料表的資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|\<繼承資料行 >||如需這個檢視所繼承的資料行的清單，請參閱 < [j &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。||  
|max_column_id_used|**int**|這份資料表用過的最大資料行識別碼。||  
|uses_ansi_nulls|**bit**|資料表是在 SET ANSI_NULLS 資料庫選項為 ON 的情況下加以建立。||  
|data_source_id|**int**|外部資料來源的物件識別碼。||  
|file_format_id|**int**|針對 HADOOP 的外部資料來源的外部資料表，這是外部檔案格式的物件識別碼。||  
|location|**nvarchar(4000)**|透過 HADOOP 的外部資料來源的外部資料表，這是 HDFS 中的外部資料的路徑。||  
|reject_type|**tinyint**|透過 HADOOP 的外部資料來源的外部資料表，這是查詢外部資料時，會計算已拒絕的資料列的方式。|值-已拒絕的資料列數目。<br /><br /> 百分比-已拒絕的資料列百分比。|  
|reject_value|**float**|透過 HADOOP 的外部資料來源的外部資料表：<br /><br /> 針對*reject_type =* 值，這是在查詢失敗之前，先允許的資料列被拒絕的次數。<br /><br /> 針對*reject_type* = percentage，這是在查詢失敗之前，先允許的資料列拒絕的百分比。||  
|reject_sample_value|**int**|針對*reject_type* = percentage，這是要載入，成功或失敗，然後才計算被拒絕的資料列百分比的資料列數目。|如果 reject_type = VALUE。|  
|distribution_type|**int**|針對 SHARD_MAP_MANAGER 的外部資料來源的外部資料表，這是基底資料表的資料列的資料分佈。|0-分區化<br /><br /> 1-複寫<br /><br /> 2-循環配置資源|  
|distribution_desc|**nvarchar(120)**|針對 SHARD_MAP_MANAGER 的外部資料來源的外部資料表，這是顯示為字串的散發類型。||  
|sharding_column_id|**int**|針對 SHARD_MAP_MANAGER 的外部資料來源和分區化分佈的外部資料表，這是包含分區化索引鍵值的資料行的資料行識別碼。||  
|remote_schema_name|**sysname**|針對 SHARD_MAP_MANAGER 的外部資料來源的外部資料表，這是基底資料表 （如果不同於其中定義外部資料表的結構描述） 在遠端資料庫所呈現的所在的結構描述。||  
|remote_object_name|**sysname**|針對 SHARD_MAP_MANAGER 的外部資料來源的外部資料表，這是在遠端資料庫 （如果與外部資料表的名稱不同） 的基底資料表的名稱。||  
  
## <a name="permissions"></a>Permissions  
 目錄檢視內中繼資料的可見性會限制在使用者所擁有的安全性實體，或已授與使用者某些權限的安全性實體。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sys.external_file_formats &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [sys.external_data_sources &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  
