---
title: "sys.spatial_indexes (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.spatial_indexes_TSQL
- spatial_indexes
- spatial_indexes_TSQL
- sys.spatial_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_indexes catalog view
ms.assetid: 40e967d5-2e8d-45af-bf5e-5251493cf7cb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 709c692ed9eacf6307995d7273eb5a7a2e906580
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="sysspatialindexes-transact-sql"></a>sys.spatial_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  表示空間索引的主要索引資訊。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|\<繼承資料行 >||繼承資料行從[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。|  
|spatial_index_type|**tinyint**|空間索引的類型：<br /><br /> 1 = 幾何空間索引<br /><br /> 2 = 地理空間索引|  
|spatial_index_type_desc|**nvarchar （60)**|輸入空間索引的描述：<br /><br /> GEOMETRY = 幾何空間索引<br /><br /> GEOGRAPHY = 地理空間索引|  
|tessellation_scheme|**sysname**|鑲嵌式配置的名稱：<br /><br /> GEOMETRY_GRID、GEOMETRY_AUTO_GRID、<br /><br /> GEOGRAPHY_GRID、GEOGRAPHY_AUTO_GRID<br /><br /> 注意： 如需有關鑲嵌式配置資訊，請參閱[空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)。|  
|\<繼承資料行 >||繼承資料行從[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。<br /><br /> 繼承的資料行 has_filter 和 filter_definition 會出現在空間索引特有的資料行後面。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>請參閱  
 [sys.objects &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_index_tessellations &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
