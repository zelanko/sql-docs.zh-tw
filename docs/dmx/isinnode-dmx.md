---
title: "IsInNode (DMX) |Microsoft 文件"
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
f1_keywords:
- IsInNode
dev_langs:
- DMX
helpviewer_keywords:
- IsInNode function
ms.assetid: 47b2114f-9ad6-45cc-9498-193ad6fa5288
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d10cc8b335fa47eee2932da7805f97fb42ed6711
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="isinnode-dmx"></a>IsInNode (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指示指定的節點是否包含目前案例。  
  
## <a name="syntax"></a>語法  
  
```  
  
IsInNode(<NodeID>)  
```  
  
## <a name="return-type"></a>傳回類型  
 Boolean 類型。  
  
## <a name="remarks"></a>備註  
 **IsInNode**僅用於[SELECT FROM &#60; 模式 &#62;。案例 &#40; DMX &#41;](../dmx/select-from-model-cases-dmx.md)和[SELECT FROM &#60; 模式 &#62;。SAMPLE_CASES &#40; DMX &#41;](../dmx/select-from-model-sample-cases-dmx.md)查詢。  
  
## <a name="examples"></a>範例  
 下列範例根據 IsInNode 函數中指定的節點相關聯的模型，傳回建立此模型的案例。  
  
```  
Select * from [TM Decision Tree].Cases  
WHERE IsInNode('0')  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

