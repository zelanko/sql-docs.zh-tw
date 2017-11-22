---
title: "sys.external_file_formats (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: a89efb2c-0a3a-4b64-9284-6e93263e29ac
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 46ac5d27d81c1e8162981340115e563d1e1c3991
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysexternalfileformats-transact-sql"></a>sys.external_file_formats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  包含目前資料庫中每個外部檔案格式的資料列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
 包含在伺服器上為每個外部檔案格式的資料列[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|外部檔案格式的物件識別碼。||  
|name|**sysname**|檔案格式的名稱。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，這是唯一的資料庫。 在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，這是唯一的伺服器。||  
|format_type|**tinyint**|檔案格式類型。|DELIMITEDTEXT、 RCFILE、 ORC，PARQUET|  
|field_terminator|**nvarchar （10)**|Format_type = DELIMITEDTEXT，這是欄位結束字元。||  
|string_delimiter|**nvarchar （10)**|Format_type = DELIMITEDTEXT，此為字串分隔符號。||  
|date_format|**nvarchar(50)**|Format_type = DELIMITEDTEXT，這是使用者定義的日期和時間格式。||  
|use_type_default|**bit**|Format_type = 分隔的文字，會指定如何處理遺漏值，PolyBase 從 HDFS 文字檔案，將項目匯入資料時[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。|0 – 會將遺漏的值儲存為字串 'NULL'。<br /><br /> 1 – 遺漏的值儲存為資料行預設值。|  
|serde_method|**nvarchar(255)**|Format_type = RCFILE，這是序列化/還原序列化方法。||  
|row_terminator|**nvarchar （10)**|Format_type = DELIMITEDTEXT，這是結束外部的 Hadoop 檔案中的每個資料列的字元字串。|一律 ' \n。 '|  
|編碼|**nvarchar （10)**|Format_type = DELIMITEDTEXT，這是外部的 Hadoop 檔案的編碼方式。|一律 ' UTF8。 '|  
|data_compression|**nvarchar(255)**|外部資料的資料壓縮方法。|Format_type = DELIMITEDTEXT:<br /><br /> -'org.apache.hadoop.io.compress.DefaultCodec'<br />-'org.apache.hadoop.io.compress.GzipCodec'<br /><br /> Format_type = RCFILE:<br /><br /> -'org.apache.hadoop.io.compress.DefaultCodec'<br /><br /> Format_type = ORC:<br /><br /> -'org.apache.hadoop.io.compress.DefaultCodec'<br />-'org.apache.hadoop.io.compress.SnappyCodec'<br /><br /> Format_type = PARQUET:<br /><br /> -'org.apache.hadoop.io.compress.GzipCodec'<br />-'org.apache.hadoop.io.compress.SnappyCodec'|  
  
## <a name="permissions"></a>Permissions  
 目錄檢視內中繼資料的可見性會限制在使用者所擁有的安全性實體，或已授與使用者某些權限的安全性實體。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [sys.external_data_sources &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [sys.external_tables &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
