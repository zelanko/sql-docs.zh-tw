---
title: 預測（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9a21336db54ab6fadaa219a3ef3d743dcf860087
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669271"
---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **Predict**函數會針對指定的資料行傳回預測值或一組值。  
  
## <a name="syntax"></a>語法  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>套用至  
 純量資料行參考或資料表資料行參考。  
  
## <a name="return-type"></a>傳回類型  
 \<純量資料行參考>  
  
 或  
  
 \<資料表資料行參考>  
  
 傳回類型會視這個函數適用的資料行類型而定。  
  
> [!NOTE]  
>  INCLUSIVE、EXCLUSIVE、INPUT_ONLY 與 INCLUDE_STATISTICS 只適用於資料表資料行參考，而 EXCLUDE_NULL 與 INCLUDE_NULL 只適用於純量資料行參考。  
  
## <a name="remarks"></a>備註  
 選項包括 EXCLUDE_NULL (預設)、INCLUDE_NULL、INCLUSIVE、EXCLUSIVE (預設)、INPUT_ONLY，以及 INCLUDE_STATISTICS。  
  
> [!NOTE]  
>  針對時間序列模型，Predict 函數不支援 INCLUDE_STATISTICS。  
  
 INCLUDE_NODE_ID 參數會在結果中傳回 $NODEID 資料行。 NODE_ID 是針對特定案例執行預測的內容節點。 在資料表資料行上使用 Predict 時，這個參數是選擇性的。  
  
 *N*參數適用于資料表資料行。 它會根據預測類型設定傳回的資料列數。 如果基礎資料行是 sequence，它會呼叫**PredictSequence**函數。 如果基礎資料行是時間序列，它會呼叫**PredictTimeSeries**函數。 對於關聯類型的預測，它會呼叫**PredictAssociation**函數。  
  
 **Predict**函數支援多型。  
  
 下列是經常使用的替代縮寫格式：  
  
-   [性別] 是**預測**（[性別]，EXCLUDE_Null）的替代方案。  
  
-   [購買的產品] 是**預測**（[購買產品]，EXCLUDE_Null，獨家）的替代方案。  
  
    > [!NOTE]  
    >  這個函數的傳回類型本身視為資料行參考。 這表示**predict**函數可以做為其他函數中的引數使用，以資料行參考做為引數（ **Predict**函數本身除外）。  
  
 將 INCLUDE_STATISTICS 傳遞至資料表值資料行的預測，會將 **$Probability**和 **$Support**的資料行加入至產生的資料表。 這些資料行描述相關聯之巢狀資料表記錄存在的機率。  
  
## <a name="examples"></a>範例  
 下列範例會使用 Predict 函式，傳回「艾德公司」資料庫中最可能一起銷售的四個產品。 因為函式是根據關聯規則採礦模型進行預測，所以它會自動使用**PredictAssociation**函數，如先前所述。  
  
```  
SELECT  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,4)  
FROM     [Association]  
```  
  
 範例結果：  
  
 此查詢會傳回包含一個資料行 `Expression` 之資料的單一資料列，但是該資料行包含下列巢狀資料表。  
  
|型號|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016331743|0.252695851192499|  
|Water Bottle|2866|0.192620471805901|0.175205052318795|  
|Patch Kit|2113|0.142012232004839|0.132389356196586|  
|Mountain Tire Tube|1992|0.133879965051415|0.125304947722259|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;的函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)  
  
  
