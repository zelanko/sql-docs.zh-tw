---
title: sys.databases external_file_formats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a89efb2c-0a3a-4b64-9284-6e93263e29ac
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eae119fe16b916f47f1acdcd2ebe15efd96e51e9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68048394"
---
# <a name="sysexternal_file_formats-transact-sql"></a>sys.databases external_file_formats （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  針對[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、和[!INCLUDE[ssSDS](../../includes/sssds-md.md)] [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，在目前資料庫中的每個外部檔案格式各包含一個資料列。  
  
 針對伺服器上的每個外部檔案格式，各包含[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|外部檔案格式的物件識別碼。||  
|NAME|**sysname**|檔案格式的名稱。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]中，這對資料庫而言是唯一的。 在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中，這對伺服器而言是唯一的。||  
|format_type|**tinyint**|檔案格式類型。|DELIMITEDTEXT、RCFILE、ORC、PARQUET|  
|field_terminator|**Nvarchar （10）**|對於 format_type = DELIMITEDTEXT，這是欄位結束字元。||  
|string_delimiter|**Nvarchar （10）**|對於 format_type = DELIMITEDTEXT，這是字串分隔符號。||  
|date_format|**nvarchar(50)**|針對 format_type = DELIMITEDTEXT，這是使用者定義的日期和時間格式。||  
|use_type_default|**bit**|針對 format_type = 分隔文字，指定當 PolyBase 將資料從 HDFS 文字檔匯入到[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]時，如何處理遺漏值。|0-儲存遺漏的值做為字串 ' Null '。<br /><br /> 1-儲存遺漏值做為資料行的預設值。|  
|serde_method|**nvarchar(255)**|對於 format_type = RCFILE，這是序列化/還原序列化方法。||  
|row_terminator|**Nvarchar （10）**|針對 format_type = DELIMITEDTEXT，這是在外部 Hadoop 檔案中終止每個資料列的字元字串。|一律為 ' \n '。|  
|編碼|**Nvarchar （10）**|針對 format_type = DELIMITEDTEXT，這是外部 Hadoop 檔案的編碼方法。|一律為 ' UTF8 '。|  
|data_compression|**nvarchar(255)**|外部資料的資料壓縮方法。|針對 format_type = DELIMITEDTEXT：<br /><br /> -' Org.apache.hadoop.io.compress.defaultcodec ' 的-'<br />-' Org.apache.hadoop.io.compress.gzipcodec ' 的-'<br /><br /> 針對 format_type = RCFILE：<br /><br /> -' Org.apache.hadoop.io.compress.defaultcodec ' 的-'<br /><br /> 針對 format_type = ORC：<br /><br /> -' Org.apache.hadoop.io.compress.defaultcodec ' 的-'<br />-' Org.apache.hadoop.io.compress.snappycodec ' 的-'<br /><br /> 針對 format_type = PARQUET：<br /><br /> -' Org.apache.hadoop.io.compress.gzipcodec ' 的-'<br />-' Org.apache.hadoop.io.compress.snappycodec ' 的-'|  
  
## <a name="permissions"></a>權限  
 目錄檢視內中繼資料的可見性會限制在使用者所擁有的安全性實體，或已授與使用者某些權限的安全性實體。  如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [external_data_sources &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [external_tables &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
