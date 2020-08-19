---
description: Hierarchize (MDX)
title: Hierarchize (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3c1683819420d150e2f9b330ba94bc9e228d167f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429910"
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
 **Hierarchize**函式會將指定之集合的成員組織成階層式順序。 此函數永遠會保留重複項。  
  
-   如果未指定 **POST** ，此函式會依自然順序來排序層級中的成員。 未指定其他排序條件時，它們的自然順序就是階層中成員的預設順序。 子成員會直接跟隨在父成員後面。  
  
-   如果指定 **post** ， **Hierarchize** 函式會使用後置順序來排序層級中的成員。 換言之，子成員會在其父系之前。  
  
## <a name="example"></a>範例  
 下列範例會在 Canada 成員向上鑽研。 **Hierarchize**函數是用來依階層式順序組織指定的集合成員，這是**DrillUpMember**函數所需的成員。  
  
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
  
 下列範例會傳回成員的總和，此成員是在 `Measures.[Order Quantity]` 維度所包含之2003的前九個月 `Date` （來自「 **艾德作品** 」 cube）所匯總。 **PeriodsToDate**函式會在集合中定義彙總函式運作的元組。 **Hierarchize**函式會依階層式順序，組織產品維度中指定之成員集合的成員。  
  
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
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
