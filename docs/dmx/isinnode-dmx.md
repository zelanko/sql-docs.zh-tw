---
title: IsInNode (DMX) |Microsoft 文件
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 21c90bea43972f1c9088c228d6810b18308f93f4
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841701"
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
 **IsInNode**僅用於[SELECT FROM&#60;模型&#62;。案例&#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md)和[SELECT FROM&#60;模型&#62;。SAMPLE_CASES &#40;DMX&#41; ](../dmx/select-from-model-sample-cases-dmx.md)查詢。  
  
## <a name="examples"></a>範例  
 下列範例根據 IsInNode 函數中指定的節點相關聯的模型，傳回建立此模型的案例。  
  
```  
Select * from [TM Decision Tree].Cases  
WHERE IsInNode('0')  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
