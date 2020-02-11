---
title: sys.databases pdw_health_alerts （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c47bcc342bf8a052aed93649ca0ad8475d937608
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68127535"
---
# <a name="syspdw_health_alerts-transact-sql"></a>sys.databases pdw_health_alerts （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  儲存可能發生在系統上之不同警示的屬性;這是警示的目錄資料表。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|警示的唯一識別碼。<br /><br /> 此視圖的索引鍵。|NOT NULL|  
|component_id|**int**|此警示適用之元件的識別碼。 元件是一般元件識別碼，例如「電源供應」，而不是特定的安裝。 請參閱[pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。|NOT NULL|  
|alert_name|**nvarchar(255)**|警示的名稱。|NOT NULL|  
|state|**Nvarchar （32）**|警示的狀態。|NOT NULL<br /><br /> 可能的值：<br /><br /> 投入<br /><br /> 'NonOperational'<br /><br /> 降級<br /><br /> 發生|  
|嚴重性|**Nvarchar （32）**|警示的嚴重性。|NOT NULL<br /><br /> 可能的值：<br /><br /> 供<br /><br /> Warning<br /><br /> 糾錯|  
|type|**Nvarchar （32）**|警示的類型。|NOT NULL<br /><br /> 可能的值：<br /><br /> StatusChange-裝置狀態已變更。<br /><br /> 閾值-值已超過臨界值。|  
|description|**nvarchar(4000)**|警示的描述。|NOT NULL|  
|condition|**nvarchar(255)**|類型 = 臨界值時使用。 定義警示臨界值的計算方式。|NULL|  
|status|**Nvarchar （32）**|警示狀態|NULL|  
|condition_value|**bit**|指出是否允許在系統操作期間發生警示。|NULL<br /><br /> 可能的值<br /><br /> 0-不會產生警示。<br /><br /> 1-產生警示。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
