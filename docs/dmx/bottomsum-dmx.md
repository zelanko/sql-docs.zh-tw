---
description: BottomSum (DMX)
title: BottomSum (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8a80c42971199d6acf57e802994feced63b7899f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431140"
---
# <a name="bottomsum-dmx"></a>BottomSum (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  以遞增次序的順序，傳回累計總和至少達指定值的最底部資料表資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
BottomSum(<table expression>, <rank expression>, <sum>)  
```  
  
## <a name="applies-to"></a>套用至  
 傳回資料表的運算式，例如 \<table column reference> ，或傳回資料表的函數。  
  
## <a name="return-type"></a>傳回類型  
 \<table expression>  
  
## <a name="remarks"></a>備註  
 **BottomSum**函數會以遞增的順位順序傳回最底層的資料列。 排名是根據 \<rank expression> 每個資料列之引數的評估值，因此值的總和 \<rank expression> 至少是引數所指定的指定總計 \<sum> 。 當仍然符合指定的總和值時， **BottomSum**會傳回可能的最小元素數目。  
  
## <a name="examples"></a>範例  
 下列範例會針對您使用「 [基本資料採礦」教學](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)課程所建立的關聯模型建立預測查詢。  
  
 若要瞭解 BottomSum 的運作方式，請先執行僅傳回嵌套資料表的預測查詢，這可能會很有説明。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  在此範例中，當做輸入提供的值包含單引號，因此必須在該值前面加上另一個單引號來逸出。 如果您不確定插入逸出字元的語法，可以使用預測查詢產生器來建立查詢。 當您從下拉式清單選取值時，就會為您插入所需的逸出字元。 如需詳細資訊，請參閱 [在資料採礦設計師中建立單一查詢](https://docs.microsoft.com/analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer)。  
  
 範例結果︰  
  
|模型|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
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
  
 BottomSum 函數會採用此查詢的結果，並傳回具有加總為指定計數之最小值的資料列。  
  
```  
SELECT   
BottomSum  
    (  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $PROBABILITY,  
    .1)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 BottomSum 函數的第一個引數是資料表資料行的名稱。 在此範例中，會藉由呼叫 Predict 函數並使用 INCLUDE_STATISTICS 引數來傳回嵌套資料表。  
  
 BottomSum 函數的第二個引數是用來排序結果的嵌套資料表中的資料行。 在此範例中，INCLUDE_STATISTICS 選項會傳回資料行 $SUPPORT、$PROBABILTY 和 $ADJUSTED PROBABILITY。 此範例會使用 $PROBABILITY 傳回加總為至少 50% 機率的資料列。  
  
 BottomSum 函數的第三個引數會以雙精度浮點數指定目標總和。 若要取得加總為百分之 10 機率之最低計數產品的資料列，請輸入 .1。  
  
 範例結果︰  
  
|模型|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.08 .。。|0.07 .。。|  
|Mountain Bottle Cage|1367|0.09 .。。|0.08 .。。|  
  
 **注意** 此範例僅提供用來說明 BottomSum 的使用方式。 根據資料集的大小而定，此查詢可能會花上很長的一段執行時間。  
  
## <a name="see-also"></a>另請參閱  
 [DMX&#41;函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數 ](../dmx/general-prediction-functions-dmx.md)   
 [BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)  
  
  
