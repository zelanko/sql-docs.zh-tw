---
title: "RangeMin (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: RangeMin
dev_langs: DMX
helpviewer_keywords: RangeMin function
ms.assetid: 64159bbe-7016-4f67-91d9-5c5f6ceb6c25
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 16d56170a3b4c995a7c93c3f9acf699e3f4e3071
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="rangemin-dmx"></a>RangeMin (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回針對分隔式資料行探索之預測值區的低端。  
  
## <a name="syntax"></a>語法  
  
```  
  
RangeMin(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>適用於  
 純量資料行。  
  
## <a name="return-type"></a>傳回類型  
 純量值。  
  
## <a name="remarks"></a>備註  
 **RangeMin**函式可用於[SELECT DISTINCT FROM &#60; 模型 &#62; &#40; DMX &#41;](../dmx/select-distinct-from-model-dmx.md)查詢。 搭配這種查詢類型使用時，純量資料行參考可以包含可預測或輸入的連續或分隔資料行。  
  
 當搭配[SELECT FROM &#60; 模式 &#62;預測聯結 &#40; DMX &#41;](../dmx/select-from-model-prediction-join-dmx.md)、 **RangeMin**， **RangeMid**，和**RangeMax**函式會傳回指定的貯體的實際界限值。 例如，您若是執行分隔式資料行的預測，查詢就會傳回分隔式資料行中的預測值區號碼。 **RangeMin**， **RangeMid**，和**RangeMax**函數會描述預測所指定的貯體。 當**RangeMin**函數搭配 PREDICTION JOIN 陳述式、 純量資料行參考只能包含分隔、 可預測資料行。  
  
## <a name="examples"></a>範例  
 下列範例傳回 Decision Tree 採礦模型中 Yearly Income 連續資料行的最小值、最大值及平均值。  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMax &#40; DMX &#41;](../dmx/rangemax-dmx.md)   
 [RangeMid &#40; DMX &#41;](../dmx/rangemid-dmx.md)  
  
  
