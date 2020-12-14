---
title: 'sys.pdw_permanent_table_mappings (Transact-sql) '
ms.custom: ''
ms.date: 07/24/2020
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: mstehrani
ms.author: emtehran
monikerRange: = azure-sqldw-latest
ms.openlocfilehash: d832c11ccf2090454a11fa3c913455d38aff84e6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97404290"
---
# <a name="syspdw_permanent_table_mappings-transact-sql"></a>sys.pdw_permanent_table_mappings (Transact-sql) 
[!INCLUDE [applies-to-version/asa](../../includes/applies-to-version/asa.md)]

  **Object_id** 將永久的使用者資料表系結至內建物件名稱。  
  
> [!NOTE]
> **sys.pdw_permanent_table_mappings** 保存永久資料表的對應，且不包含暫存或外部資料表對應。

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|physical_name|**Nvarchar (36)**|資料表的機構名稱。<br /><br /> **physical_name** 並 **object_id** 形成此視圖的索引鍵。||  
|object_id|**int**|資料表的物件識別碼。 請參閱 [sys. objects &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。<br /><br /> **physical_name** 並 **object_id** 形成此視圖的索引鍵。||  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.pdw_index_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)  
  
  
