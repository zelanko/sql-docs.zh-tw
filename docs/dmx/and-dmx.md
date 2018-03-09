---
title: "和 (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: AND
dev_langs: DMX
helpviewer_keywords: AND, DMX
ms.assetid: d337b20c-f80e-48be-9354-371367e53735
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4acd3c33863e8e8c198480e4cc90e4661f7acf94
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
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
  
## <a name="see-also"></a>請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [邏輯運算子 &#40; DMX &#41;](../dmx/operators-logical.md)   
 [運算子 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
