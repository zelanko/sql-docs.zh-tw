---
title: 子代（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2a981595c19c321ab498fe9eb65b8570eb17f3ee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67999983"
---
# <a name="descendants-mdx"></a>Descendants (MDX)


  傳回特定層集或距離的成員之子系集合，選擇性包括或排除其他層級中的子系。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member expression syntax using a level expression  
Descendants(Member_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Member_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
Set expression syntax using a level expression  
Descendants(Set_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Set_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
 *Distance*  
 有效的數值運算式，會指定與指定成員間的距離。  
  
 *Desc_Flag*  
 指定描述旗標的有效字串運算式，以區分可能的下階集合。  
  
## <a name="remarks"></a>備註  
 如果指定了層級，下**階函數會**傳回一個集合，其中包含指定之成員的下階，或指定之集合的成員（選擇性地由*Desc_Flag*中指定的旗標修改）。  
  
 如果指定了*距離*，下**階函數會**傳回一個集合，其中包含指定之成員的下階，或指定之集合的成員，而這些層級是指定成員之階層中的指定數目，並可選擇性地由*Desc_Flag*中指定的旗標加以修改。 一般說來，您可以使用這個函數搭配 Distance 引數，來處理不完全階層。 如果指定的距離是零 (0)，此函數會傳回只由指定成員或指定集合所組成的集合。  
  
 如果指定了集合運算式 **，則會**針對集合的每個成員個別解析子系函式，然後再次建立集合。 換句話說，用於**子代**函式的語法在功能上相當於 MDX[產生](../mdx/generate-mdx.md)函式。  
  
 如果沒有指定層級或距離，函數所使用之層級的預設值是藉由呼叫[level](../mdx/level-mdx.md)函數（<\<成員>> 來決定。層級）：指定的成員（如果已指定成員），或針對指定集合的每個成員呼叫**level**函數（如果已指定集合）。 如果沒有指定層級運算式、距離或旗標，函數執行方式就如同使用下列語法一樣：  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Member_Expression.Level ,`  
  
 `SELF_BEFORE_AFTER`  
  
 `)`  
  
 如果指定了層級運算式，而且沒有指定描述旗標，函數執行方式就如同使用下列語法一樣。  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Level_Expression,`  
  
 `SELF`  
  
 `)`  
  
 無論指定的層級或距離為何，您都可以藉由變更描述旗標的值，包含或排除已指定之層級或距離的下階、已指定之層級或距離前後 (直到分葉節點) 的子系，以及所有分葉子系。 下表描述*Desc_Flag*引數中允許的旗標。  
  
|旗標|描述|  
|----------|-----------------|  
|SELF|只傳回指定層級或指定距離的下階成員。 如果指定的層級是指定成員的層級，此函數會包含指定成員。|  
|AFTER|傳回從屬於指定層級或距離之所有層級的下階成員。|  
|BEFORE|傳回指定成員和指定層級 (或指定距離) 間所有層級的下階成員。 包含指定成員，但不包含來自指定層級或距離的成員。|  
|BEFORE_AND_AFTER|傳回從屬於指定成員層級之所有層級的下階成員。 包含指定成員，但不包含來自指定層級或指定距離的成員。|  
|SELF_AND_AFTER|傳回來自指定層級或指定距離的下階成員，以及從屬於指定層級或指定距離之所有層級的下階成員。|  
|SELF_AND_BEFORE|傳回來自指定層級或指定距離的下階成員，以及介於指定成員和指定層級 (或指定距離) 之間所有層級的下階成員，包括指定的成員。|  
|SELF_BEFORE_AFTER|傳回從屬於指定成員層級之所有層級的下階成員，並且包含指定的成員。|  
|LEAVES|傳回介於指定成員和指定層級 (或指定距離) 之間的分葉下階成員。|  
  
## <a name="examples"></a>範例  
 下列範例會傳回指定的成員 (United States)，以及介於該指定成員 (United States) 和指定層級 (City) 上一個層級成員之間的成員。範例會傳回指定成員本身 (United States)，以及 State-Province 層級 (City 層級的上一個層級) 的成員。 這個範例包含標記為註解的引數，讓您能輕鬆測試這個函數的其他引數。  
  
```  
SELECT Descendants  
   ([Geography].[Geography].[Country].&[United States]  
      //, [Geography].[Geography].[Country]  
   , [Geography].[Geography].[City]  
      //, [Geography].[Geography].Levels (3)  
      //, SELF   
      //, AFTER  
      , BEFORE  
      // BEFORE_AND_AFTER  
      //, SELF_AND_AFTER  
      //, SELF_AND_BEFORE  
      //,SELF_BEFORE_AFTER  
      //,LEAVES   
   ) ON 0  
FROM [Adventure Works]   
```  
  
 下列範例會傳回`Measures.[Gross Profit Margin]`量值的每日平均值，計算方式是從「**艾德公司**」 cube 中，在2003會計年度每個月的每個月的天數內。 下**階函數會**傳回從階層的目前成員`[Date].[Fiscal]`決定的一組天數。  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS Avg  
   (  
      Descendants( [Date].[Fiscal].CurrentMember,   
           [Date].[Fiscal].[Date]  
          ),   
        Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
   [Date].[Fiscal].[Month].Members ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Fiscal Year].&[2003])  
```  
  
 下列範例使用層級運算式，並且會傳回 Australia 每個 State-Province 的 Internet Sales Amount，及傳回每個 State-Province 佔 Australia 之 Internet Sales Amount 總計的百分比。 這個範例使用 Item 函數，從**祖**系函式所傳回的集合中，將第一個（且唯一的）元組解壓縮。  
  
```  
WITH MEMBER Measures.x AS   
   [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],  
      Ancestors   
         ( [Customer].[Customer Geography].CurrentMember,   
           [Customer].[Customer Geography].[Country]  
         ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],   
     [Customer].[Customer Geography].[State-Province], SELF   
   )    
} ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
