---
title: "VarP (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: VARP
dev_langs: kbMDX
helpviewer_keywords: VarP function [MDX]
ms.assetid: feca648d-bbc8-44c8-9a0e-38f66d914c72
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b149d346c3caba0c573f5e3f85ad6647b2e178b0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="varp-mdx"></a>VarP (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回使用偏誤的母體公式，在集合評估後數值運算式的母體擴展變異數 (除以 *n* -1)。  
  
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
 **VarP**函式會傳回指定的數值運算式，評估指定集合的偏誤變異數。  
  
 **VarP**函數使用偏誤的母體公式，而[Var](../mdx/var-mdx.md)函式會使用非偏誤的母體公式。  
  
## <a name="see-also"></a>請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
