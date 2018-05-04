---
title: Var (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- VAR
dev_langs:
- kbMDX
helpviewer_keywords:
- Var function [MDX]
ms.assetid: 5575b68e-ebc1-4eaf-9547-1321d495ea62
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: d70b4797bcc493fd85daad02b99566dda8a11557
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="var-mdx"></a>Var (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回的樣本變異數的數值運算式，評估集合，使用非偏誤的母體公式 (除以*n*)。  
  
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
 **Var**函式會傳回指定的集合上評估指定數值運算式的偏誤變異數。  
  
 **Var**函式使用非偏誤的母體公式，而[VarP](../mdx/varp-mdx.md)函數使用偏誤的母體公式。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
