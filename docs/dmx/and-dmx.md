---
title: 和 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0c727e6a6f981dd2862575bfb4943b104196080
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913741"
---
# <a name="and-dmx"></a>AND (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在兩個數值運算式上執行邏輯結合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>參數  
 *Expression1*  
 有效的資料採礦延伸模組 (DMX) 運算式，會傳回數值。  
  
 *Expression2*  
 傳回數值的有效 DMX 運算式。  
  
## <a name="return-value"></a>傳回值  
 一個布林值，如果兩個參數都評估為 TRUE，就會傳回 TRUE；否則為 FALSE。  
  
## <a name="remarks"></a>備註  
 運算子執行邏輯結合之前，兩個參數都當成布林值處理 (0 為 FALSE；否則為 TRUE)。 下表會列出根據參數值的各種組合傳回的值。  
  
|如果 Expression1 為|如果 Expression2 為|傳回值為|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|FALSE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [邏輯運算子&#40;DMX&#41;](../dmx/operators-logical.md)   
 [運算子&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
