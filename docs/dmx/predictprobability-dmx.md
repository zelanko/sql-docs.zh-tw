---
title: '[Predictprobability] (DMX) |Microsoft 文件'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f2a01e2cfd460d503e4326c44eaf356b8a5ecb4
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841461"
---
# <a name="predictprobability-dmx"></a>PredictProbability (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回指定狀態的機率。  
  
## <a name="syntax"></a>語法  
  
```  
  
PredictProbability(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>適用於  
 純量資料行。  
  
## <a name="return-type"></a>傳回類型  
 純量值。  
  
## <a name="remarks"></a>備註  
 如果省略預測狀態，就會使用機率最高的狀態，遺漏狀態值區除外。 若要包含遺漏狀態值區，設定\<預測狀態 > 至**INCLUDE_NULL**。 若要傳回遺漏狀態的機率，請設定\<預測狀態 > 為 NULL。  
  
> [!NOTE]  
>  有些採礦模型不提供機率值，因此無法使用此函數。 此外，任何特定目標值的機率值會以不同的方式計算，或者根據您要查詢的模型類型而有不同的解譯。 如需有關如何針對特定模型類型而計算機率的詳細資訊，請參閱中的個別演算法主題[採礦模型內容&#40;Analysis Services-Data Mining&#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)。  
  
## <a name="examples"></a>範例  
 下列範例根據 TM Decision Tree 採礦模型，使用自然預測聯結以判斷個人是否可能成為腳踏車買主，也判斷預測的機率。 在此範例中有兩個 PredictProbability 函數，其中一個用於每個可能的值。 如果您省略這個引數，函數會傳回最可能之值的機率。  
  
```  
SELECT  
  [Bike Buyer],  
  PredictProbability([Bike Buyer], 1) AS [Bike Buyer = Yes],  
  PredictProbability([Bike Buyer], 0) AS [Bike Buyer = No]  
FROM [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 範例結果：  
  
|Bike Buyer|Bike Buyer = Yes|Bike Buyer = No|  
|----------------|-----------------------|----------------------|  
|@shouldalert|0.867074195848097|0.132755556974282|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
