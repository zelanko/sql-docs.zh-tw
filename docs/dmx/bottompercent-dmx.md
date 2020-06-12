---
title: BottomPercent （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6fdb1563f644b544fd9c0bd2ee0857bf4b403329
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669835"
---
# <a name="bottompercent-dmx"></a>BottomPercent (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  以遞增次序的順序，傳回累計總和至少達指定百分比的最底部資料表資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
BottomPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="arguments"></a>引數  
 *\<資料表運算式>*  
 巢狀資料表資料行的名稱或資料表值運算式。  
  
 *\<次序運算式>*  
 巢狀資料表中的資料行，或評估為資料行的運算式。  
  
 *\<>百分比*  
 表示總目標百分比的雙精確度浮點數。  
  
## <a name="result-type"></a>結果類型  
 資料表。  
  
## <a name="remarks"></a>備註  
 **BottomPercent**函數會以遞增的次序順序傳回最底端的資料列。 次序是 \< 以每個資料列的次序運算式> 引數的評估值為基礎，因此 \< 次序運算式> 值的總和至少是 \< percent> 引數所指定的給定百分比。 **BottomPercent**會傳回仍然符合指定之百分比值的最小元素數目。  
  
## <a name="examples"></a>範例  
 下列範例會針對您在[基本資料採礦教學](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)課程中建立的關聯模型，建立預測查詢。  
  
 若要瞭解 BottomPercent 的運作方式，第一次執行只傳回嵌套資料表的預測查詢可能會很有説明。  
  
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
  
 BottomPercent 函數會採用此查詢的結果，並傳回總和為指定百分比的最小值資料列。  
  
```  
SELECT   
BottomPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 BottomPercent 函數的第一個引數是資料表資料行的名稱。 在此範例中，會藉由呼叫 Predict 函數並使用 INCLUDE_STATISTICS 引數來傳回嵌套的資料表。  
  
 BottomPercent 函數的第二個引數是用來排序結果的嵌套資料表中的資料行。 在此範例中，INCLUDE_STATISTICS 選項會傳回資料行 $SUPPORT、$PROBABILTY 和 $ADJUSTED PROBABILITY。 此範例因為支援值不是分數而使用 $SUPPORT，因此比較容易確認。  
  
 BottomPercent 函數的第三個引數會將百分比指定為雙精度浮點數。 若要取得代表支援之最下層 50% 的資料列，可以輸入 50。  
  
 範例結果︰  
  
|型號|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
  
 **注意**此範例僅供說明 BottomPercent 的使用方式。 根據資料集的大小而定，此查詢可能會花上很長的一段執行時間。  
  
> [!WARNING]  
>  當用來計算百分比的值包含負數時，TOPPERCENT 和 BOTTOMPERCENT 的 MDX 函數會產生非預期的結果。 這種行為並不影響 DMX 函數。 如需詳細資訊，請參閱[BottomPercent &#40;MDX&#41;](../mdx/bottompercent-mdx.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;的函數 &#40;](../dmx/functions-dmx.md)  
  
  
