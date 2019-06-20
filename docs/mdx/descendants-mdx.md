---
title: 下階 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 013b7a7a2124788f3f1bcaa6d09b8ef7b10562e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248111"
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
  
 *距離*  
 有效的數值運算式，會指定與指定成員間的距離。  
  
 *Desc_Flag*  
 指定描述旗標的有效字串運算式，以區分可能的下階集合。  
  
## <a name="remarks"></a>備註  
 如果指定層級，則**子代**函式會傳回一個集合，包含指定的成員或指定的集合，在指定的層級，選擇性地在指定的旗標加以修改成員的下階*Desc_Flag*。  
  
 如果*距離*指定，則**子代**函式會傳回包含指定的成員或離開層級中指定的數目指定的集合成員的下階的集合指定的成員，選擇性地在指定的旗標加以修改階層*Desc_Flag*。 一般說來，您可以使用這個函數搭配 Distance 引數，來處理不完全階層。 如果指定的距離是零 (0)，此函數會傳回只由指定成員或指定集合所組成的集合。  
  
 如果指定了集合運算式，則**子系**函式是個別解析集中，每個成員且重新建立集合。 換句話說，所使用的語法**子代**函式相當於 MDX[產生](../mdx/generate-mdx.md)函式。  
  
 如果指定任何層級或距離，函式所用的層級的預設值取決於呼叫[層級](../mdx/level-mdx.md)函式 (<\<成員 >>。層級） 指定的成員 （如果已指定成員），或藉由呼叫**層級**（如果已指定一組），指定集合的每個成員函式。 如果沒有指定層級運算式、距離或旗標，函數執行方式就如同使用下列語法一樣：  
  
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
  
 無論指定的層級或距離為何，您都可以藉由變更描述旗標的值，包含或排除已指定之層級或距離的下階、已指定之層級或距離前後 (直到分葉節點) 的子系，以及所有分葉子系。 下表描述中允許的旗標*Desc_Flag*引數。  
  
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
  
 下列範例會傳回每日平均`Measures.[Gross Profit Margin]`量值，計算出的 2003年會計年度，每個月的天數**Adventure Works** cube。 **子代**函式會傳回一組天次從目前的成員來決定`[Date].[Fiscal]`階層。  
  
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
  
 下列範例使用層級運算式，並且會傳回 Australia 每個 State-Province 的 Internet Sales Amount，及傳回每個 State-Province 佔 Australia 之 Internet Sales Amount 總計的百分比。 此範例使用 Item 函數來擷取所傳回的集合中的第一個 （且唯一） tuple**祖系**函式。  
  
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
  
  
