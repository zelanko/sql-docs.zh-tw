---
description: TopPercent (DMX)
title: TopPercent (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f1193e43a00fc4c20487a92e8df3a9f705fa4490
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726075"
---
# <a name="toppercent-dmx"></a>TopPercent (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  **TopPercent**函式會依遞減排名的順序，傳回累計總和至少為指定百分比之資料表的最上層資料列。  
  
## <a name="syntax"></a>Syntax  
  
```  
  
TopPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="applies-to"></a>套用至  
 傳回資料表的運算式，例如 \<table column reference> ，或傳回資料表的函數。  
  
## <a name="return-type"></a>傳回類型  
 \<table expression>  
  
## <a name="remarks"></a>備註  
 **TopPercent**函數會根據每個資料列引數的評估值，以遞減的次序順序傳回最上層的 \<rank expression> 資料列，因此值的總和 \<rank expression> 至少是引數所指定的指定百分比 \<percent> 。 當仍然符合指定的百分比值時， **TopPercent**會傳回可能的最小元素數目。  
  
## <a name="examples"></a>範例  
 下列範例會針對您使用「 [基本資料採礦」教學](/previous-versions/sql/sql-server-2016/ms167167(v=sql.130))課程所建立的關聯模型建立預測查詢。  
  
 若要瞭解 TopPercent 的運作方式，請先執行僅傳回嵌套資料表的預測查詢，這可能會很有説明。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  在此範例中，當做輸入提供的值包含單引號，因此必須在該值前面加上另一個單引號來逸出。 如果您不確定插入逸出字元的語法，可以使用預測查詢產生器來建立查詢。 當您從下拉式清單選取值時，就會為您插入所需的逸出字元。 如需詳細資訊，請參閱 [在資料採礦設計師中建立單一查詢](/analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer)。  
  
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
  
 TopPercent 函式會採用此查詢的結果，並傳回具有最大值的資料列加總為指定的百分比。  
  
```  
SELECT   
TopPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 TopPercent 函數的第一個引數是資料表資料行的名稱。 在此範例中，會藉由呼叫 Predict 函數並使用 INCLUDE_STATISTICS 引數來傳回嵌套資料表。  
  
 TopPercent 函數的第二個引數是用來排序結果的嵌套資料表中的資料行。 在此範例中，INCLUDE_STATISTICS 選項會傳回資料行 $SUPPORT、$PROBABILTY 和 $ADJUSTED PROBABILITY。 此範例因為支援值不是分數而使用 $SUPPORT，因此比較容易確認。  
  
 TopPercent 函數的第三個引數會將百分比指定為雙精度浮點數。 若要取得總和為支援總計之百分之 50 的重要產品資料列，請輸入 50。  
  
 範例結果︰  
  
|模型|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29 .。。|0.25 .。。|  
|Water Bottle|2866|0.19 .。。|0.17 .。。|  
|Patch kit|2113|0.14 .。。|0.13 .。。|  
|Mountain Tire Tube|1992|0.133 .。。|0.12 .。。|  
  
 **注意** 此範例僅提供用來說明 TopPercent 的使用方式。 根據資料集的大小而定，此查詢可能會花上很長的一段執行時間。  
  
> [!WARNING]  
>  當用來計算百分比的值包含負數時，TOPPERCENT 和 BOTTOMPERCENT 的 MDX 函數會產生非預期的結果。 這種行為並不影響 DMX 函數。 如需詳細資訊，請參閱 [BottomPercent &#40;MDX&#41;](../mdx/bottompercent-mdx.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數 ](../dmx/general-prediction-functions-dmx.md)  
  
