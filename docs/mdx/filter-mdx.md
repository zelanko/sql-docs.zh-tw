---
description: Filter (MDX)
title: 篩選 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 026e4720803d828ae9ba96a4d3df7f5a72d59e8d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387504"
---
# <a name="filter-mdx"></a>Filter (MDX)


  傳回根據搜尋條件篩選指定集合後所得的集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Filter(Set_Expression, Logical_Expression )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Logical_Expression*  
 評估為 true 或 false 的有效多維度運算式 (MDX) 邏輯運算式。  
  
## <a name="remarks"></a>備註  
 **篩選**函數會針對指定之集合中的每個元組，評估指定的邏輯運算式。 函數會傳回一個集合，其中包含指定之集合中的每個元組，其中邏輯運算式評估為 **true**。 如果沒有任何元組評估為 **true**，則會傳回空集合。  
  
 **篩選**函數的運作方式類似于[IIf](../mdx/iif-mdx.md)函式的方式。 **IIf**函數只會根據 MDX 邏輯運算式的評估傳回兩個選項的其中一個，而**Filter**函數會傳回一組符合指定搜尋條件的元組。 實際上， **Filter** 函數會 `IIf(Logical_Expression, Set_Expression.Current, NULL)` 在集合中的每個元組上執行，並傳回結果集。  
  
## <a name="examples"></a>範例  
 下列範例示範如何在查詢的資料列軸上使用 Filter 函數，以便只傳回 Internet Sales Amount 大於 $10000 的日期：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 Filter 函數也可以在導出成員定義內使用。 下列範例會傳回成員的總和，此成員是在 `Measures.[Order Quantity]` 維度所包含之2003的前九個月 `Date` （來自「 **艾德作品** 」 cube）所匯總。 **PeriodsToDate**函式會在集合中定義**聚合**函數運作的元組。 **篩選**函式會將傳回的元組限制為具有較低值的元組，以作為前一個時間週期的「轉售商銷售量」量值。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS Count  
   (Filter  
      (Existing  
         (Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] <   
               ([Measures].[Reseller Sales Amount],[Date].Calendar.PrevMember)  
        )  
    )  
MEMBER [Geography].[State-Province].x AS Aggregate   
( {[Geography].[State-Province].&[WA]&[US],   
   [Geography].[State-Province].&[OR]&[US] }   
)  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})}  
        )  
    ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
   [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
