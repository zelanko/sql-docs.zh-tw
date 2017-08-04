---
title: "BottomSum (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BOTTOMSUM
dev_langs:
- DMX
helpviewer_keywords:
- BottomSum function
ms.assetid: fd4b0418-f814-4d83-b2fe-850117e1beb7
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8f6d13ccce9bc25f08e1f0f86b026b24ea75d375
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="bottomsum-dmx"></a>BottomSum (DMX)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  以遞增次序的順序，傳回累計總和至少達指定值的最底部資料表資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
BottomSum(<table expression>, <rank expression>, <sum>)  
```  
  
## <a name="applies-to"></a>適用於  
 運算式會傳回資料表，例如\<資料表資料行參考 >，或傳回資料表的函數。  
  
## <a name="return-type"></a>傳回類型  
 \<資料表運算式 >  
  
## <a name="remarks"></a>備註  
 **BottomSum**函數會以遞增次序順序傳回最底部資料列。 次序為基礎的評估值\<排名運算式 >，每一列的引數的總和\<排名運算式 > 值至少是所指定的給定的總和\<總和 > 引數。 **BottomSum**傳回符合指定的總和值的可能最小元素數目。  
  
## <a name="examples"></a>範例  
 下列範例會建立預測查詢的關聯模型，您使用建置[基本資料採礦教學課程](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。  
  
 若要了解 BottomSum 的運作方式，可能很有幫助先執行僅傳回巢狀的資料表的預測查詢。  
  
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
  
 BottomSum 函數會採用此查詢的結果，並傳回數值最低的資料列加總為指定計數。  
  
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
  
 BottomSum 函數的第一個引數是資料表資料行的名稱。 在此範例中，巢狀的資料表會傳回呼叫預測函式，並使用 INCLUDE_STATISTICS 引數。  
  
 BottomSum 函式的第二個引數是您用來排序結果的巢狀資料表中的資料行。 在此範例中，INCLUDE_STATISTICS 選項會傳回資料行 $SUPPORT、$PROBABILTY 和 $ADJUSTED PROBABILITY。 此範例會使用 $PROBABILITY 傳回加總為至少 50% 機率的資料列。  
  
 BottomSum 函數的第三個引數會指定將目標總和為 double。 若要取得加總為百分之 10 機率之最低計數產品的資料列，請輸入 .1。  
  
 範例結果：  
  
|模型|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.08…|0.07…|  
|Mountain Bottle Cage|1367|0.09…|0.08…|  
  
 **請注意**提供這個範例只是為了說明 BottomSum 的使用方式。 根據資料集的大小而定，此查詢可能會花上很長的一段執行時間。  
  
## <a name="see-also"></a>另請參閱  
 [函式 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomPercent &#40; DMX &#41;](../dmx/bottompercent-dmx.md)  
  
  

