---
title: 存在 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9b53932676cae30e4b1111c785a6a78c992a3685
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62690863"
---
# <a name="exists-mdx"></a>Exists (MDX)


  傳回屬於第一個指定集合並且與第二個指定集合中一或多個 Tuple 同時存在的 Tuple 集合。 這個函數會手動執行自動存在功能自動執行的動作。 如需有關自動存在，請參閱 < [MDX 的關鍵概念&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)。  
  
 如果選擇性\<量值群組名稱 > 所提供的函式會傳回一或多個 tuple 存在的 tuple 與第二個集合具有相關聯的事實資料表中指定的量值群組的資料列的 tuple。  
  
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
  
1.  量值包含 null 值的量值群組資料列變為**Exists** MeasureGroupName 引數指定時。 這是這種形式的 Exists 和 Nonempty 函數之間的差異： 如果這些量值的 NullProcessing 屬性設為 Preserve，這表示對 cube; 該部分執行查詢時，量值會顯示 Null 值而具有 MeasureGroupName 引數的 Exists 不會篩選有相關聯的量值群組資料列的 tuple，即使量值是 Null，則 nonEmpty 永遠會從有 Null 量值的值，一組移除 tuple。  
  
2.  如果*MeasureGroupName*參數，結果取決於參考的量值群組中是否有可見的量值; 如果參考的量值群組中沒有任何可見的量值，則 EXISTS 一定會傳回空的集合，不論值*Set_Expression1*並*Set_Expression2*。  
  
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
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Crossjoin &#40;MDX&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [NonEmpty &#40;MDX&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
  
