---
description: Rank (MDX)
title: 順位 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 391ba9d805684a9fd469d8e6c66727caba71ce70
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341334"
---
# <a name="rank-mdx"></a>Rank (MDX)


  傳回指定集合中、指定 Tuple 的以一為基底次序。  
  
## <a name="syntax"></a>語法  
  
```  
  
Rank(Tuple_Expression, Set_Expression [ ,Numeric Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Tuple_Expression*  
 傳回 Tuple 的有效多維度運算式 (MDX) 運算式。  
  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果指定了數值運算式，則 **Rank** 函數會針對元組評估指定的數值運算式，以判斷指定之元組的單一次序。 如果指定了數值運算式， **rank** 函數會將相同的 rank 指派給集合中具有重複值的元組。 指派相同的順序給重複值，會影響集合中後續 Tuple 的順序。 例如，有個集合由以下 Tuple 構成：`{(a,b), (e,f), (c,d)}`。 Tuple `(a,b)` 和 Tuple `(c,d)` 擁有相同的值。 如果 Tuple `(a,b)` 的次序為 1，則 `(a,b)` 和 `(c,d)` 的次序都會是 1。 不過，Tuple `(e,f)` 的次序會是 3。 這個集合中可能不會有次序 2 的 Tuple。  
  
 如果未指定數值運算式， **Rank** 函數會傳回指定之元組的以一個為基底的序數位置。  
  
 **Rank**函數不會排序集合。  
  
## <a name="example"></a>範例  
 下列範例會傳回包含客戶和購買日期的元組**集合，方法**是使用**Filter**、非空白、 **Item**和**Rank**函數來尋找每個客戶購買的最後一個日期。  
  
```  
WITH SET MYROWS AS FILTER  
   (NONEMPTY  
      ([Customer].[Customer Geography].MEMBERS  
         * [Date].[Date].[Date].MEMBERS  
         , [Measures].[Internet Sales Amount]  
      ) AS MYSET  
   , NOT(MYSET.CURRENT.ITEM(0)  
      IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))  
   )  
SELECT [Measures].[Internet Sales Amount] ON 0,  
MYROWS ON 1  
FROM [Adventure Works]  
```  
  
 下列範例會使用 **Order** 函數（而非 **Rank** 函數），根據「轉售商銷售金額」量值為 City 階層的成員進行排名，然後以排名順序顯示這些成員。 藉由使用 **Order** 函數來先排序 City 階層的成員集合，排序只會完成一次，然後再以線性掃描的形式呈現排序的順序。  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [順序 &#40;MDX&#41;](../mdx/order-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
