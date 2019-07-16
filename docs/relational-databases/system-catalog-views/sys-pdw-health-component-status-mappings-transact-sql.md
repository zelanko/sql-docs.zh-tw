---
title: sys.pdw_health_component_status_mappings (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ec631e9008cc37a7b4f91ed3f530e5388bdf9c0d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127504"
---
# <a name="syspdwhealthcomponentstatusmappings-transact-sql"></a>sys.pdw_health_component_status_mappings & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  定義之間的對應[!INCLUDE[ssDW](../../includes/ssdw-md.md)]元件狀態和製造商定義的元件名稱。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|屬性的唯一識別碼。<br /><br /> 屬性識別碼 」、 「 component_id，與 「 physical_name 構成此檢視的索引鍵。|NOT NULL|  
|component_id|**int**|元件的識別碼。 請參閱[sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。<br /><br /> 屬性識別碼 」、 「 component_id，與 「 physical_name 構成此檢視的索引鍵。|NOT NULL|  
|physical_name|**nvarchar(32)**|製造商所定義的屬性名稱。<br /><br /> 屬性識別碼 」、 「 component_id，與 「 physical_name 構成此檢視的索引鍵。|NOT NULL|  
|logical_name|**nvarchar(255)**|所定義的屬性名稱[!INCLUDE[ssDW](../../includes/ssdw-md.md)]。|NOT NULL<br /><br /> 0-裝置執行個體是唯一的。<br /><br /> 1-裝置執行個體不是唯一的。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
