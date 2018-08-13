---
title: sys.external_file_formats & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a89efb2c-0a3a-4b64-9284-6e93263e29ac
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: dea0275fbdeea5dc413d4fc69a1da224cd2a6a04
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39560518"
---
# <a name="sysexternalfileformats-transact-sql"></a>sys.external_file_formats & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  包含一個資料列的目前資料庫中每一個外部檔案格式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
 包含一個資料列的伺服器上的每一個外部檔案格式[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|外部檔案格式的物件識別碼。||  
|NAME|**sysname**|檔案格式的名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，這是唯一的資料庫。 在  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，這是唯一的伺服器。||  
|format_type|**tinyint**|檔案格式類型。|DELIMITEDTEXT，RCFILE、 ORC、 PARQUET|  
|field_terminator|**nvarchar(10)**|Format_type = DELIMITEDTEXT，這是將欄位結束字元。||  
|string_delimiter|**nvarchar(10)**|Format_type = DELIMITEDTEXT，此為字串分隔符號。||  
|date_format|**nvarchar(50)**|Format_type = DELIMITEDTEXT，這是使用者定義的日期和時間格式。||  
|use_type_default|**bit**|Format_type = 分隔的文字，會指定如何處理遺漏值，PolyBase 會從 HDFS 文字檔案，將項目匯入資料時[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。|0 – 會將遺漏的值儲存為 'NULL' 字串。<br /><br /> 1 – 將遺漏的值儲存為資料行預設值。|  
|serde_method|**nvarchar(255)**|Format_type = RCFILE，這是序列化/還原序列化方法。||  
|row_terminator|**nvarchar(10)**|Format_type = DELIMITEDTEXT，這是結束外部 Hadoop 檔案中的每個資料列的字元字串。|一律 ' \n。 '|  
|編碼|**nvarchar(10)**|Format_type = DELIMITEDTEXT，這是適用於外部 Hadoop 檔案編碼的方法。|一律 ' UTF8。 '|  
|data_compression|**nvarchar(255)**|外部資料的資料壓縮方法。|Format_type = DELIMITEDTEXT:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.GzipCodec'<br /><br /> Format_type = RCFILE:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br /><br /> Format_type = ORC:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'<br /><br /> Format_type = PARQUET:<br /><br /> -   'org.apache.hadoop.io.compress.GzipCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'|  
  
## <a name="permissions"></a>Permissions  
 目錄檢視內中繼資料的可見性會限制在使用者所擁有的安全性實體，或已授與使用者某些權限的安全性實體。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sys.external_data_sources &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [sys.external_tables &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
