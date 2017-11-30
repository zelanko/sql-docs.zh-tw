---
title: "StdevP (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: STDEVP
dev_langs: kbMDX
helpviewer_keywords: StdevP function [MDX]
ms.assetid: cd8ae7c9-3cef-49f0-bb41-8f577c7b6f31
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9cf8116a2aecec959c105515e8765496a55afb0d
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="stdevp-mdx"></a>StdevP (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回使用偏誤的母體公式，在集合評估後數值運算式的母體擴展標準差 (除以 *n* )。  
  
## <a name="syntax"></a>語法  
  
```  
  
StdevP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **StdevP**函數使用偏誤的母體公式，而[Stdev](../mdx/stdev-mdx.md)函式會使用非偏誤的母體公式。  
  
## <a name="example"></a>範例  
 下列範例使用偏誤母體公式，針對 2003 日曆年度前三個月評估後，傳回 Internet Order Quantity 的標準差。  
  
```  
WITH MEMBER Measures.x AS   
   StdevP   
   ( { [Date].[Calendar].[Month].[January 2003],  
       [Date].[Calendar].[Month].[February 2003],  
       [Date].[Calendar].[Month].[March 2003]},  
    [Measures].[Internet Order Quantity])  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
