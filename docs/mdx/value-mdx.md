---
description: Value (MDX)
title: " (MDX) 的值 |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 52224625f5e2e6fc70ca9a76f750ed374108c52c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196726"
---
# <a name="value-mdx"></a>Value (MDX)


  傳回查詢內容中與屬性階層目前成員交集之 Measures 維度的目前成員值。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression[.Value]   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **值**函數會以字串形式傳回指定成員的值。 **值**引數是選擇性的，因為成員的值是成員的預設屬性，而如果沒有指定其他值，則是針對成員傳回的值。 如需有關成員屬性的詳細資訊，請參閱 [&#40;mdx&#41;](/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) 的內建成員屬性，以及 [&#40;Mdx&#41;的使用者自訂成員屬性 ](/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties)。  
  
## <a name="examples"></a>範例  
 下列範例會傳回成員值，並且會明確傳回成員名稱。  
  
```  
WITH MEMBER [Date].[Calendar].NumericValue as [Date].[Calendar].[July 1, 2001].Value  
MEMBER [Date].[Calendar].MemberName AS [Date].[Calendar].[July 1, 2001].Name  
  
SELECT {[Date].[Calendar].NumericValue, [Date].[Calendar].MemberName} ON 0  
from [Adventure Works]  
```  
  
 下列範例會傳回成員值，做為座標軸上為成員傳回的預設值。  
  
```  
SELECT {[Date].[Calendar].[July 1, 2001]} ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MemberValue &#40;MDX&#41;](../mdx/membervalue-mdx.md)   
 [MDX&#41;&#40;屬性 ](../mdx/properties-mdx.md)   
 [MDX&#41;名稱 &#40;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
