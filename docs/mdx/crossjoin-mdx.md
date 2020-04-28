---
title: 交叉聯結（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 63de71ae82e60b8ec7d8a39e18f89e6bd2393f2d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68892940"
---
# <a name="crossjoin-mdx"></a>Crossjoin (MDX)


  傳回兩個集合的交叉乘積。  
  
## <a name="syntax"></a>語法  
  
```  
  
Standard syntax  
Crossjoin(Set_Expression1 ,Set_Expression2 [,...n] )  
  
Alternate syntax  
Set_Expression1 * Set_Expression2 [* ...n]  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression1*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Set_Expression2*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **交叉**聯結函數會傳回兩個或多個指定集合的交叉乘積。 Tuple 在結果集中的順序，會依據要聯結的集合順序以及它們成員的順序而定。 例如，當第一個集合由 {x1，x2,..., x*n*} 組成，而第二個集合由 {y1，y2，...，y*n*} 組成時，這些集合的交叉乘積就是：  
  
 {（x1，y1），（x1，y2）,..., （x1，y*n*），（x2，y1），（x2，y2）,..。,  
  
 （x2，y*n*）,..., （x*n*，y1），（x*n*，y2）,..., （xn，y*n*）}  
  
> [!IMPORTANT]  
>  如果交叉聯結中的集合是由相同維度之不同屬性階層的 Tuple 組成，這個函數只會傳回實際存在的 Tuple。 如需詳細資訊，請參閱[MDX 中的重要概念 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)。  
  
## <a name="examples"></a>範例  
 下列查詢會示範在查詢的資料行軸和資料列軸上使用 Crossjoin 函數的範例：  
  
 `SELECT`  
  
 `[Customer].[Country].Members *`  
  
 `[Customer].[State-Province].Members`  
  
 `ON 0,`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].Members,`  
  
 `[Product].[Category].[Category].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE Measures.[Internet Sales Amount]`  
  
 下列範例示範當相同維度中的不同階層交叉聯結時，所發生的自動篩選：  
  
 `SELECT`  
  
 `Measures.[Internet Sales Amount]`  
  
 `ON 0,`  
  
 `//Only the dates in Calendar Years 2003 and 2004 will be returned here`  
  
 `Crossjoin(`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]},`  
  
 `[Date].[Date].[Date].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 下列三個範例都會傳回相同的結果 - 美國各州的 Internet Sales Amount。 前兩個範例使用兩個交叉聯結語法，第三個示範 WHERE 子句用法，以傳回相同資訊。  
  
### <a name="example-1"></a>範例 1  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
       [Customer].[State-Province].Members  
   ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-2"></a>範例 2  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-3"></a>範例 3  
  
```  
SELECT   
   [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
