---
title: TopCount （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d4b91b06470c9cb22e98ac76ea52494728a7ca11
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68893098"
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  依照運算式指定的遞減次序順序，傳回指定數目的最頂部資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>套用至  
 傳回資料表的運算式，例如\<資料表資料行參考>，或傳回資料表的函數。  
  
## <a name="return-type"></a>傳回類型  
 \<資料表運算式>  
  
## <a name="remarks"></a>備註  
 \<次序運算式> 引數所提供的值，會決定\<資料表運算式> 引數中所提供資料列的次序遞減順序，並傳回\<count> 引數中指定之最上層資料列的數目。  
  
 TopCount 函數原本是為了啟用關聯預測而引進，而且通常會產生與包含**SELECT TOP**和**ORDER BY**子句的語句相同的結果。 如果您使用**預測（DMX）** 函數來支援要傳回之預測數目的指定，您將可獲得關聯預測的較佳效能。  
  
 不過，在某些情況下，您可能仍然需要使用 TopCount。 例如，DMX 不支援在子 select 語句中使用**TOP**辨識符號。 [PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md)函數也不支援新增**TOP**。  
  
## <a name="examples"></a>範例  
 下列範例是針對您使用[基本資料採礦教學](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)課程所建立的關聯模型進行的預測查詢。 查詢會傳回相同的結果，但第一個範例會使用 TopCount，而第二個範例會使用 Predict 函數。  
  
 若要瞭解 TopCount 的運作方式，第一次執行只傳回嵌套資料表的預測查詢可能會很有説明。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  在此範例中，當做輸入提供的值包含單引號，因此必須在該值前面加上另一個單引號來逸出。 如果您不確定插入逸出字元的語法，可以使用預測查詢產生器來建立查詢。 當您從下拉式清單選取值時，就會為您插入所需的逸出字元。 如需詳細資訊，請參閱[在資料採礦設計工具中建立單一查詢](https://docs.microsoft.com/analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer)。  
  
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
  
 TopCount 函數會採用此查詢的結果，並傳回指定數目的最小值資料列。  
  
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
  
 TopCount 函數的第一個引數是資料表資料行的名稱。 在此範例中，會藉由呼叫 Predict 函數並使用 INCLUDE_STATISTICS 引數來傳回嵌套的資料表。  
  
 TopCount 函數的第二個引數是用來排序結果的嵌套資料表中的資料行。 在此範例中，INCLUDE_STATISTICS 選項會傳回資料行 $SUPPORT、$PROBABILTY 和 $ADJUSTED PROBABILITY。 此範例會使用 $SUPPORT 來排名結果。  
  
 TopCount 函數的第三個引數會指定要傳回的資料列數目（以整數表示）。 若要取得前三個產品 (如 $SUPPORT 所排序)，請輸入 3。  
  
 範例結果︰  
  
|模型|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29 .。。|0.25 .。。|  
|Water Bottle|2866|0.19 .。。|0.17 .。。|  
|Patch kit|2113|0.14 .。。|0.13 .。。|  
  
 但是，這種類型的查詢可能會影響實際設定的效能。 這是因為此查詢會從演算法傳回所有預測的集合、排序這些預測，並傳回前三個。  
  
 下列範例會提供替代陳述式，此陳述式會傳回相同的結果，但是執行速度則快得多。 這個範例會將 TopCount 取代為 Predict 函式，此函數接受數個預測做為引數。 這個範例也會使用 **$SUPPORT**關鍵字直接抓取嵌套的資料表資料行。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 結果包含了根據支援值所排序的前三項預測。 您可以使用 $PROBABILITY 或 $ADJUSTED_PROBABILITY 來取代 $SUPPORT，以傳回根據機率或調整過的機率所排名的預測。 如需詳細資訊，請參閱**Predict （DMX）**。  
  
## <a name="see-also"></a>另請參閱  
 [DMX&#41;的函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)   
 [DMX&#41;的 BottomCount &#40;](../dmx/bottomcount-dmx.md)   
 [DMX&#41;的 TopPercent &#40;](../dmx/toppercent-dmx.md)   
 [DMX&#41;的 TopSum &#40;](../dmx/topsum-dmx.md)  
  
  
