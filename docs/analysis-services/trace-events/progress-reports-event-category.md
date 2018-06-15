---
title: 進度報表事件類別目錄 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f3e48e34e5b85093793b0ea70786b106d72235a7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34045862"
---
# <a name="progress-reports-event-category"></a>進度報表事件類別目錄
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  進度報表事件類別目錄具有下表所描述的事件類別。  
  
|Event Class|事件識別碼|說明|  
|-----------------|--------------|-----------------|  
|進度報表開始|5|收集自從啟動追蹤之後的所有進度報表開始事件。|  
|進度報表結束|6|收集自從啟動追蹤之後的所有進度報表結束事件。|  
|進度報表目前事件|7|收集自從啟動追蹤之後的所有進度報表目前事件。 例如，在處理期間，目前的報表會包括關於處理中物件 (維度、資料分割、Cube 等等) 的處理資訊。|  
|進度報表錯誤|8|收集自從啟動追蹤之後的所有進度報表錯誤事件。|  
  
 每一個進度報表開始事件是以進度事件資料流開始，然後以進度報表結束事件結束。 資料流可包含任何數量的進度報表目前事件和進度報表錯誤事件。  
  
 如需每個 [進度報表] 事件類別之相關資料行的資訊，請參閱 [進度報表資料行](../../analysis-services/trace-events/progress-reports-data-columns.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 追蹤事件](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
