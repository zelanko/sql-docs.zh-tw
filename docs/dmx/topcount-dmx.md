---
title: "TopCount (DMX) |Microsoft 文件"
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
f1_keywords: TOPCOUNT
dev_langs: DMX
helpviewer_keywords: TopCount function
ms.assetid: cbe031c9-4ff0-45df-9810-ebaebacf161d
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 412c741e3f48c23f65eafa2a998a257f07034dd9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  依照運算式指定的遞減次序順序，傳回指定數目的最頂部資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>適用於  
 運算式會傳回資料表，例如\<資料表資料行參考 >，或傳回資料表的函數。  
  
## <a name="return-type"></a>傳回類型  
 \<資料表運算式 >  
  
## <a name="remarks"></a>備註  
 所提供的值\<排名運算式 > 引數會決定遞減次序順序中提供的資料列\<資料表運算式 > 引數，以及中所指定的最高的資料列數目\<計數 > 引數會傳回。  
  
 TopCount 函數原本引進為了啟用關聯預測，而且通常會產生與包含的陳述式相同的結果**選取前**和**ORDER BY**子句。 如果您使用，您將會得到關聯預測的較佳效能**預測 (DMX)**函式，以支援要傳回之預測數目的指定。  
  
 不過，有很多情況下，您可能仍然需要使用 TopCount。 例如，不支援 DMX**頂端**子 select 陳述式中的辨識符號。 [PredictHistogram &#40; DMX &#41;](../dmx/predicthistogram-dmx.md)函式也不支援新增**頂端**。  
  
## <a name="examples"></a>範例  
 下列範例會使用您建立的關聯模型的預測查詢[基本資料採礦教學課程](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。 查詢會傳回相同的結果，但是第一個範例會使用 TopCount，而且第二個範例使用預測函數。  
  
 若要了解 TopCount 的運作方式，可能很有幫助先執行僅傳回巢狀的資料表的預測查詢。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  在此範例中，當做輸入提供的值包含單引號，因此必須在該值前面加上另一個單引號來逸出。 如果您不確定插入逸出字元的語法，可以使用預測查詢產生器來建立查詢。 當您從下拉式清單選取值時，就會為您插入所需的逸出字元。 如需詳細資訊，請參閱[資料採礦設計師中建立單一查詢](../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md)。  
  
 範例結果：  
  
|[模型]|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016|0.252695851|  
|Water Bottle|2866|0.192620472|0.175205052|  
|Patch kit|2113|0.142012232|0.132389356|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
  
 TopCount 函數會採用此查詢的結果，並傳回指定的最小值的資料列數。  
  
```  
SELECT   
TopCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 TopCount 函數的第一個引數是資料表資料行的名稱。 在此範例中，巢狀的資料表會傳回呼叫預測函式，並使用 INCLUDE_STATISTICS 引數。  
  
 TopCount 函式的第二個引數是您用來排序結果的巢狀資料表中的資料行。 在此範例中，INCLUDE_STATISTICS 選項會傳回資料行 $SUPPORT、$PROBABILTY 和 $ADJUSTED PROBABILITY。 此範例會使用 $SUPPORT 來排名結果。  
  
 TopCount 函數的第三個引數指定要傳回，以整數形式的資料列數目。 若要取得前三個產品 (如 $SUPPORT 所排序)，請輸入 3。  
  
 範例結果：  
  
|[模型]|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29…|0.25…|  
|Water Bottle|2866|0.19…|0.17…|  
|Patch kit|2113|0.14…|0.13…|  
  
 但是，這種類型的查詢可能會影響實際設定的效能。 這是因為此查詢會從演算法傳回所有預測的集合、排序這些預測，並傳回前三個。  
  
 下列範例會提供替代陳述式，此陳述式會傳回相同的結果，但是執行速度則快得多。 此範例會使用預測函數，可接受之預測數目當做引數取代 TopCount。 此範例也會使用**$SUPPORT**關鍵字，直接擷取巢狀的資料表資料行。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 結果包含了根據支援值所排序的前三項預測。 您可以使用 $PROBABILITY 或 $ADJUSTED_PROBABILITY 來取代 $SUPPORT，以傳回根據機率或調整過的機率所排名的預測。 如需詳細資訊，請參閱**預測 (DMX)**。  
  
## <a name="see-also"></a>請參閱  
 [函式 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomCount &#40; DMX &#41;](../dmx/bottomcount-dmx.md)   
 [TopPercent &#40; DMX &#41;](../dmx/toppercent-dmx.md)   
 [TopSum &#40; DMX &#41;](../dmx/topsum-dmx.md)  
  
  
