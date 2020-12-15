---
description: 'sys.pdw_health_alerts (Transact-sql) '
title: sys.pdw_health_alerts (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: fcdb396016c58f82f3e67f08af2b5489adb40731
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472939"
---
# <a name="syspdw_health_alerts-transact-sql"></a>sys.pdw_health_alerts (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  儲存可能發生在系統上之不同警示的屬性;這是警示的目錄資料表。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|警示的唯一識別碼。<br /><br /> 此視圖的索引鍵。|NOT NULL|  
|component_id|**int**|此警示適用的元件識別碼。 元件是一般的元件識別碼，例如「電源供應」，而不是安裝特有的元件識別碼。 請參閱 [sys.pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。|NOT NULL|  
|alert_name|**nvarchar(255)**|警示的名稱。|NOT NULL|  
|state|**nvarchar(32)**|警示的狀態。|NOT NULL<br /><br /> 可能的值：<br /><br /> 手術<br /><br /> 'NonOperational'<br /><br /> 降級<br /><br /> 沒有|  
|severity|**nvarchar(32)**|警示的嚴重性。|NOT NULL<br /><br /> 可能的值：<br /><br /> 資訊<br /><br /> 條<br /><br /> 錯誤|  
|類型|**nvarchar(32)**|警示的類型。|NOT NULL<br /><br /> 可能的值：<br /><br /> StatusChange-裝置狀態已變更。<br /><br /> 臨界值-值已超過閾值。|  
|description|**nvarchar(4000)**|警示的描述。|NOT NULL|  
|condition (條件)|**nvarchar(255)**|當 type = 臨界值時使用。 定義警示閾值的計算方式。|NULL|  
|status|**nvarchar(32)**|警示狀態|NULL|  
|condition_value|**bit**|指出是否允許在系統操作期間發生警示。|NULL<br /><br /> 可能值<br /><br /> 0-不產生警示。<br /><br /> 1-產生警示。|  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
