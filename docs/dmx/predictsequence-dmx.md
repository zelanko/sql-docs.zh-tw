---
title: "PredictSequence (DMX) |Microsoft 文件"
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e9ddd402be082937ec828a86d82a238d121e55dd
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="predictsequence-dmx"></a>PredictSequence (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 如果 *n* 指定參數，它會傳回下列值：  
  
-   如果 *n* 大於零，最可能的時序值，在下一個 *n* 步驟。  
  
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
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函式 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

