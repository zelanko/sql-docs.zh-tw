---
title: "sys.dm_pdw_component_health_alerts (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 88f05392-1e97-4693-ba60-a4910af3c000
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 51360614a6939c64b005a93cd178b2e6ff22e4e2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmpdwcomponenthealthalerts-transact-sql"></a>sys.dm_pdw_component_health_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  存放區先前發行的應用裝置元件的警示。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|唯一識別項[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]節點。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 形成這個檢視的索引鍵。|NOT NULL|  
|component_id|**int**|元件的識別碼。 請參閱[sys.pdw_health_components &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 形成這個檢視的索引鍵。|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 形成這個檢視的索引鍵。|NOT NULL|  
|alert_id|**int**|警示類型的識別碼。 請參閱[sys.pdw_health_alerts &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 形成這個檢視的索引鍵。|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|識別指定警示的執行個體。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 形成這個檢視的索引鍵。|NOT NULL|  
|previous_value|**nvarchar(255)**|警示是型別 StatusChange 時使用。 這是先前的元件狀態。 值為 NULL 類型閾值的警示。 請參閱[sys.pdw_health_alerts &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)的警示類型清單。|NULL|  
|current_value|**nvarchar(255)**|警示是型別 StatusChange 時使用。 這是目前元件的狀態。 值為 NULL 類型閾值的警示。 請參閱[sys.pdw_health_alerts &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)的警示類型清單。|NULL|  
|create_time|**datetime**|警示產生時的日期和時間。|NOT NULL|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
