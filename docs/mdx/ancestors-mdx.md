---
title: "上階 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ANCESTORS
dev_langs: kbMDX
helpviewer_keywords: Ancestors function
ms.assetid: abdf2e9c-72c8-4f2e-a823-d42efc4cc7d5
caps.latest.revision: "46"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1258a09acc7c2459742f5670a3ab0bd1a770cafe
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="ancestors-mdx"></a>Ancestors (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  會傳回指定層級上指定之成員的所有上階集合或離該成員指定距離之所有上階集合的函數。 與[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，傳回集將會永遠包含單一成員-[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]不支援多個父代的單一成員。  
  
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
 與**祖系**函式，您提供 MDX 成員運算式給函數，，然後提供一個層級，該成員的上階的 MDX 運算式或代表該成員上面的層級數目的數值運算式。 利用此資訊，**祖系**函式會傳回該層級之成員 （這會是一個成員所組成的一組） 的集合。  
  
> [!NOTE]  
>  要傳回上階成員，而非上階集合，使用[祖系](../mdx/ancestor-mdx.md)函式。  
  
 如果指定層級運算式，則**祖系**函數會傳回指定層級指定的成員所有上階的集合。 如果指定成員不是位在指定層級的相同階層中，函數會傳回錯誤。  
  
 如果指定距離，**祖系**函數會傳回由成員運算式所指定的階層中的步驟數目的所有成員的集合。 成員可以指定為屬性階層或使用者自訂階層的成員，或在某些狀況下指定為父子式階層的成員。 數字 1 會傳回位於父層級的成員集合，而且數字 2 會傳回位於祖系層級的成員集合 (如果存在的話)。 數字 0 會傳回只含成員本身的集合。  
  
> [!NOTE]  
>  使用這種形式**祖系**函式的情況下的父層級未知或無法命名。  
  
## <a name="examples"></a>範例  
 下列範例會使用**祖系**函式來傳回成員、 其父系及祖 Internet Sales Amount 量值。 這個範例使用層級運算式指定要傳回的層級。 這些層級是在成員運算式中所指定之成員的相同階層中。  
  
```  
SELECT {  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Category]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Subcategory]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Product])  
    } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 下列範例會使用**祖系**函式來傳回成員、 其父系及祖 Internet Sales Amount 量值。 這個範例使用數值運算式指定所傳回的層級。 這些層級是在成員運算式中所指定之成員的相同階層中。  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
