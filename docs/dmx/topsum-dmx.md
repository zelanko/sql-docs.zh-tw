---
title: TopSum (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e94af73873414f1486908b63b508143093194508
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606588"
---
# <a name="topsum-dmx"></a>TopSum (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  以遞減次序的順序，傳回累計總和至少達指定值的最頂部資料表資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
TopSum(<table expression>, <rank expression>, <sum>)  
```  
  
## <a name="applies-to"></a>適用於  
 該運算式會傳回資料表，例如\<資料表資料行參考 >，或傳回資料表的函式。  
  
## <a name="return-type"></a>傳回類型  
 \<資料表運算式 >  
  
## <a name="remarks"></a>備註  
 **TopSum**函式會傳回最頂部資料列的已評估值為基礎的順位的遞減順序\<排名運算式 > 引數，每個資料列，使總和\<排名運算式 >值至少是所指定的給定的總和\<總和 > 引數。 **TopSum**傳回符合指定的總和值的可能最小元素數目。  
  
## <a name="examples"></a>範例  
 下列範例會建立預測查詢的關聯模型，您使用建置[83c8-9df5dddfeb9c"&gt;basic Data Mining Tutorial&lt](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。  
  
 若要了解 TopPercent 的運作方式，可能要先執行僅傳回巢狀的資料表的預測查詢很有幫助。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  在此範例中，當做輸入提供的值包含單引號，因此必須在該值前面加上另一個單引號來逸出。 如果您不確定插入逸出字元的語法，可以使用預測查詢產生器來建立查詢。 當您從下拉式清單選取值時，就會為您插入所需的逸出字元。 如需詳細資訊，請參閱 <<c0> [ 資料採礦設計師中建立單一查詢](../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md)。  
  
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
  
 **TopSum**函式會採用此查詢的結果，並傳回具有最大值的資料列加總為指定計數。  
  
```  
SELECT   
TopSum  
    (  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $PROBABILITY,  
    .5)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 第一個引數**TopSum**函式是資料表資料行的名稱。 在此範例中，巢狀的資料表會傳回呼叫 Predict 函式，並使用 INCLUDE_STATISTICS 引數。  
  
 第二個引數**TopSum**函式是巢狀資料表，您用來排序結果中的資料行。 在此範例中，INCLUDE_STATISTICS 選項會傳回資料行 $SUPPORT、$PROBABILTY 和 $ADJUSTED PROBABILITY。 此範例會使用 $PROBABILITY 傳回加總為至少 50% 機率的資料列。  
  
 第三個引數**TopSum**函式會將目標總和指定為雙精度浮點數。 若要取得加總為百分之 50 機率之重要產品的資料列，請輸入 .5。  
  
 範例結果：  
  
|[模型]|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29…|0.25…|  
|Water Bottle|2866|0.19…|0.17…|  
|Patch kit|2113|0.14…|0.13…|  
  
 **附註**這個範例提供只是為了說明的使用方式**TopSum**。 根據資料集的大小而定，此查詢可能會花上很長的一段執行時間。  
  
## <a name="see-also"></a>另請參閱  
 [函式&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)  
  
  
