---
description: 除 (MDX)
title: 除以 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0999df34ff817131e890afade89fc5daad85796b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484011"
---
# <a name="divide-mdx"></a>除 (MDX)


  執行除法運算，並傳回替代結果或除以 0 的 BLANK()。  
  
## <a name="syntax"></a>語法  
  
```  
  
Divide (<numerator>, <denominator> [,<alternateresult>])  
```  
  
## <a name="arguments"></a>引數  
 *分子*  
 被除數或要除以的數字。  
  
 *分母*  
 除數或要除的數字。  
  
 *alternateResult*  
 (選擇性) 除以零產生錯誤結果時所傳回的值。 未提供時，預設值為 BLANK()。  
  
## <a name="remarks"></a>備註  
 除以 0 的替代結果必須是常數。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
