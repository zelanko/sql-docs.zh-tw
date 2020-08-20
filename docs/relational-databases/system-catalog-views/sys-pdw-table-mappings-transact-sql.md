---
description: 'sys. pdw_table_mappings (Transact-sql) '
title: sys. pdw_table_mappings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/01/2018
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1af14fe0-e562-4f48-a7f0-783f300a88ac
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 50d2a8869ea5eec3f8a0dcd560f1fa7ef0be59e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475337"
---
# <a name="syspdw_table_mappings-transact-sql"></a>sys. pdw_table_mappings (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  **Object_id**將使用者資料表系結至內建物件名稱。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|physical_name|**Nvarchar (36) **|資料表的機構名稱。<br /><br /> **physical_name** 並 **object_id** 形成此視圖的索引鍵。||  
|object_id|**int**|資料表的物件識別碼。 請參閱 [sys. objects &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。<br /><br /> **physical_name** 並 **object_id** 形成此視圖的索引鍵。||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys. pdw_index_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)   
 [sys. pdw_database_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  
