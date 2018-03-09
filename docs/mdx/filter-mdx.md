---
title: "篩選器 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: filter
dev_langs: kbMDX
helpviewer_keywords: Filter function
ms.assetid: f2df51c8-6acb-4300-b71c-2a480c9fbdf8
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 729adc2230242798e67914907b6928ec7346b871
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="filter-mdx"></a>Filter (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 **篩選**函式會評估指定的邏輯運算式，對每個 tuple 中指定的集合。 此函數會傳回邏輯運算式評估為指定集合中的每個 tuple 所組成的一組**true**。 如果沒有 tuple 評估為**true**，會傳回空集合。  
  
 **篩選**函式運作方式類似於[IIf](../mdx/iif-mdx.md)函式。 **IIf**函式會傳回兩個選項的其中之一依據 MDX 邏輯運算式的評估結果，而**篩選**函式會傳回符合指定的搜尋條件的 tuple 集合。 實際上，**篩選**函式會執行`IIf(Logical_Expression, Set_Expression.Current, NULL)`上每個 tuple 集合，並傳回結果集。  
  
## <a name="examples"></a>範例  
 下列範例示範如何在查詢的資料列軸上使用 Filter 函數，以便只傳回 Internet Sales Amount 大於 $10000 的日期：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 Filter 函數也可以在導出成員定義內使用。 下列範例會傳回的 sum`Measures.[Order Quantity]`成員進行彙總前 9 個月中含括之 2003年`Date`維度中，從**Adventure Works** cube。 **PeriodsToDate**函式的集合中定義 tuple**彙總**函式運作。 **篩選**函式限制為具有較低的值 Reseller Sales Amount 量值傳回的上一個時間週期的 tuple。  
  
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
  
## <a name="see-also"></a>請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
