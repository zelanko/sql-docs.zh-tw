---
title: "屬性 (MDX) |Microsoft 文件"
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
- Properties
dev_langs:
- kbMDX
helpviewer_keywords:
- Properties function
ms.assetid: 2d8442c5-30c4-4fd1-99ea-9845b6533e41
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c77317f1717cc2f4b637839e40836a2096fa517d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="properties-mdx"></a>Properties (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 **屬性**函式會傳回指定的成員屬性的指定成員的值。 成員屬性可以是任何內建成員屬性，例如**名稱**，**識別碼**，**金鑰**，或**標題**，也可以是使用者自訂成員屬性。 如需詳細資訊，請參閱[內建成員屬性 &#40;MDX &#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md)和[使用者自訂成員屬性 &#40;MDX &#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
 依預設，值會強制轉型成字串。 如果**具型別**指定，則傳回值強型別。  
  
-   如果為內建的屬性類型，此函數會傳回原始的成員類型。  
  
-   如果使用者定義的屬性類型，傳回值的類型是傳回值的型別相同**MemberValue**函式。  
  
> [!NOTE]  
>  Properties ('Key') 會傳回與 Key0 相同的結果，但複合索引鍵例外， 因為複合索引鍵的 Properties ('Key') 會傳回 Null。 使用金鑰*x*複合索引鍵，做為範例所示的語法。 Properties ('Key0')、Properties('Key1')、Properties('Key2') 等共同形成複合索引鍵。  
  
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
  
 下列範例示範如何使用索引鍵的*x*屬性。  
  
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
 [使用成員屬性 &#40;MDX &#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

