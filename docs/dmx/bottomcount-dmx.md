---
title: BottomCount （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: db7e660b5b92d49f5a5151d5d71e9ac31f9e9013
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969956"
---
# <a name="bottomcount-dmx"></a>BottomCount (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  依照運算式指定的遞增次序順序，傳回指定數目的最底部資料列。  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BottomCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>套用至  
 傳回資料表的運算式，例如 \<table column reference> ，或傳回資料表的函數。  
  
## <a name="return-type"></a>傳回類型  
 \<table expression>  
  
## <a name="remarks"></a>備註  
 引數所提供的值會 \<rank expression> 決定引數中所提供資料列的次序增加順序 \<table expression> ，並傳回引數中指定的最底部資料列數目 \<count> 。  
  
## <a name="examples"></a>範例  
 下列範例會針對您使用[基本資料採礦教學](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)課程所建立的關聯模型，建立預測查詢。  
  
 若要瞭解 BottomCount 的運作方式，第一次執行只傳回嵌套資料表的預測查詢可能會很有説明。  
  
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
  
|型號|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
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
  
 BottomCount 函數會採用此查詢的結果，並傳回總和為指定百分比的最小值資料列。  
  
```  
SELECT   
BottomCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 BottomCount 函數的第一個引數是資料表資料行的名稱。 在此範例中，會藉由呼叫 Predict 函數並使用 INCLUDE_STATISTICS 引數來傳回嵌套的資料表。  
  
 BottomCount 函數的第二個引數是用來排序結果的嵌套資料表中的資料行。 在此範例中，INCLUDE_STATISTICS 選項會傳回資料行 $SUPPORT、$PROBABILTY 和 $ADJUSTED PROBABILITY。 此範例因為支援值不是分數而使用 $SUPPORT，因此比較容易確認。  
  
 BottomCount 函數的第三個引數會指定資料列的數目。 若要取得三個排名最低的資料列 (如 $SUPPORT 所排序)，請輸入 3。  
  
 範例結果︰  
  
|型號|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
  
 **注意**此範例僅供說明 BottomCount 的使用。 根據資料集的大小而定，此查詢可能會花上很長的一段執行時間。  
  
## <a name="see-also"></a>另請參閱  
 [DMX&#41;的函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)   
 [DMX&#41;的 BottomPercent &#40;](../dmx/bottompercent-dmx.md)   
 [DMX&#41;的 BottomSum &#40;](../dmx/bottomsum-dmx.md)   
 [DMX&#41;的 TopCount &#40;](../dmx/topcount-dmx.md)  
  
  
