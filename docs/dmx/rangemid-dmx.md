---
title: RangeMid (DMX) |Microsoft 文件
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ee926e04dc5b845be152e96150c99cb17182a7c5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042114"
---
# <a name="rangemid-dmx"></a>RangeMid (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回針對分隔式資料行探索之預測值區的中點。  
  
## <a name="syntax"></a>語法  
  
```  
  
RangeMid(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>適用於  
 分隔的純量資料行。  
  
## <a name="return-type"></a>傳回類型  
 純量值。  
  
## <a name="remarks"></a>備註  
 當搭配[SELECT FROM&#60;模型&#62;PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)，則**RangeMin**， **RangeMid**，以及**RangeMax**函式會傳回指定的貯體的實際界限值。 例如，您若是執行分隔式資料行的預測，查詢就會傳回分隔式資料行中的預測值區號碼。 **RangeMin**， **RangeMid**，並**RangeMax**函數會描述預測所指定的貯體。 當**RangeMid**函數搭配 PREDICTION JOIN 陳述式、 純量資料行參考只能包含分隔、 可預測資料行。  
  
## <a name="examples"></a>範例  
 下列範例傳回 TM Decision Tree 採礦模型中 Yearly Income 連續資料行的最小值、最大值及平均值。  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;函式參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)   
 [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
  
