---
title: 註解 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6469921572b8a1809e228fff0d25061475399ae7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181575"
---
# <a name="comment-mdx"></a>註解 (MDX)


  指出使用者提供的註解文字。  
  
## <a name="syntax"></a>語法  
  
```  
  
/* Comment_Text */      
```  
  
#### <a name="parameters"></a>參數  
 *Comment_Text*  
 包含註解文字的字串。  
  
## <a name="remarks"></a>備註  
 伺服器不會評估註解字元之間的文字 / * 和\*/。 註解可以插在單獨一行或多維度運算式 (MDX) 陳述式之中。 多行註解必須以 /\*和\*/。  
  
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
 [&#40;Comment&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)   
 [-- &#40;註解&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [MDX 運算子參考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
