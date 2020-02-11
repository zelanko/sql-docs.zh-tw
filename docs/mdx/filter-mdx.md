---
title: Filter （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3a70bceed4cdccf6a22f0cfea4e5093634f88f1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132685"
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
 **Filter**函數會針對指定集合中的每個元組，評估指定的邏輯運算式。 函式會傳回集合，其中包含指定集合中的每個元組，其中邏輯運算式評估為**true**。 如果沒有元組評估為**true**，則會傳回空的集合。  
  
 **Filter**函式的運作方式類似于[IIf](../mdx/iif-mdx.md)函式的功能。 **IIf**函數只會根據 MDX 邏輯運算式的評估，傳回兩個選項的其中一個，而**Filter**函數會傳回一組符合指定搜尋條件的元組。 實際上， **Filter**函數會在集合`IIf(Logical_Expression, Set_Expression.Current, NULL)`中的每個元組上執行，並傳回結果集。  
  
## <a name="examples"></a>範例  
 下列範例示範如何在查詢的資料列軸上使用 Filter 函數，以便只傳回 Internet Sales Amount 大於 $10000 的日期：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 Filter 函數也可以在導出成員定義內使用。 下列範例會從「**艾德公司**」 `Measures.[Order Quantity]` cube 傳回成員的總和（在`Date`維度中包含的前9個月2003匯總）。 **PeriodsToDate**函數會在集合中定義**聚合**函數操作所在的元組。 **篩選**函數會將傳回的元組限制為較低的值，以符合上一個時間週期的「轉售商銷售量」量值。  
  
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
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
