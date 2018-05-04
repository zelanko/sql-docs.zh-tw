---
title: PredictAssociation (DMX) |Microsoft 文件
ms.custom: ''
ms.date: 09/14/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PredictAssociation
dev_langs:
- DMX
helpviewer_keywords:
- PredictAssociation function
ms.assetid: 33eb66b5-84c6-449f-aaae-316345bc4ad5
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 3a3fd8d22cd601fc26b53af35a4d101ffcaea3e4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  預測關聯的成員資格。  
  
例如，您可以使用 PredictAssociation 函數以取得建議給客戶的購物籃的目前狀態的集合。 
  
## <a name="syntax"></a>語法  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>適用於  
 包含可預測的巢狀的資料表，包括關聯和某些分類演算法的演算法。 支援巢狀的資料表的分類演算法包括[!INCLUDE[msCoName](../includes/msconame-md.md)]決策樹[!INCLUDE[msCoName](../includes/msconame-md.md)]貝氏機率分類和[!INCLUDE[msCoName](../includes/msconame-md.md)]類神經網路演算法。  
  
## <a name="return-type"></a>傳回類型  
 \<資料表運算式 >  
  
## <a name="remarks"></a>備註  
 選項**PredictAssociation**函式包括 EXCLUDE_NULL、 INCLUDE_NULL、 INCLUSIVE、 EXCLUSIVE （預設）、 INPUT_ONLY、 INCLUDE_STATISTICS 和 INCLUDE_NODE_ID。  
  
> [!NOTE]  
>  INCLUSIVE、EXCLUSIVE、INPUT_ONLY 與 INCLUDE_STATISTICS 只適用於資料表資料行參考，而 EXCLUDE_NULL 與 INCLUDE_NULL 只適用於純量資料行參考。  
  
 INCLUDE_STATISTICS 只會傳回 **$Probability**和 **$AdjustedProbability**。  
  
 如果數字參數*n*指定，則**PredictAssociation**函式會傳回前 n 個最可能的值根據機率：  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 如果您包含 **$AdjustedProbability**，陳述式傳回前*n*值根據 **$AdjustedProbability**。  
  
## <a name="examples"></a>範例  
 下列範例會使用**PredictAssociation**函數傳回的四項產品在 Adventure Works 資料庫中最有可能同時銷售。  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
下列範例會示範如何使用巢狀的資料表當做預測函數的輸入使用 SHAPE 子句。 SHAPE 查詢建立一個資料列集具有 customerId 做為一個資料行和巢狀的資料表做為第二個資料行，其中包含的產品已經帶來客戶的清單。 

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
 [資料採礦延伸模組&#40;DMX&#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
