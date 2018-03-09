---
title: "-（註解） (MDX) |Microsoft 文件"
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
f1_keywords: --
dev_langs: kbMDX
helpviewer_keywords:
- commenting characters
- -- (comment character)
ms.assetid: 02aec133-6809-4829-b9a2-102c376e21da
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2bcafeb6ee60d42f63780f4479ae0c7ccd2f7eba
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="comment---mdx-operator-reference"></a>註解-MDX 運算子參考
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指出使用者提供的註解文字。  
  
## <a name="syntax"></a>語法  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>參數  
 *Comment_Text*  
 包含註解文字的字串。  
  
## <a name="remarks"></a>備註  
 程式註解可以在多維度運算式 (MDX) 指令碼行後面，或在 MDX 陳述式內，以單獨一行巢狀插入。 伺服器不會評估註解。  
  
 在單行或巢狀註解使用這個運算子。 使用 -- 插入的程式註解由新行字元分隔。  
  
 註解沒有長度上限。  
  
## <a name="examples"></a>範例  
 以下範例示範此運算子的用法。  
  
```  
-- This member returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
      [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM -- Select from the Adventure Works cube.  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>請參閱  
 [註解 &#40;MDX&#41;](../mdx/comment-mdx.md)   
 [&#40;註解 &#41;&#40;MDX &#41;](../mdx/comment-mdx-double-slash.md)   
 [MDX 運算子參考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
