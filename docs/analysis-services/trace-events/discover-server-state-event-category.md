---
title: 探索伺服器狀態事件類別目錄 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 953936b1f8054e6294788184750bb9e888b43f0f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="discover-server-state-event-category"></a>探索伺服器狀態事件類別目錄
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  探索伺服器狀態事件類別目錄具有下表所描述的事件類別。  
  
|Event Class|事件識別碼|說明|  
|-----------------|--------------|-----------------|  
|伺服器狀態探索的開始|33|收集自從啟動追蹤之後的所有伺服器狀態 XMLA 探索開始事件。|  
|伺服器狀態探索資料|34|收集自從啟動追蹤之後的所有伺服器狀態 XMLA 探索資料事件。 這些事件會擷取探索要求的回應內容。|  
|伺服器狀態探索的結束|35|收集自從啟動追蹤之後的所有伺服器狀態 XMLA 探索結束事件。|  
  
 如需與每個「查詢事件」事件類別相關聯之資料行的資訊，請參閱 [探索伺服器狀態事件資料行](../../analysis-services/trace-events/discover-server-state-events-data-columns.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 追蹤事件](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
