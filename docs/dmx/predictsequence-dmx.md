---
title: PredictSequence (DMX) |Microsoft 文件
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 813641b7fa72405a0ba5a026e255f03feb94bd05
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841551"
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
 A\<資料表運算式 >。  
  
## <a name="remarks"></a>備註  
 如果*n*指定參數，它會傳回下列值：  
  
-   如果*n*大於零，最可能的時序值，在下一個*n*步驟。  
  
-   如果兩個*n 開始*和*n 端*指定，則序列中的值*n 開始*至*n 結束*。  
  
## <a name="examples"></a>範例  
 下列範例根據時序群集採礦模型，傳回 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 資料庫中客戶最可能購買的五項產品。  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
