---
title: 存在 (MDX) |Microsoft 文件
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7237a4023bf9ad67f0050951b60b1ee33db4a53f
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740607"
---
# <a name="exists-mdx"></a>Exists (MDX)


  傳回屬於第一個指定集合並且與第二個指定集合中一或多個 Tuple 同時存在的 Tuple 集合。 這個函數會手動執行自動存在功能自動執行的動作。 如需有關自動存在，請參閱 < [MDX 的關鍵概念&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)。  
  
 如果選擇性\<量值群組名稱 > 所提供函式傳回一個或多個 tuple 存在的 tuple 從第二個集合，以及具有相關聯的事實資料表中指定的量值群組的資料列的 tuple。  
  
## <a name="syntax"></a>語法  
  
```  
  
Exists( Set_Expression1 , Set_Expression2 [, MeasureGroupName] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression1*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Set_Expression2*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *MeasureGroupName*  
 指定量值群組名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
  
1.  含有 null 值的量值與量值群組資料列會構成**Exists**指定 MeasureGroupName 引數時。 這個形式的 Exists 和 Nonempty 函數之間的差異如下：如果這些量值的 NullProcessing 屬性設為 Preserve，這表示在對 Cube 的該部分執行查詢時，量值會顯示 Null 值；NonEmpty 永遠會從有 Null 量值的集合中移除 Tuple，而具有 MeasureGroupName 引數的 Exists 則不會篩選有相關量值群組資料列的 Tuple，即使量值為 Null 也一樣。  
  
2.  如果*MeasureGroupName*參數，則結果將會相依於參考的量值群組中是否有可見的量值; 如果參考的量值群組中不有任何可見的量值，則 EXISTS 一定會傳回空集合，不論值*Set_Expression1*和*Set_Expression2*。  
  
## <a name="examples"></a>範例  
 住在加州的客戶：  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
) ON 1   
FROM [Adventure Works]  
  
```  
  
 住在加州並且有銷售額的客戶：  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 有銷售額的客戶：  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, , "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 購買自行車的客戶：  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Product].[Product Categories].[Category].&[1]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [交叉聯結&#40;MDX&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [NonEmpty &#40;MDX&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
  
