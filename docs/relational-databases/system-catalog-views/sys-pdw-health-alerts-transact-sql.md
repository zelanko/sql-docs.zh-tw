---
title: "sys.pdw_health_alerts (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f7e05ccc9cc264faf5d4d7f563d1df028969309
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwhealthalerts-transact-sql"></a>sys.pdw_health_alerts (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  不同的警示，可能發生在系統; 的存放區屬性這是類別目錄資料表中的警示。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|警示的唯一識別碼。<br /><br /> 此檢視的索引鍵。|NOT NULL|  
|component_id|**int**|此警示適用於元件的識別碼。 元件是一般元件的識別碼，例如 「 電源提供 」，並不是安裝所特有。 請參閱[sys.pdw_health_components &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|alert_name|**nvarchar(255)**|警示的名稱。|NOT NULL|  
|state|**nvarchar （32)**|警示的狀態。|NOT NULL<br /><br /> 可能的值如下：<br /><br /> ' Operational'<br /><br /> '為' 非作業的狀態。<br /><br /> ' 降級 '<br /><br /> 「 失敗 」|  
|severity|**nvarchar （32)**|警示的嚴重性。|NOT NULL<br /><br /> 可能的值如下：<br /><br /> ' 資訊 '<br /><br /> 「 警告 」<br /><br /> 「 錯誤 」|  
|型別|**nvarchar （32)**|警示類型。|NOT NULL<br /><br /> 可能的值如下：<br /><br /> StatusChange-裝置狀態已變更。<br /><br /> 臨界值的值已超過臨界值。|  
|description|**nvarchar(4000)**|警示的描述。|NOT NULL|  
|condition (條件)|**nvarchar(255)**|輸入時，使用 = 臨界值。 定義警示的臨界值的計算方式。|NULL|  
|status|**nvarchar （32)**|警示狀態|NULL|  
|condition_value|**bit**|指出是否允許警示系統作業期間發生。|NULL<br /><br /> 可能值<br /><br /> 0-不會產生警示。<br /><br /> 1 個警示。|  
  
## <a name="see-also"></a>請參閱＜  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
