---
description: 'sys. dm_pdw_component_health_active_alerts (Transact-sql) '
title: sys. dm_pdw_component_health_active_alerts (Transact-sql
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: c53e4a36-b841-424a-b8e2-255b1878deb6
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9ce9818d2544cfc1a2e97dedb24934b4ea342d26
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89531576"
---
# <a name="sysdm_pdw_component_health_active_alerts-transact-sql"></a>sys. dm_pdw_component_health_active_alerts (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  儲存元件上的作用中警示 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|節點的唯一識別碼 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 。<br /><br /> pdw_node_id、component_id、component_instance_id、alert_id 和 alert_instance_id 會形成此視圖的索引鍵。|NOT NULL|  
|component_id|**int**|元件的識別碼。 請參閱 [sys. pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。<br /><br /> pdw_node_id、component_id、component_instance_id、alert_id 和 alert_instance_id 會形成此視圖的索引鍵。|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id、component_id、component_instance_id、alert_id 和 alert_instance_id 會形成此視圖的索引鍵。|NOT NULL|  
|alert_id|**int**|警示類型的識別碼。 請參閱 [sys. pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)。<br /><br /> pdw_node_id、component_id、component_instance_id、alert_id 和 alert_instance_id 會形成此視圖的索引鍵。|NOT NULL|  
|alert_instance_id|**Nvarchar (36) **|識別指定之警示的實例。<br /><br /> pdw_node_id、component_id、component_instance_id、alert_id 和 alert_instance_id 會形成此視圖的索引鍵。|NOT NULL|  
|current_value|**nvarchar(255)**|當警示的類型為 StatusChange 時使用。 這是目前的元件狀態。 針對類型臨界值的警示，值為 Null。 請參閱 [sys. pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) 以取得警示類型清單。|NULL|  
|previous_value|**nvarchar(255)**|當警示的類型為 StatusChange 時使用。 這是先前的元件狀態。 針對類型臨界值的警示，值為 Null。 請參閱 [sys. pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) 以取得警示類型清單。|NULL|  
|create_time|**datetime**|產生警示的時間和日期。|NOT NULL|  
  
 如需此視圖所保留之最大資料列的相關資訊，請參閱中的「最小值與最大值」 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
