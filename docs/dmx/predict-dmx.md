---
title: "預測 (DMX) |Microsoft 文件"
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
- PREDICT
dev_langs:
- DMX
helpviewer_keywords:
- Predict function
ms.assetid: f02ff4b3-9bd7-409d-ad14-ead67b3206c4
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a976011c3b892d826d29038fb0501e57db4c5008
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **預測**函式會傳回一組值，指定之資料行或預測的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>適用於  
 純量資料行參考或資料表資料行參考。  
  
## <a name="return-type"></a>傳回類型  
 \<純量資料行參考 >  
  
 或  
  
 \<資料表資料行參考 >  
  
 傳回類型會視這個函數適用的資料行類型而定。  
  
> [!NOTE]  
>  INCLUSIVE、EXCLUSIVE、INPUT_ONLY 與 INCLUDE_STATISTICS 只適用於資料表資料行參考，而 EXCLUDE_NULL 與 INCLUDE_NULL 只適用於純量資料行參考。  
  
## <a name="remarks"></a>備註  
 選項包括 EXCLUDE_NULL (預設)、INCLUDE_NULL、INCLUSIVE、EXCLUSIVE (預設)、INPUT_ONLY，以及 INCLUDE_STATISTICS。  
  
> [!NOTE]  
>  時間序列模型，預測函式不支援 INCLUDE_STATISTICS。  
  
 INCLUDE_NODE_ID 參數會在結果中傳回 $NODEID 資料行。 NODE_ID 是針對特定案例執行預測的內容節點。 資料表資料行上使用預測時，這個參數是選擇性的。  
  
 *n* 參數適用於資料表資料行。 它會根據預測類型設定傳回的資料列數。 如果基礎資料行順序，它會呼叫**PredictSequence**函式。 如果基礎資料行是時間序列，它會呼叫**PredictTimeSeries**函式。 對於關聯類型的預測，它會呼叫**PredictAssociation**函式。  
  
 **預測**函數支援多型。  
  
 下列是經常使用的替代縮寫格式：  
  
-   [Gender] 是的替代**預測**([Gender]，EXCLUDE_NULL)。  
  
-   [Products Purchases] 是的替代**預測**([Products Purchases]，EXCLUDE_NULL，EXCLUSIVE)。  
  
    > [!NOTE]  
    >  這個函數的傳回類型本身視為資料行參考。 這表示**預測**函式可以當做其他接受資料行參考做為引數的函式的引數 (除了**預測**函式本身)。  
  
 將 INCLUDE_STATISTICS 傳遞至預測中，資料表值的資料行上加入資料行**$Probability**和**$Support**加入產生的資料表。 這些資料行描述相關聯之巢狀資料表記錄存在的機率。  
  
## <a name="examples"></a>範例  
 下列範例會使用預測函數，傳回最可能一起銷售的 Adventure Works 資料庫中的四項產品。 此函式針對在關聯規則採礦模型預測，因為它會自動使用**PredictAssociation**函式，如先前所述。  
  
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
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

