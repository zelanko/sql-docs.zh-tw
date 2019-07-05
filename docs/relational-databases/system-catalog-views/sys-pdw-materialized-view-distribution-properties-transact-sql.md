---
title: sys.pdw_materialized_view_distribution_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 165e143dd1293520c10596117128566a4197ef29
ms.sourcegitcommit: e4b241fd92689c2aa6e1f5e625874bd0b807dd01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2019
ms.locfileid: "67566630"
---
# <a name="syspdwmaterializedviewdistributionproperties-transact-sql-preview"></a>sys.pdw_materialized_view_distribution_properties (Transact-SQL) (preview)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

顯示發佈資訊具體化檢視。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------| 
|object_id|**int**|具體化檢視的三個屬性所指定的識別碼。| 
|distribution_policy |**tinyint**|2 = 雜湊</br>4 = ROUND_ROBIN|  
|distribution_policy_desc |**nvarchar(60)**|雜湊 ROUND_ROBIN|  
 
## <a name="permissions"></a>Permissions

需要 VIEW DATABASE STATE 權限。
 
## <a name="see-also"></a>另請參閱

[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure SQL 資料倉儲中支援的系統檢視表](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure SQL 資料倉儲中支援的 T-SQL 陳述式](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
