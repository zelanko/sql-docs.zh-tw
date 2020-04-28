---
title: 除（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6184aa9d932355cd935a9131848ec27895faea5f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68049304"
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
  
 *標準*  
 除數或要除的數字。  
  
 *alternateResult*  
 (選擇性) 除以零產生錯誤結果時所傳回的值。 未提供時，預設值為 BLANK()。  
  
## <a name="remarks"></a>備註  
 除以 0 的替代結果必須是常數。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
