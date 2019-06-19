---
title: Filter (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d740148052712a69a39e0de314496733b3b26a8b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63154636"
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
 **篩選**函式會評估指定的邏輯運算式，對指定集合中每個 tuple。 此函數會傳回一組所組成的邏輯運算式評估為指定集合中的每個 tuple **，則為 true**。 如果沒有 tuple 評估為 **，則為 true**，會傳回空集合。  
  
 **篩選條件**函式的工作方式類似於[IIf](../mdx/iif-mdx.md)函式。 **IIf**函式會傳回兩個選項的其中之一為基礎的 MDX 邏輯運算式評估，而**篩選**函式會傳回符合指定的搜尋條件的 tuple 集合。 實際上**篩選條件**函式會執行`IIf(Logical_Expression, Set_Expression.Current, NULL)`上每個 tuple 集合，並傳回結果集。  
  
## <a name="examples"></a>範例  
 下列範例示範如何在查詢的資料列軸上使用 Filter 函數，以便只傳回 Internet Sales Amount 大於 $10000 的日期：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 Filter 函數也可以在導出成員定義內使用。 下列範例會傳回的總和`Measures.[Order Quantity]`成員，在中含括之 2003 年的第九個月彙總`Date`維度中，從**Adventure Works** cube。 **PeriodsToDate**函式的集合中定義 tuple**彙總**函式運作。 **篩選**函式會限制為上一個時間週期為具有較低的值 Reseller Sales Amount 量值所傳回的 tuple。  
  
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
  
  
