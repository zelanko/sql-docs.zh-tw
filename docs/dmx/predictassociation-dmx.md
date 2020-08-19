---
description: PredictAssociation (DMX)
title: PredictAssociation (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b94af0ab8da71e5bf978852fd884d46b460715bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426150"
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  預測關聯的成員資格。  
  
例如，您可以使用 PredictAssociation 函式，根據客戶的購物籃目前狀態來取得建議集合。 
  
## <a name="syntax"></a>語法  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>套用至  
 包含可預測的嵌套資料表（包括關聯和某些分類演算法）的演算法。 支援嵌套資料表的分類演算法包括 [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹、 [!INCLUDE[msCoName](../includes/msconame-md.md)] 貝氏貝氏機率分類和類 [!INCLUDE[msCoName](../includes/msconame-md.md)] 神經網路演算法。  
  
## <a name="return-type"></a>傳回類型  
 \<table expression>  
  
## <a name="remarks"></a>備註  
 **PredictAssociation**函數的選項包括 EXCLUDE_Null、INCLUDE_Null、內含、專有 (預設) 、INPUT_ONLY、INCLUDE_STATISTICS 和 INCLUDE_NODE_ID。  
  
> [!NOTE]  
>  INCLUSIVE、EXCLUSIVE、INPUT_ONLY 與 INCLUDE_STATISTICS 只適用於資料表資料行參考，而 EXCLUDE_NULL 與 INCLUDE_NULL 只適用於純量資料行參考。  
  
 INCLUDE_STATISTICS 只會傳回 **$Probability** 和 **$AdjustedProbability**。  
  
 如果指定數值參數 *n* ， **PredictAssociation** 函式會根據機率傳回前 n 個最可能的值：  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 如果您包含 **$AdjustedProbability**，語句會根據 **$AdjustedProbability**傳回前*n*個值。  
  
## <a name="examples"></a>範例  
 下列範例會使用 **PredictAssociation** 函式，傳回在艾德作品資料庫中最有可能一起銷售的四項產品。  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
下列範例示範如何使用 SHAPE 子句，將嵌套資料表作為預測函數的輸入。 SHAPE 查詢會建立一個資料列集，其中包含 customerId 做為一個資料行，而將一個嵌套資料表作為第二個數據行，其中包含客戶已提供的產品清單。 

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
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數 ](../dmx/general-prediction-functions-dmx.md)  
  
  
