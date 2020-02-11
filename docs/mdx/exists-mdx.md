---
title: Exists （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ba2cef1cfb95319cbe0aff827cb251ff7e2317c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68893615"
---
# <a name="exists-mdx"></a>Exists (MDX)


  傳回屬於第一個指定集合並且與第二個指定集合中一或多個 Tuple 同時存在的 Tuple 集合。 這個函數會手動執行自動存在功能自動執行的動作。 如需自動存在的詳細資訊，請參閱[MDX 中的重要概念 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)。  
  
 如果提供了\<選擇性量值組名>，此函數會傳回與第二個集合中的一個或多個元組存在的元組，以及在指定之量值群組的事實資料表中具有相關聯資料列的元組。  
  
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
  
1.  當指定 MeasureGroupName 引數時，包含 null 值之量值的量值群組資料列有助於**存在**。 這是這種形式的 Exists 和非空白函數之間的差異：如果這些量值的 NullProcessing 屬性設定為 [保留]，這表示當對 cube 的該部分執行查詢時，量值將會顯示 Null 值;非空白會一律從具有 Null 量值的集合中移除元組，而 Exists 與 MeasureGroupName 引數則不會篩選具有相關聯量值群組資料列的元組，即使量值是 Null 也一樣。  
  
2.  如果使用*MeasureGroupName*參數，則結果會取決於參考的量值群組中是否有可見量值;如果參考的量值群組中沒有可見的量值，則不論*Set_Expression1*和*Set_Expression2*的值為何，EXISTS 一律會傳回空的集合。  
  
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
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX&#41;的交叉聯結 &#40;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [非空的 &#40;MDX&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
  
