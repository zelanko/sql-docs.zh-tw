---
title: Count （集合）（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aac2f72cc8cd91e1964fd7734b858be8215cfdd8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68047290"
---
# <a name="count-set-mdx"></a>Count (集合) (MDX)


  傳回集合中的資料格數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
Standard syntax  
Count(Set_Expression [ , ( EXCLUDEEMPTY | INCLUDEEMPTY ) ] )  
  
Alternate syntax  
Set_Expression.Count  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **Count （Set）** 函數包含或排除空的資料格，視所使用的語法而定。 如果使用標準語法，則可以分別使用**EXCLUDEEMPTY**或**INCLUDEEMPTY**旗標來排除或包含空的資料格。 如果使用替代語法，此函數永遠會包括空資料格。  
  
 若要在集合的計數中排除空的資料格，請使用標準語法和選擇性的**EXCLUDEEMPTY**旗標。  
  
> [!NOTE]  
>  **Count （Set）** 函數預設會計算空白資料格的數目。 相反地，OLE DB 中計算集合的**Count**函數預設會排除空的資料格。  
  
## <a name="examples"></a>範例  
 下列範例會計算成員集合中的資料格數目，該成員集合由 Product 維度中 Model Name 屬性階層的子系組成。  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會使用**DrilldownLevel**函數搭配**Count**函數，計算 Product 維度中的產品數目。  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 下列範例會使用**Count**函數搭配**篩選**函數和一些其他函式，來傳回與上一個日曆季相比，與上一個行事曆相比，具有下降銷售量的轉銷商。 此查詢會使用**聚合**函數來支援選取多個 geography 成員，例如在用戶端應用程式的下拉式清單中進行選取。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
   (Filter  
      (Existing(Reseller.Reseller.Reseller),  
         [Measures].[Reseller Sales Amount]   
         < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
      )  
   )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate  
   ( {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
   )  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})  
      })  
   ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,  
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
   ,[Measures].[Declining Reseller Sales])  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;維度&#41; &#40;MDX&#41;計數](../mdx/count-dimension-mdx.md)   
 [&#40;&#41; &#40;MDX 的階層層級計數&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [計算 &#40;元組&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [MDX&#41;的屬性 &#40;](../mdx/properties-mdx.md)   
 [匯總 &#40;MDX&#41;](../mdx/aggregate-mdx.md)   
 [篩選 &#40;MDX&#41;](../mdx/filter-mdx.md)   
 [PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
