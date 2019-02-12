---
title: sys.dm_pdw_component_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 88f05392-1e97-4693-ba60-a4910af3c000
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7b3c6cb1c61c15cb81a5c9452b874263cf62bc02
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56033079"
---
# <a name="sysdmpdwcomponenthealthalerts-transact-sql"></a>sys.dm_pdw_component_health_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  存放區先前發行的應用裝置元件的警示。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|唯一識別碼[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]節點。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 形成這個檢視的索引鍵。|NOT NULL|  
|component_id|**int**|元件的識別碼。 請參閱[sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 形成這個檢視的索引鍵。|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 形成這個檢視的索引鍵。|NOT NULL|  
|alert_id|**int**|警示類型的識別碼。 請參閱[sys.pdw_health_alerts &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 形成這個檢視的索引鍵。|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|識別指定警示的執行個體。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 形成這個檢視的索引鍵。|NOT NULL|  
|previous_value|**nvarchar(255)**|型別的 StatusChange 警示時，會使用它。 這是先前的元件狀態。 值為 NULL 的型別臨界值警示。 請參閱[sys.pdw_health_alerts &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)如需警示類型的清單。|NULL|  
|current_value|**nvarchar(255)**|型別的 StatusChange 警示時，會使用它。 這是目前的元件狀態。 值為 NULL 的型別臨界值警示。 請參閱[sys.pdw_health_alerts &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)如需警示類型的清單。|NULL|  
|create_time|**datetime**|警示產生時的日期和時間。|NOT NULL|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
