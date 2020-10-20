---
description: Properties (MDX)
title: MDX) 的屬性 (|Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cbdae47b3ede8ad2b22258e83a69b4f2776115d9
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192338"
---
# <a name="properties-mdx"></a>Properties (MDX)


  傳回包含成員屬性值的字串或強型別 (strongly-typed) 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.Properties(Property_Name [, TYPED])  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Property_Name*  
 成員屬性名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 **Properties**函數會傳回指定成員屬性的指定成員值。 成員屬性可以是任何內建成員屬性，例如 **名稱**、 **識別碼**、索引 **鍵**或 **標題**，也可以是使用者定義的成員屬性。 如需詳細資訊，請參閱 [&#40;mdx&#41;](/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) 的內建成員屬性，以及 [&#40;Mdx&#41;的使用者自訂成員屬性 ](/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties)。  
  
 依預設，值會強制轉型成字串。 如果指定了 **類型** ，則傳回值為強型別。  
  
-   如果為內建的屬性類型，此函數會傳回原始的成員類型。  
  
-   如果屬性類型是使用者定義的，則傳回值的類型與 **MemberValue** 函式之傳回值的類型相同。  
  
> [!NOTE]  
>  Properties ('Key') 會傳回與 Key0 相同的結果，但複合索引鍵例外， 因為複合索引鍵的 Properties ('Key') 會傳回 Null。 如範例所示，請使用複合索引鍵的索引鍵*x* 語法。 Properties ('Key0')、Properties('Key1')、Properties('Key2') 等共同形成複合索引鍵。  
  
## <a name="example"></a>範例  
 下列範例會傳回內建和使用者自訂成員屬性，並利用 TYPED 引數來傳回 Day Name 成員屬性的強型別值。  
  
```  
WITH MEMBER Measures.MemberName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Name')  
MEMBER Measures.MemberVal AS   
   [Date].[Calendar].[July 1, 2003].Properties('Member_Value')  
MEMBER Measures.MemberKey AS   
   [Date].[Calendar].[July 1, 2003].Properties('Key')  
MEMBER Measures.MemberID AS   
   [Date].[Calendar].[July 1, 2003].Properties('ID')  
MEMBER Measures.MemberCaption AS   
   [Date].[Calendar].[July 1, 2003].Properties('Caption')  
MEMBER Measures.DayName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name', TYPED)  
MEMBER Measures.DayNameTyped AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name')  
MEMBER Measures.DayofWeek AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Week')  
MEMBER Measures.DayofMonth AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Month')  
MEMBER Measures.DayofYear AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Year')  
  
SELECT {Measures.MemberName  
   , Measures.MemberVal  
   , Measures.MemberKey  
   , Measures.MemberID  
   , Measures.MemberCaption  
   , Measures.DayName  
   , Measures.DayNameTyped  
   , Measures.DayofWeek  
   , Measures.DayofMonth  
   , Measures.DayofYear  
   }  ON 0  
FROM [Adventure Works]  
```  
  
 下列範例示範如何使用 KEY*x* 屬性。  
  
```  
WITH   
MEMBER Measures.MemberKey AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key')  
MEMBER Measures.MemberKey0 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key0')  
MEMBER Measures.MemberKey1 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key1')  
  
SELECT {Measures.MemberKey  
   , Measures.MemberKey0  
   , Measures.MemberKey1     
   }  ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用成員屬性 &#40;MDX&#41;](/analysis-services/multidimensional-models/mdx/mdx-member-properties)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
