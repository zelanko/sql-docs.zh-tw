---
title: CurrentOrdinal （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 38ac7a3f4c966f9496f5ff9a0855960da8a38fb6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68135876"
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
 當逐一查看集合（例如使用[Filter （mdx）](../mdx/filter-mdx.md)或[產生（mdx）](../mdx/generate-mdx.md)函數）時， **CurrentOrdinal**函數會傳回反復專案編號。  
  
## <a name="examples"></a>範例  
 下列簡單範例示範如何搭配 [**產生**] 來使用**CurrentOrdinal** ，以傳回字串，其中包含集合中每個專案的名稱，以及其在集合中的位置：  
  
 `WITH SET MySet AS [Customer].[Customer Geography].[Country].MEMBERS`  
  
 `MEMBER MEASURES.CURRENTORDINALDEMO AS`  
  
 `GENERATE(MySet, CSTR(MySet.CURRENTORDINAL) + ") " + MySet.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTORDINALDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
 CurrentOrdinal 的實際使用限制為非常複雜的計算。 下列範例會傳回唯一的集合中的產品數目，使用**order**函數來排序非空白的元組，然後再利用**篩選**函數。 **CurrentOrdinal**函數是用來比較和消除系結。  
  
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
  
  
