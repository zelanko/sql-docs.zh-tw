---
title: "Count （集合） (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COUNT
dev_langs:
- kbMDX
helpviewer_keywords:
- Count function [MDX]
ms.assetid: 22f530e9-f8e1-4608-affa-9a2bc0821591
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 97a997760b2796bc0fb7708503caf1a278e0d59d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="count-set-mdx"></a>Count (集合) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 **Count （集合）**函式包含或排除空白資料格，根據使用的語法。 如果使用標準語法時，可以排除或包含使用空資料格**EXCLUDEEMPTY**或**INCLUDEEMPTY**分別旗標。 如果使用替代語法，此函數永遠會包括空資料格。  
  
 若要排除的一組計數中空白資料格，請使用標準語法與選擇性**EXCLUDEEMPTY**旗標。  
  
> [!NOTE]  
>  **Count （集合）**函數預設會計算空白資料格。 相反地，**計數**函式在 OLE DB，它會計算一組預設排除空白資料格。  
  
## <a name="examples"></a>範例  
 下列範例會計算成員集合中的資料格數目，該成員集合由 Product 維度中 Model Name 屬性階層的子系組成。  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會計算 Product 維度中的產品數目使用**DrilldownLevel**函數搭配**計數**函式。  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 下列範例會傳回使用相較於先前的日曆季銷售量衰退的轉售商**計數**函數搭配**篩選**函式和一些其他功能。 此查詢會使用**彙總**函式，以支援選取的多個地理位置的成員，例如從用戶端應用程式中的下拉式清單中選取項目。  
  
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
 [計數 &#40; 維度 &#41;&#40;MDX &#41;](../mdx/count-dimension-mdx.md)   
 [計數 &#40;階層層級 &#41;&#40;MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [計數 &#40;Tuple &#41;&#40;MDX &#41;](../mdx/count-tuple-mdx.md)   
 [DrilldownLevel &#40;MDX &#41;](../mdx/drilldownlevel-mdx.md)   
 [AddCalculatedMembers &#40;MDX &#41;](../mdx/addcalculatedmembers-mdx.md)   
 [Hierarchize &#40;MDX &#41;](../mdx/hierarchize-mdx.md)   
 [屬性 &#40;MDX &#41;](../mdx/properties-mdx.md)   
 [彙總 &#40;MDX &#41;](../mdx/aggregate-mdx.md)   
 [篩選 &#40;MDX &#41;](../mdx/filter-mdx.md)   
 [PrevMember &#40;MDX &#41;](../mdx/prevmember-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

