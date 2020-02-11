---
title: 批註（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f0aa1455ffd9f52fd917f68d2bb0bb80e3f25a94
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006269"
---
# <a name="comment-mdx"></a>批註（MDX）


  指出使用者提供的註解文字。  
  
## <a name="syntax"></a>語法  
  
```  
  
/* Comment_Text */      
```  
  
#### <a name="parameters"></a>參數  
 *Comment_Text*  
 包含註解文字的字串。  
  
## <a name="remarks"></a>備註  
 伺服器不會評估批註字元/* 和\*/之間的文字。 註解可以插在單獨一行或多維度運算式 (MDX) 陳述式之中。 多行批註必須以/\*和\*/表示。  
  
 註解沒有長度上限。 註解可以為巢狀；例如 `/* Test /*Comment*/ Text*/` 就是巢狀註解的範例。  
  
## <a name="examples"></a>範例  
 以下範例示範此運算子的用法。  
  
```  
/* This member returns the gross profit margin for product types  
  and reseller types crossjoined by year. */  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM /* Select from the Adventure Works cube. */  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;批註&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)   
 [--&#40;批註&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
