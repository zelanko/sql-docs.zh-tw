---
description: 'sys.dm_pdw_component_health_status (Transact-sql) '
title: sys.dm_pdw_component_health_status (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 68cc3f7a-693c-4d5d-a76b-455352af8d7f
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: 6c525237b8e2cf92eef038f3cdfe668c8b87af49
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482609"
---
# <a name="sysdm_pdw_component_health_status-transact-sql"></a>sys.dm_pdw_component_health_status (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  保存設備元件目前健康情況的相關資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**||非 NULL|  
|component_id|int|元件的識別碼。 請參閱 [sys.pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。<br /><br /> pdw_node_id、component_id、property_id 和 component_instance_id 會形成此視圖的索引鍵。|非 NULL|  
|property_id|**int**|屬性的識別碼。 請參閱 [sys.pdw_health_component_properties &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md)。|NOT NULL|  
|component_instance_id|**nvarchar(255)**|識別元件的實例。 例如，CPU 的實例可能會由 component_instance_id = ' CPU1 ' 識別。<br /><br /> pdw_node_id、component_id、property_id 和 component_instance_id 會形成此視圖的索引鍵。|NOT NULL|  
|property_value|**nvarchar(255)**|目前的屬性值。|NULL|  
|update_time|**datetime**|上次更新度量的時間。|NOT NULL|  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
