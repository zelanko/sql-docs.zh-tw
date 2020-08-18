---
description: OR (DMX)
title: 或 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 86a9aede9f1b9b12f465fa52b0343cf22c04b295
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88395434"
---
# <a name="or-dmx"></a>OR (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

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
 運算子執行邏輯分離之前，兩個引數都會當成布林值處理 (0 為 FALSE；否則為 TRUE)。 如果任一個引數或兩個引數都評估為 TRUE，則運算子會傳回 TRUE。 如果 *運算式* 值評估為 TRUE，且 *運算式* 評估為 FALSE，則運算子會傳回 true。  
  
 下表說明如何執行邏輯分離。  
  
|如果 Expression1 為|如果 Expression2 為|傳回值為|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|true|false|true|  
|false|TRUE|true|  
|false|false|false|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [&#40;DMX&#41;的邏輯運算子 ](../dmx/operators-logical.md)   
 [DMX &#40;的運算子&#41;](../dmx/operators-dmx.md)  
  
  
