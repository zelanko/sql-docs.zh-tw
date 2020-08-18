---
description: CurrentOrdinal (MDX)
title: CurrentOrdinal (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 68119266fd9460a28e036914fce036ec165e553a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413154"
---
# <a name="currentordinal-mdx"></a>CurrentOrdinal (MDX)


  反覆運算時傳回集合中目前的反覆運算編號。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set_Expression.CurrentOrdinal  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 逐一查看集合時，例如 [ (mdx) 的篩選準則 ](../mdx/filter-mdx.md) ，或 [產生 (mdx) ](../mdx/generate-mdx.md) 函數時， **CurrentOrdinal** 函式會傳回反復專案數目。  
  
## <a name="examples"></a>範例  
 下列簡單的範例示範如何搭配使用 **CurrentOrdinal** 與 [ **產生** ]，以傳回字串，其中包含集合中每個專案的名稱以及其在集合中的位置：  
  
 `WITH SET MySet AS [Customer].[Customer Geography].[Country].MEMBERS`  
  
 `MEMBER MEASURES.CURRENTORDINALDEMO AS`  
  
 `GENERATE(MySet, CSTR(MySet.CURRENTORDINAL) + ") " + MySet.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTORDINALDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
 CurrentOrdinal 的實際使用限制為非常複雜的計算。 下列範例會使用 **order** 函數來排序非空白的元組，然後再利用 **Filter** 函數，傳回集合中唯一的產品數目。 **CurrentOrdinal**函數是用來比較和消除系結。  
  
```  
WITH MEMBER [Measures].[PrdTies] AS Count  
   (Filter  
      (Order  
        (NonEmpty  
          ([Product].[Product].[Product].Members  
          , {[Measures].[Reseller Order Quantity]}  
          )  
       , [Measures].[Reseller Order Quantity]  
       , BDESC  
       ) AS OrdPrds  
    , NOT((OrdPrds.CurrentOrdinal < OrdPrds.Count   
       AND [Measures].[Reseller Order Quantity] =   
          ( [Measures].[Reseller Order Quantity]  
            , OrdPrds.Item  
               (OrdPrds.CurrentOrdinal  
               )  
            )  
         )  
         OR (OrdPrds.CurrentOrdinal > 1   
            AND [Measures].[Reseller Order Quantity] =   
               ([Measures].[Reseller Order Quantity]  
               , OrdPrds.Item  
                  (OrdPrds.CurrentOrdinal-2)  
                )  
             )  
          ))  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
