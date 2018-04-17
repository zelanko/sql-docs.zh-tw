---
title: sys.all_columns (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- all_columns_TSQL
- all_columns
- sys.all_columns_TSQL
- sys.all_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_columns catalog view
ms.assetid: 40e04fe9-0b64-4799-84c0-57f128b2bdc2
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 93f61e8ae7e9835a9dca3469b5050b4751c51805
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysallcolumns-transact-sql"></a>sys.all_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  顯示屬於使用者自訂物件和系統物件之所有資料行的聯集。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|這個資料行所屬的物件識別碼。|  
|name|**sysname**|資料行的名稱。 在物件中，這是唯一的。|  
|column_id|**int**|資料行的識別碼。 在物件中，這是唯一的。<br /><br /> 資料行識別碼不一定會循序排列。|  
|system_type_id|**tinyint**|資料行的系統類型識別碼。|  
|user_type_id|**int**|使用者所定義的資料行類型識別碼。<br /><br /> 若要傳回的型別名稱，加入[sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)目錄檢視這個資料行。|  
|max_length|**smallint**|資料行的最大長度 (以位元組為單位)。<br /><br /> -1 = 資料行資料類型是**varchar （max)**， **nvarchar （max)**， **varbinary （max)**，或**xml**。<br /><br /> 如**文字**資料行，max_length 值就是 16，或是由 sp_tableoption 'text in row' 所設定的值。|  
|有效位數|**tinyint**|如果是以數值為基礎，便是資料行的有效位數；否則，便是 0。|  
|scale|**tinyint**|如果是以數值為基礎，便是資料行的小數位數；否則，便是 0。|  
|collation_name|**sysname**|如果是以字元為基礎，便是資料行的定序名稱；否則，便是 NULL。|  
|is_nullable|**bit**|1 = 資料行可為 Null。|  
|is_ansi_padded|**bit**|1 = 如果是字元、二進位或變數，則資料行會使用 ANSI_PADDING ON 行為。<br /><br /> 0 = 資料行不是字元、二進位或變數。|  
|is_rowguidcol|**bit**|1 = 資料行是已宣告的 ROWGUIDCOL。|  
|is_identity|**bit**|1 = 資料行有識別值|  
|is_computed|**bit**|1 = 資料行是一個計算資料行。|  
|is_filestream|**bit**|1 = 宣告資料行使用檔案資料流儲存體。|  
|is_replicated|**bit**|1 = 資料行已被複寫。|  
|is_non_sql_subscribed|**bit**|1 = 資料行有非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的訂閱者。|  
|is_merge_published|**bit**|1 = 資料行已經合併發行。|  
|is_dts_replicated|**bit**|1 = 資料行是利用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 加以複寫。|  
|is_xml_document|**bit**|1 = 內容是完整的 XML 文件集。<br /><br /> 0 = 內容是文件片段，或者資料行資料類型不是 XML。|  
|xml_collection_id|**int**|非零的資料行資料類型是否**xml**且 XML 具備類型。 這個值是包含資料行的驗證 XML 結構描述命名空間之集合的識別碼。<br /><br /> 0 = 沒有 XML 結構描述集合。|  
|default_object_id|**int**|預設物件，無論它是獨立的識別碼[sys.sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)，或內嵌、 資料行層級 DEFAULT 條件約束。 內嵌資料行層級預設物件的 parent_object_id 資料行，就是資料表本身的參考。<br /><br /> 0 = 沒有預設值。|  
|rule_object_id|**int**|獨立規則的識別碼，這個規則是利用 sys.sp_bindrule 與資料行繫結。<br /><br /> 0 = 沒有獨立規則。<br /><br /> 資料行層級 CHECK 條件約束，請參閱[sys.check_constraints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)。|  
|is_sparse|bit|1 = 資料行是疏鬆資料行。 如需詳細資訊，請參閱 [使用疏鬆資料行](../../relational-databases/tables/use-sparse-columns.md)。|  
|is_column_set|bit|1 = 資料行是資料行集。 如需詳細資訊，請參閱 [使用資料行集](../../relational-databases/tables/use-column-sets.md)。|  
|將 generated_always_type|**tinyint**|**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 數字的值，表示資料行的類型：<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END|  
|generated_always_type_desc|**nvarchar(60)**|**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 文字描述的資料行的類型：<br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.system_columns &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)  
  
  
