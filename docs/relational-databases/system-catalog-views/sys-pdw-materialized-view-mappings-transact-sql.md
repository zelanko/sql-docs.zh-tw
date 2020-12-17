---
description: 'sys.pdw_materialized_view_mappings (Transact-sql) '
title: sys.pdw_materialized_view_mappings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest
ms.openlocfilehash: 5d09d97fe51acec8466bcff8f64c3edfbc9316e2
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/17/2020
ms.locfileid: "97642380"
---
# <a name="syspdw_materialized_view_mappings-transact-sql"></a>sys.pdw_materialized_view_mappings (Transact-sql)   

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Object_id 將具體化視圖系結至內建物件名稱。

Physical_name 和 object_id 的資料行會形成此目錄檢視的索引鍵。
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|physical_name |**Nvarchar (36)**|具體化視圖的機構名稱。|  
|object_id  |**int**|具體化視圖的物件識別碼。 請參閱 [sys. objects (transact-sql) ](./sys-objects-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)。| 

## <a name="permissions"></a>權限

需要 VIEW DATABASE STATE 權限。
  
## <a name="see-also"></a>另請參閱

[使用具體化檢視進行效能調整](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-materialized-view-as-select-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-materialized-view-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[EXPLAIN &#40;Transact-SQL&#41;](../../t-sql/queries/explain-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](./sys-pdw-materialized-view-column-distribution-properties-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](./sys-pdw-materialized-view-distribution-properties-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[Azure Synapse Analytics 和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure Synapse Analytics 中支援的系統檢視](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure Synapse Analytics 中支援的 T-SQL 陳述式](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)