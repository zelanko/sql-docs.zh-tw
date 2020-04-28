---
title: PredictSequence （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c6828b77af36b5dbbc50fbca0210961a7f2ed20c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68041918"
---
# <a name="predictsequence-dmx"></a>PredictSequence (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  預測指定之時序資料集合的未來時序值。  
  
## <a name="syntax"></a>語法  
  
```  
  
PredictSequence(<table column reference>)  
PredictSequence(\<table column reference, n>)  
PredictSequence(\<table column reference, n-start, n-end>)  
```  
  
## <a name="return-type"></a>傳回類型  
 \<資料表運算式>。  
  
## <a name="remarks"></a>備註  
 如果指定了*n*參數，它會傳回下列值：  
  
-   如果*n*大於零，則在接下來的*n*個步驟中最可能的順序值。  
  
-   如果同時指定了*n-start*和*n 結束*，則從*n-start*到*n-end*的順序值。  
  
## <a name="examples"></a>範例  
 下列範例根據時序群集採礦模型，傳回 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 資料庫中客戶最可能購買的五項產品。  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;的函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)  
  
  
