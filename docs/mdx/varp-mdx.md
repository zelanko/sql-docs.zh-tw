---
description: VarP (MDX)
title: VarP (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c850ba60ac9900228c6adaa03aa97b46b1abddf1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429720"
---
# <a name="varp-mdx"></a>VarP (MDX)


  使用偏差擴展公式 (除以 *n-1*) ，傳回對集合進行評估之數值運算式的擴展變異數。  
  
## <a name="syntax"></a>語法  
  
```  
  
VarP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **VarP**函數會傳回指定之數值運算式的偏差變異數，並對指定的集合進行評估。  
  
 **VarP**函數使用偏誤擴展公式，而[Var](../mdx/var-mdx.md)函數使用非偏誤的人口公式。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
