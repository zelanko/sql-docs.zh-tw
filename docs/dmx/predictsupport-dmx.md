---
title: PredictSupport (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: efe9fb0222dc745e48c248214c42ce706ea18d89
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041867"
---
# <a name="predictsupport-dmx"></a>PredictSupport (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回指定狀態的支援值。  
  
## <a name="syntax"></a>語法  
  
```  
  
PredictSupport(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>適用於  
 純量資料行。  
  
## <a name="return-type"></a>傳回類型  
 純量值所指定之型別的 *\<* 純量資料行參考 *>* 。  
  
## <a name="remarks"></a>備註  
 如果省略預測狀態，就會使用可預測之機率最高的狀態，遺漏狀態值區除外。 若要包含遺漏狀態值區，設定\<預測狀態 > 要**INCLUDE_NULL**。  
  
 若要傳回遺漏狀態的支援，請設定\<預測狀態 > 為 NULL。  
  
> [!NOTE]  
>  支援值會以不同的方式計算，或者根據您要查詢的模型類型而有不同的解譯。 如需如何針對特定模型類型計算支援的詳細資訊，請參閱個別輸入中的演算法[採礦模型內容&#40;Analysis Services-Data Mining&#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)。  
  
## <a name="examples"></a>範例  
 下列範例根據 TM Decision Tree 採礦模型，使用單一查詢來預測個人是否可能成為腳踏車買主，也判斷預測的支援。  
  
```  
SELECT  
  [Bike Buyer],  
  PredictSupport([Bike Buyer]) AS [Support],  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;函式參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
