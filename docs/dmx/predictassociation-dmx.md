---
title: PredictAssociation (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7a23407b546bcde2dd1fde81654da4fe861e0719
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62501834"
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  預測關聯的成員資格。  
  
比方說，您可以使用 PredictAssociation 函式，以取得建議給客戶的購物籃的目前狀態的集合。 
  
## <a name="syntax"></a>語法  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>適用於  
 包含可預測的巢狀的資料表，包括關聯和一些分類演算法的演算法。 支援巢狀的資料表的分類演算法包括[!INCLUDE[msCoName](../includes/msconame-md.md)]決策樹[!INCLUDE[msCoName](../includes/msconame-md.md)]貝氏機率分類和[!INCLUDE[msCoName](../includes/msconame-md.md)]類神經網路演算法。  
  
## <a name="return-type"></a>傳回類型  
 \<資料表運算式 >  
  
## <a name="remarks"></a>備註  
 選項**PredictAssociation**函式包括 EXCLUDE_NULL、 INCLUDE_NULL、 INCLUSIVE、 EXCLUSIVE （預設）、 INPUT_ONLY、 INCLUDE_STATISTICS 與 INCLUDE_NODE_ID。  
  
> [!NOTE]  
>  INCLUSIVE、EXCLUSIVE、INPUT_ONLY 與 INCLUDE_STATISTICS 只適用於資料表資料行參考，而 EXCLUDE_NULL 與 INCLUDE_NULL 只適用於純量資料行參考。  
  
 INCLUDE_STATISTICS 只會傳回 **$Probability**並 **$AdjustedProbability**。  
  
 如果將數字參數*n*指定，則**PredictAssociation**函式會傳回根據機率的前 n 個最可能值：  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 如果您納入 **$AdjustedProbability**，此陳述式傳回前*n*值根據 **$AdjustedProbability**。  
  
## <a name="examples"></a>範例  
 下列範例會使用**PredictAssociation**函式傳回的四種產品，在 Adventure Works 資料庫，最有可能一起銷售。  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
下列範例會示範如何使用巢狀的資料表當做預測函式中，輸入使用 SHAPE 子句。 SHAPE 查詢會使用 customerId 做為一個資料行和巢狀的資料表做為第二個資料行，其中包含客戶已經已經給了的產品清單建立資料列集。 

~~~~
SELECT T.[CustomerId], PredictAssociation(MyNestedTable, 5) // returns top 5 associated items
FROM My Model
PREDICTION JOIN
SHAPE {
    OPENQUERY([Adventure Works DW],'SELECT CustomerID, OrderNumber
    FROM vAssocSeqOrders ORDER BY OrderNumber')
} APPEND (
    {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, model FROM 
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}
  RELATE OrderNumber to OrderNumber) AS T
~~~~  

  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;函式參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
