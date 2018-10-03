---
title: sys.pdw_health_alerts (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d26b8d9b19b29a92481c3dccf9d4809e74691a44
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47794466"
---
# <a name="syspdwhealthalerts-transact-sql"></a>sys.pdw_health_alerts & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  將可能會發生不同警示的內容儲存在系統上;這是警示類別目錄資料表。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|警示的唯一識別碼。<br /><br /> 此檢視的索引鍵。|NOT NULL|  
|component_id|**int**|此警示適用於元件的識別碼。 元件是一般的元件識別碼，例如 「 電源供應器，"，而且不會安裝所特有。 請參閱[sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。|NOT NULL|  
|alert_name|**nvarchar(255)**|警示的名稱。|NOT NULL|  
|state|**nvarchar(32)**|警示的狀態。|NOT NULL<br /><br /> 可能的值如下：<br /><br /> ' Operational'<br /><br /> '為' 非作業的狀態。<br /><br /> 「 已降級 」<br /><br /> 「 失敗 」|  
|severity|**nvarchar(32)**|警示的嚴重性。|NOT NULL<br /><br /> 可能的值如下：<br /><br /> 「 資訊 」<br /><br /> 「 警告 」<br /><br /> 「 錯誤 」|  
|型別|**nvarchar(32)**|警示類型。|NOT NULL<br /><br /> 可能的值如下：<br /><br /> StatusChange-已變更裝置狀態。<br /><br /> 閾值-值已超過臨界值。|  
|description|**nvarchar(4000)**|警示的描述。|NOT NULL|  
|condition (條件)|**nvarchar(255)**|輸入時，使用 = 臨界值。 定義警示的臨界值的計算方式。|NULL|  
|status|**nvarchar(32)**|警示狀態|NULL|  
|condition_value|**bit**|指出是否允許警示系統作業期間會發生。|NULL<br /><br /> 可能值<br /><br /> 0-不會產生警示。<br /><br /> 1-會產生警示。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
