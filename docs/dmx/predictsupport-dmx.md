---
description: PredictSupport (DMX)
title: PredictSupport (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cea4913bf3668c89fb0c1c66632359a372f3d54b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422252"
---
# <a name="predictsupport-dmx"></a>PredictSupport (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  傳回指定狀態的支援值。  
  
## <a name="syntax"></a>語法  
  
```  
  
PredictSupport(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>套用至  
 純量資料行。  
  
## <a name="return-type"></a>傳回類型  
 所指定之類型的純量值 *\<*scalar column reference*>* 。  
  
## <a name="remarks"></a>備註  
 如果省略預測狀態，就會使用可預測之機率最高的狀態，遺漏狀態值區除外。 若要包含遺漏的狀態值區，請將設定 \<predicted state> 為 **INCLUDE_Null**。  
  
 若要傳回遺漏狀態的支援，請將設定 \<predicted state> 為 Null。  
  
> [!NOTE]  
>  支援值會以不同的方式計算，或者根據您要查詢的模型類型而有不同的解譯。 如需有關如何針對任何特定模型類型計算支援的詳細資訊，請參閱「採礦模型內容」中的個別演算法類型 [&#40;Analysis Services-資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining)。  
  
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
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數 ](../dmx/general-prediction-functions-dmx.md)  
  
  
