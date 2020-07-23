---
title: PredictAssociation （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a834c87c3febf0554ad07334000d62f1f9a93fee
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "86968192"
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  預測關聯的成員資格。  
  
例如，您可以使用 PredictAssociation 函式，根據客戶的購物籃目前狀態來取得建議集合。 
  
## <a name="syntax"></a>Syntax  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>套用至  
 包含可預測的嵌套資料表的演算法，包括關聯和一些分類演算法。 支援嵌套資料表的分類演算法包括 [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹、 [!INCLUDE[msCoName](../includes/msconame-md.md)] 貝氏貝氏機率分類和類 [!INCLUDE[msCoName](../includes/msconame-md.md)] 神經網路演算法。  
  
## <a name="return-type"></a>傳回類型  
 \<table expression>  
  
## <a name="remarks"></a>備註  
 **PredictAssociation**函數的選項包括 EXCLUDE_Null、INCLUDE_Null、內含、獨佔（預設）、INPUT_ONLY、INCLUDE_STATISTICS 和 INCLUDE_NODE_ID。  
  
> [!NOTE]  
>  INCLUSIVE、EXCLUSIVE、INPUT_ONLY 與 INCLUDE_STATISTICS 只適用於資料表資料行參考，而 EXCLUDE_NULL 與 INCLUDE_NULL 只適用於純量資料行參考。  
  
 INCLUDE_STATISTICS 只會傳回 **$Probability**和 **$AdjustedProbability**。  
  
 如果指定了數值參數*n* ， **PredictAssociation**函數會根據機率傳回前 n 個最可能的值：  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 如果您包含 **$AdjustedProbability**，語句會根據 **$AdjustedProbability**傳回前*n*個值。  
  
## <a name="examples"></a>範例  
 下列範例會使用**PredictAssociation**函式，傳回「艾德作品」資料庫中最可能一起銷售的四個產品。  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
下列範例會示範如何使用 SHAPE 子句，將嵌套資料表當做預測函數的輸入。 SHAPE 查詢會建立一個資料列集，其中包含 customerId 當做一個資料行，而另一個嵌套資料表則是第二欄，其中包含客戶已提供的產品清單。 

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
 [DMX&#41;的函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)  
  
  
