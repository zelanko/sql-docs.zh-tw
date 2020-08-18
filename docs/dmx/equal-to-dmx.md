---
description: = (等於) (DMX)
title: = (等於)  (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ba57583c8af1b739335abc27c33eaaf2ea54dc1f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413355"
---
# <a name="-equal-to-dmx"></a>= (等於) (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  執行比較作業，判斷某個資料採礦延伸模組 (DMX) 運算式的值是否等於另一個 DMX 運算式的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
DMX_Expression = DMX_Expression   
```  
  
#### <a name="parameters"></a>參數  
 *DMX_Expression*  
 有效的 DMX 運算式。  
  
## <a name="return-value"></a>傳回值  
 一個布林值，其中如果兩個參數都為非 Null，而且第一個參數的值等於第二個參數的值，則為 TRUE。 如果兩個參數都為非 Null，而且第一個參數的值不等於第二個參數的值，則布林值為 FALSE。 如果任一個參數或兩個參數都評估為 Null 值，則布林值為 Null 值。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;DMX&#41;的比較運算子 ](../dmx/operators-comparison.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX &#40;的運算子&#41;](../dmx/operators-dmx.md)  
  
  
