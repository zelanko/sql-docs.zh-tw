---
description: 'sys.pdw_health_component_properties (Transact-sql) '
title: sys.pdw_health_component_properties (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: a6446cb81a33fef53ac398f9e23bd080b310ede4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439473"
---
# <a name="syspdw_health_component_properties-transact-sql"></a>sys.pdw_health_component_properties (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  儲存描述裝置的屬性。 某些屬性會顯示裝置狀態，而某些屬性會描述裝置本身。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|元件之屬性的唯一識別碼。<br /><br /> property_id 並 component_id 形成此視圖的索引鍵。|NOT NULL|  
|component_id|**int**|元件的識別碼。 請參閱 [sys.pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。<br /><br /> property_id 並 component_id 形成此視圖的索引鍵。|NOT NULL|  
|property_name|**nvarchar(255)**|屬性的名稱。|NOT NULL|  
|physical_name|**nvarchar(32)**|屬性名稱，如製造商所定義。|NOT NULL|  
|is_key|**bit**|判斷裝置實例是否唯一或不是唯一的。|NOT NULL<br /><br /> 0-裝置實例是唯一的。<br /><br /> 1-裝置實例不是唯一的。|  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
