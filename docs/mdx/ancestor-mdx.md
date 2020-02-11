---
title: 祖系（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 385206d4a94362831e0949bafe5a11c1ce48d7bd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68017135"
---
# <a name="ancestor-mdx"></a>Ancestor (MDX)


  會傳回指定層級上指定之成員的上階或離該成員指定距離之上階的函數。  
  
## <a name="syntax"></a>語法  
  
```  
  
Level syntax  
Ancestor(Member_Expression, Level_Expression)  
  
Numeric syntax  
Ancestor(Member_Expression, Distance)  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
 *長途電話*  
 有效的數值運算式，會指定與指定成員間的距離。  
  
## <a name="remarks"></a>備註  
 使用**祖系**函式，您可以提供 mdx 成員運算式給函數，然後提供屬於成員上階之層級的 MDX 運算式，或代表該成員上方層級數目的數值運算式。 使用此資訊時，**祖**系函式會傳回該層級的上階成員。  
  
> [!NOTE]  
>  若要傳回包含祖系成員的集合，而不只是上階成員，請使用[&#40;MDX&#41;](../mdx/ancestors-mdx.md)函數的上階。  
  
 如果指定了層級運算式，**祖系**函式會在指定的層級傳回指定成員的上階。 如果指定成員不是位在指定層級的相同階層中，函數會傳回錯誤。  
  
 如果指定距離，**祖系**函式會傳回指定成員的上階，也就是成員運算式所指定之階層中所指定的步驟數目。 成員可以指定為屬性階層或使用者自訂階層的成員，或在某些狀況下指定為父子式階層的成員。 數字 1 會傳回成員的父系，數字 2 會傳回成員的祖系 (如果存在的話)。 數字 0 會傳回成員本身。  
  
> [!NOTE]  
>  若父系的層級不明或無法命名，請使用這種形式的**祖系**函式。  
  
## <a name="examples"></a>範例  
 下列範例使用層級運算式，並且會傳回 Australia 每個 State-Province 的 Internet Sales Amount，及其佔 Australia 之 Internet Sales Amount 總計的百分比。  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
   [Measures].[Internet Sales Amount],    
      Ancestor   
         (  
         [Customer].[Customer Geography].CurrentMember,  
            [Customer].[Customer Geography].[Country]  
         )  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
        [Customer].[Customer Geography].[Country].&[Australia],  
           [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
 下列範例使用數值運算式，並且會傳回 Australia 每個 State-Province 的 Internet Sales Amount，及其佔所有國家 (地區) Internet Sales Amount 總計的百分比。  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
      [Measures].[Internet Sales Amount],  
         Ancestor   
            ([Customer].[Customer Geography].CurrentMember, 2)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
         [Customer].[Customer Geography].[Country].&[Australia],  
            [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
