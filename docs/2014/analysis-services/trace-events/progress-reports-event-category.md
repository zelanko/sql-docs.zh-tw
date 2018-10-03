---
title: 進度報表事件類別目錄 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- progress events [Analysis Services]
- Progress Reports event category
- event classes [Analysis Services], progress reports
ms.assetid: c130f160-28ef-49bc-9ee6-da47dc9aab2a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1098df2f9a1c06277971f2a51ae3385c288bfd2a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079778"
---
# <a name="progress-reports-event-category"></a>進度報表事件類別目錄
  進度報表事件類別目錄具有下表所描述的事件類別。  
  
|Event Class|事件識別碼|描述|  
|-----------------|--------------|-----------------|  
|進度報表開始|5|收集自從啟動追蹤之後的所有進度報表開始事件。|  
|進度報表結束|6|收集自從啟動追蹤之後的所有進度報表結束事件。|  
|進度報表目前事件|7|收集自從啟動追蹤之後的所有進度報表目前事件。 例如，在處理期間，目前的報表會包括關於處理中物件 (維度、資料分割、Cube 等等) 的處理資訊。|  
|進度報表錯誤|8|收集自從啟動追蹤之後的所有進度報表錯誤事件。|  
  
 每一個進度報表開始事件是以進度事件資料流開始，然後以進度報表結束事件結束。 資料流可包含任何數量的進度報表目前事件和進度報表錯誤事件。  
  
 如需每個 [進度報表] 事件類別之相關資料行的資訊，請參閱 [進度報表資料行](progress-reports-data-columns.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 追蹤事件](analysis-services-trace-events.md)  
  
  
