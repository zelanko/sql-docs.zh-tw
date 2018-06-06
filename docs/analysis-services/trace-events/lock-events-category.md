---
title: 鎖定事件類別目錄 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 62804b077f43b5123b1992a6f52b29af288e2821
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="lock-events-category"></a>Lock 事件類別目錄
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  鎖定事件的事件類別目錄具有下表所描述的事件類別。  
  
|Event Class|事件識別碼|說明|  
|-----------------|--------------|-----------------|  
|死結|50|收集自從啟動追蹤之後的所有中繼資料鎖定死結事件。|  
|鎖定逾時|51|收集自從啟動追蹤之後的所有中繼資料鎖定逾時事件。|  
|取得的鎖定|52|收集自從啟動追蹤之後與已取得的鎖定有關的資訊。|  
|釋放的鎖定|53|收集自從啟動追蹤之後與已釋放的鎖定有關的資訊。|  
|正在等候的鎖定|54|收集自從啟動追蹤之後與處於等候狀態的鎖定有關的資訊。|  
  
 如需有關每個鎖定事件類別相關聯之資料行的詳細資訊，請參閱＜ [Lock Events Data Columns](../../analysis-services/trace-events/lock-events-data-columns.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 追蹤事件](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
