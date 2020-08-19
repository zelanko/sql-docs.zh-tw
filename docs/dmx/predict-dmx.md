---
description: Predict (DMX)
title: 預測 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4f53f331b078fce4f02e548a83a145dce8ba6a91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426200"
---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  **Predict**函數會針對指定的資料行傳回預測值或一組值。  
  
## <a name="syntax"></a>語法  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>套用至  
 純量資料行參考或資料表資料行參考。  
  
## <a name="return-type"></a>傳回類型  
 \<scalar column reference>  
  
 或  
  
 \<table column reference>  
  
 傳回類型會視這個函數適用的資料行類型而定。  
  
> [!NOTE]  
>  INCLUSIVE、EXCLUSIVE、INPUT_ONLY 與 INCLUDE_STATISTICS 只適用於資料表資料行參考，而 EXCLUDE_NULL 與 INCLUDE_NULL 只適用於純量資料行參考。  
  
## <a name="remarks"></a>備註  
 選項包括 EXCLUDE_NULL (預設)、INCLUDE_NULL、INCLUSIVE、EXCLUSIVE (預設)、INPUT_ONLY，以及 INCLUDE_STATISTICS。  
  
> [!NOTE]  
>  在時間序列模型中，Predict 函數不支援 INCLUDE_STATISTICS。  
  
 INCLUDE_NODE_ID 參數會在結果中傳回 $NODEID 資料行。 NODE_ID 是針對特定案例執行預測的內容節點。 在資料表資料行上使用 Predict 時，此參數是選擇性的。  
  
 *N*參數適用于資料表資料行。 它會根據預測類型設定傳回的資料列數。 如果基礎資料行是 sequence，則會呼叫 **PredictSequence** 函數。 如果基礎資料行是時間序列，則會呼叫 **PredictTimeSeries** 函數。 若為關聯類型的預測，則會呼叫 **PredictAssociation** 函數。  
  
 **Predict**函數支援多型。  
  
 下列是經常使用的替代縮寫格式：  
  
-   [性別] 是 **預測** ( [性別]、EXCLUDE_Null) 的替代方案。  
  
-   [產品購買] 是 **預測** ( [產品購買]、EXCLUDE_Null、專屬) 的替代方案。  
  
    > [!NOTE]  
    >  這個函數的傳回類型本身視為資料行參考。 這表示 **predict** 函式可以當做其他函數中的引數使用，這些函數會採用資料行參考做為引數 (但 **Predict** 函數本身) 除外。  
  
 將 INCLUDE_STATISTICS 傳遞給資料表值資料行的預測，會將資料行 **$Probability** 和 **$Support** 加入至結果資料表。 這些資料行描述相關聯之巢狀資料表記錄存在的機率。  
  
## <a name="examples"></a>範例  
 下列範例會使用 Predict 函式來傳回「艾德作品」資料庫中最有可能一起銷售的四項產品。 因為函式是針對關聯規則採礦模型進行預測，所以會自動使用先前所述的 **PredictAssociation** 函數。  
  
```  
SELECT  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,4)  
FROM     [Association]  
```  
  
 範例結果：  
  
 此查詢會傳回包含一個資料行 `Expression` 之資料的單一資料列，但是該資料行包含下列巢狀資料表。  
  
|模型|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016331743|0.252695851192499|  
|Water Bottle|2866|0.192620471805901|0.175205052318795|  
|Patch Kit|2113|0.142012232004839|0.132389356196586|  
|Mountain Tire Tube|1992|0.133879965051415|0.125304947722259|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數 ](../dmx/general-prediction-functions-dmx.md)  
  
  
