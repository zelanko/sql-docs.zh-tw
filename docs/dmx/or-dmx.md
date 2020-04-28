---
title: 或（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 76b1f8ac9a5f7ad584f42110f2c3b22e5c1918ff
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68008139"
---
# <a name="or-dmx"></a>OR (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在兩個數值運算式上執行邏輯分離的邏輯運算子。  
  
## <a name="syntax"></a>語法  
  
```  
  
Expression1 OR Expression2  
```  
  
#### <a name="parameters"></a>參數  
 *Expression1*  
 有效的資料採礦延伸模組 (DMX) 運算式，會傳回數值。  
  
 *Expression2*  
 傳回數值的有效 DMX 運算式。  
  
## <a name="return-value"></a>傳回值  
 一個布林值，如果任一個引數或兩個引數都評估為 TRUE，就會傳回 TRUE；否則為 FALSE。  
  
## <a name="remarks"></a>備註  
 運算子執行邏輯分離之前，兩個引數都會當成布林值處理 (0 為 FALSE；否則為 TRUE)。 如果任一個引數或兩個引數都評估為 TRUE，則運算子會傳回 TRUE。 如果*運算式*的評估結果為 TRUE，且*運算式*2 判斷值為 FALSE，則運算子會傳回 TRUE。  
  
 下表說明如何執行邏輯分離。  
  
|如果 Expression1 為|如果 Expression2 為|傳回值為|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|TRUE|  
|FALSE|TRUE|TRUE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>另請參閱  
 [DMX&#41; Operator Reference &#40;的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [&#40;DMX&#41;的邏輯運算子](../dmx/operators-logical.md)   
 [DMX&#41;&#40;的運算子](../dmx/operators-dmx.md)  
  
  
