---
title: 值 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f373f626d778c4d77ec5843dca5bb11da728451d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887450"
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
 **Value**函式會以字串形式傳回指定成員的值。 **值**引數是選擇性的, 因為成員的值是成員的預設屬性, 而如果未指定其他值, 則是針對成員傳回的值。 如需成員屬性的詳細資訊, 請參閱[內部成員&#40;屬性&#41; mdx](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties)和[使用者自訂成員&#40;屬性&#41;mdx](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties)。  
  
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
 [Properties &#40;MDX&#41;](../mdx/properties-mdx.md)   
 [名稱&#40;MDX&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
