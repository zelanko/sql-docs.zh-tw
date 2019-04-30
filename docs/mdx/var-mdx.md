---
title: Var (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 14caf6e96b41fdf2e7f8b4d20f16852e890bd166
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251517"
---
# <a name="var-mdx"></a>Var (MDX)


  傳回使用非偏誤的母體公式，在集合評估後數值運算式的樣本變異數 (除以*n*)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Var(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **Var**函式會傳回指定的集合上評估指定數值運算式的非偏誤變異數。  
  
 **Var**函式會使用非偏誤的母體公式，而[VarP](../mdx/varp-mdx.md)函數使用偏誤的母體公式。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
