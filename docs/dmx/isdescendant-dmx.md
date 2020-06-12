---
title: IsDescendant （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2ef32a9e133c199aae0779c819736d77e0d15c45
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670067"
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
 **IsDescendant**僅用於[SELECT FROM &#60;model&#62;。&#40;DMX&#41;的內容](../dmx/select-from-model-content-dmx.md)，並[從 &#60;模型&#62; 中選取。DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)查詢。  
  
## <a name="examples"></a>範例  
 下列範例根據 IsDescendant 函數指定的節點，傳回節點子系的所有案例。  
  
```  
SELECT * FROM [TM Decision Tree].CONTENT  
WHERE IsDescendant('00000000100')  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;的函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)  
  
  
