---
title: IsDescendant (DMX) |Microsoft 文件
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c33a607587ee19de0f47942cd2c1e5b350229a88
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38061036"
---
# <a name="isdescendant-dmx"></a>IsDescendant (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指出目前的節點是否從指定的節點衍生。  
  
## <a name="syntax"></a>語法  
  
```  
  
IsDescendant(<NodeID>)  
```  
  
## <a name="return-type"></a>傳回類型  
 Boolean 類型。  
  
## <a name="remarks"></a>備註  
 **IsDescendant**只會在[FROM&#60;模型&#62;。內容&#40;DMX&#41; ](../dmx/select-from-model-content-dmx.md)並[選取 從&#60;模型&#62;。DIMENSION_CONTENT &#40;DMX&#41; ](../dmx/select-from-model-dimension-content-dmx.md)查詢。  
  
## <a name="examples"></a>範例  
 下列範例根據 IsDescendant 函數指定的節點，傳回節點子系的所有案例。  
  
```  
SELECT * FROM [TM Decision Tree].CONTENT  
WHERE IsDescendant('00000000100')  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;函式參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
