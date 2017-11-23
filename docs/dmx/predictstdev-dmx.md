---
title: "PredictStdev (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: PredictStdev
dev_langs: DMX
helpviewer_keywords: PredictStdev function
ms.assetid: 2614aad0-f3f2-4f56-9dad-9c436f11a35f
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 63a4d43c4c851f4bc03675fe06220e3a42827a85
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="predictstdev-dmx"></a>PredictStdev (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回指定之資料行的預測標準差。  
  
## <a name="syntax"></a>語法  
  
```  
  
PredictStdev(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>適用於  
 純量資料行。  
  
## <a name="return-type"></a>傳回類型  
 純量值所指定之型別的*\<純量資料行參考 >*。  
  
## <a name="remarks"></a>備註  
 如果資料行參考是離散的**PredictStdev**傳回 0，因為無法從離散值計算標準差。  
  
## <a name="examples"></a>範例  
 下列範例根據 TM Decision Tree 採礦模型，使用自然預測聯結以判斷個人是否可能成為腳踏車買主，也判斷預測的標準差。  
  
```  
SELECT  
  [Bike Buyer],  
  PredictStdev([Bike Buyer]) AS [Standard Deviation]  
FROM  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>請參閱＜  
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
