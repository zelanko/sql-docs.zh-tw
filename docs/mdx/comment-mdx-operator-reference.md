---
title: -（註解） (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 564327619cabc00684b064585aa323c9426597c2
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577370"
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
  
## <a name="see-also"></a>另請參閱  
 [註解 &#40;MDX&#41;](../mdx/comment-mdx.md)   
 [&#40;註解&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)   
 [MDX 運算子參考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
