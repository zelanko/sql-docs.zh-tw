---
title: PredictSequence (DMX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
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
- PredictSequence
dev_langs:
- DMX
helpviewer_keywords:
- PredictSequence function
ms.assetid: c2992dfc-b99d-4430-8dcd-21ad3ffd4590
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b8ef0b3f0ba361e368695b31d15b26cd013ed6e8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
  
  
