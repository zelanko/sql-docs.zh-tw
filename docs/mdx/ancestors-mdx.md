---
description: Ancestors (MDX)
title: " (MDX) 的祖系 |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d92f15f20c872fbe63db09a55356b5d1e35ff0d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461680"
---
# <a name="ancestors-mdx"></a>Ancestors (MDX)


  會傳回指定層級上指定之成員的所有上階集合或離該成員指定距離之所有上階集合的函數。 使用時 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，傳回的集合一律由單一成員所組成-不 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支援單一成員有多個父系。  
  
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
 使用 **祖** 系函式時，您會提供具有 MDX 成員運算式的函式，然後提供層級的 mdx 運算式，該成員是該成員的上階，或代表該成員上方層級數目的數值運算式。 利用這項資訊， **祖** 系函數會傳回一組成員 (這組成員是由該層級的一個成員) 組成。  
  
> [!NOTE]  
>  若要傳回上階成員，而不是上階集合，請使用 [祖系](../mdx/ancestor-mdx.md) 函數。  
  
 如果指定了層級運算式， **祖** 系函數會傳回指定層級之指定成員的所有上階集。 如果指定成員不是位在指定層級的相同階層中，函數會傳回錯誤。  
  
 如果指定距離， **祖** 系函數會傳回成員運算式所指定之階層中所指定之步驟數目的所有成員集合。 成員可以指定為屬性階層或使用者自訂階層的成員，或在某些狀況下指定為父子式階層的成員。 數字 1 會傳回位於父層級的成員集合，而且數字 2 會傳回位於祖系層級的成員集合 (如果存在的話)。 數字 0 會傳回只含成員本身的集合。  
  
> [!NOTE]  
>  在父代的層級未知或無法命名的情況下，請使用這種形式的 **祖** 系函數。  
  
## <a name="examples"></a>範例  
 下列範例會使用 **祖** 系函數來傳回成員、其父系和祖系的網際網路銷售量量值。 這個範例使用層級運算式指定要傳回的層級。 這些層級是在成員運算式中所指定之成員的相同階層中。  
  
```  
SELECT {  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Category]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Subcategory]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Product])  
    } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 下列範例會使用 **祖** 系函數來傳回成員、其父系和祖系的網際網路銷售量量值。 這個範例使用數值運算式指定所傳回的層級。 這些層級是在成員運算式中所指定之成員的相同階層中。  
  
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
  
 下列範例會使用 **祖** 系函數來傳回屬性階層之成員父系的網際網路銷售量量值。 這個範例使用數值運算式指定所傳回的層級。 因為成員運算式中的成員是屬性階層的成員，所以它的父系是 [All] 層級。  
  
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
  
  
