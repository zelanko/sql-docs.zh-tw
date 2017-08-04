---
title: "註解 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '*/'
- /*
dev_langs:
- kbMDX
helpviewer_keywords:
- commenting characters
- /*...*/ (comment)
ms.assetid: 64434ae4-80ce-4634-86b8-4125dfaa7f61
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: fca15a526cbd5329c8116e751bda4959a46e1713
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="comment-mdx"></a>註解 (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [&#40;註解 &#41;&#40;MDX &#41;](../mdx/comment-mdx-double-slash.md)   
 [-&#40;註解 &#41;&#40;MDX &#41;](../mdx/comment-mdx-operator-reference.md)   
 [MDX 運算子參考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

