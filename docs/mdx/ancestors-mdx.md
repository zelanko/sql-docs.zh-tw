---
title: 上階 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0c108ea102e03000481d18bfc69f657e6bd8a0ce
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313729"
---
# <a name="ancestors-mdx"></a>Ancestors (MDX)


  會傳回指定層級上指定之成員的所有上階集合或離該成員指定距離之所有上階集合的函數。 具有[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，傳回集一律會包含單一成員-[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]不支援的單一成員有多個父代。  
  
## <a name="syntax"></a>語法  
  
```  
  
Level syntax  
Ancestors(Member_Expression, Level_Expression)  
  
Numeric syntax  
Ancestors(Member_Expression, Distance)  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
 *距離*  
 有效的數值運算式，會指定與指定成員間的距離。  
  
## <a name="remarks"></a>備註  
 具有**祖系**函式，您提供 MDX 成員運算式給函數，然後提供一個層級，該成員之上階的 MDX 運算式或數值運算式，表示層級數目該成員的上方。 使用此資訊，請**祖系**函式會傳回該層級的成員 （這會是一個成員所組成的一組） 的集合。  
  
> [!NOTE]  
>  若要傳回上階成員，而非上階集合，使用[祖系](../mdx/ancestor-mdx.md)函式。  
  
 如果指定層級運算式，則**祖系**函數會傳回指定層級指定的成員所有上階的集合。 如果指定成員不是位在指定層級的相同階層中，函數會傳回錯誤。  
  
 如果指定距離，就**祖系**函數會傳回集合的所有成員之上方層級成員運算式所指定的階層中的步驟數目。 成員可以指定為屬性階層或使用者自訂階層的成員，或在某些狀況下指定為父子式階層的成員。 數字 1 會傳回位於父層級的成員集合，而且數字 2 會傳回位於祖系層級的成員集合 (如果存在的話)。 數字 0 會傳回只含成員本身的集合。  
  
> [!NOTE]  
>  使用這種形式**祖系**函式的情況下的父層級未知或無法命名。  
  
## <a name="examples"></a>範例  
 下列範例會使用**祖系**函數來傳回成員、 其父系及祖系的 Internet Sales Amount 量值。 這個範例使用層級運算式指定要傳回的層級。 這些層級是在成員運算式中所指定之成員的相同階層中。  
  
```  
SELECT {  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Category]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Subcategory]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Product])  
    } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 下列範例會使用**祖系**函數來傳回成員、 其父系及祖系的 Internet Sales Amount 量值。 這個範例使用數值運算式指定所傳回的層級。 這些層級是在成員運算式中所指定之成員的相同階層中。  
  
```  
SELECT {  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],2  
      ),  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],1  
      ),  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],0  
      )  
   } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM  [Adventure Works]  
```  
  
 下列範例會使用**祖系**函式來傳回屬性階層的成員之父系的 Internet Sales Amount 量值。 這個範例使用數值運算式指定所傳回的層級。 因為成員運算式中的成員是屬性階層的成員，所以它的父系是 [All] 層級。  
  
```  
SELECT {  
   Ancestors(  
      [Product].[Product].[Mountain-100 Silver, 38],1  
      )  
   } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
