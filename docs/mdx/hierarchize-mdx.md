---
title: Hierarchize （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8ab2c866f201c53684c316282a143b4f672cb8e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68105428"
---
# <a name="hierarchize-mdx"></a>Hierarchize (MDX)


  以階層式架構排列集合成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Hierarchize(Set_Expression [ , POST ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **Hierarchize**函數會將指定集合的成員組織成階層式的順序。 此函數永遠會保留重複項。  
  
-   如果未指定**POST** ，函式會依其自然順序來排序層級中的成員。 未指定其他排序條件時，它們的自然順序就是階層中成員的預設順序。 子成員會直接跟隨在父成員後面。  
  
-   如果指定了**post** ， **Hierarchize**函數會使用後置的順序來排序層級中的成員。 換言之，子成員會在其父系之前。  
  
## <a name="example"></a>範例  
 下列範例會在 Canada 成員向上鑽研。 **Hierarchize**函數是用來以階層順序組織指定的集合成員，這是**DrillUpMember**函數所需的。  
  
```  
SELECT DrillUpMember   
   (  
      Hierarchize  
         (  
            {[Geography].[Geography].[Country].[Canada]  
            ,[Geography].[Geography].[Country].[United States]  
            ,[Geography].[Geography].[State-Province].[Alberta]  
            ,[Geography].[Geography].[State-Province].[Brunswick]  
            ,[Geography].[Geography].[State-Province].[Colorado]   
            }  
         ), {[Geography].[Geography].[Country].[United States]}  
   )  
ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會從「**艾德公司**」 `Measures.[Order Quantity]` cube 傳回成員的總和（在`Date`維度中包含的前9個月2003匯總）。 **PeriodsToDate**函數會在集合中定義彙總函式操作所在的元組。 **Hierarchize**函數會以階層順序組織產品維度中指定成員集合的成員。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS Count  
   (Filter  
      (Existing  
         (Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] <   
               ([Measures].[Reseller Sales Amount],[Date].Calendar.PrevMember)  
        )  
    )  
MEMBER [Geography].[State-Province].x AS Aggregate   
( {[Geography].[State-Province].&[WA]&[US],   
   [Geography].[State-Province].&[OR]&[US] }   
)  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})}  
        )  
    ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
   [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
