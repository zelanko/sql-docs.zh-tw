---
title: 查詢處理事件的類別目錄 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 576a07ac29c598691ccdbf00cd3ca165edf99c0d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="query-processing-events-category"></a>查詢處理事件類別目錄
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  查詢處理事件類別目錄具有下表所描述的事件類別。  
  
|**Event Class**|**事件識別碼**|**說明**|  
|---------------------|------------------|---------------------|  
|查詢 Subcube|11|查詢 Subcube 以用於基於使用方式的最佳化。|  
|查詢 Subcube 詳細資訊|12|查詢 Subcube 的詳細資訊。 開啟時，這個事件可能會對效能造成負面影響。|  
|從彙總取得資料|60|藉由從彙總取得資料來回答查詢。 開啟時，這個事件可能會對效能造成負面影響。|  
|從快取取得資料|61|藉由從其中一個快取取得資料來回答查詢。 開啟時，這個事件可能會對效能造成負面影響。|  
|查詢 Cube 開始|70|收集自從啟動追蹤之後的所有查詢 Cube 開始事件。|  
|查詢 Cube 結束|71|收集自從啟動追蹤之後的所有查詢 Cube 結束事件。|  
|計算非空白開始|72|計算非空白開始。|  
|計算非空白目前|73|計算非空白目前。|  
|計算非空白結束|74|計算非空白結束。|  
|序列化結果開始|75|序列化結果開始。|  
|序列化結果目前|76|序列化結果目前。|  
|序列化結果結束|77|序列化結果結束。|  
|執行 MDX 指令碼開始|78|執行 MDX 指令碼開始。|  
|執行 MDX 指令碼目前|79|執行 MDX 指令碼目前。|  
|執行 MDX 指令碼結束|80|執行 MDX 指令碼結束。|  
|查詢維度|81|查詢維度。|  
|VertiPaq SE 查詢開始|82|VertiPaq SE 查詢|  
|VertiPaq SE 查詢結束|83|VertiPaq SE 查詢|  
  
 如需有關每個查詢處理事件類別相關聯之資料行的詳細資訊，請參閱＜ [Query Processing Events Data Columns](../../analysis-services/trace-events/query-processing-events-data-columns.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 追蹤事件](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
