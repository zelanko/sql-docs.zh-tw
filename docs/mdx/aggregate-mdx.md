---
title: 匯總（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6c75ab71456dc8b7ffc3efdf6bd157693de14881
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68017176"
---
# <a name="aggregate-mdx"></a>Aggregate (MDX)


  傳回數字，該數字是彙總集合運算式傳回的資料格所計算出。 如果沒有指定數值運算式，此函數會使用為每個量值指定的預設彙總運算子，彙總目前查詢內容中的每個量值。 如果提供了數值運算式，此函數會先評估然後加總指定之集合中每個資料格的數值運算式。  
  
## <a name="syntax"></a>語法  
  
```  
  
Aggregate(Set_Expression [ ,Numeric_Expression ])  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果已指定空的 Tuple 集合或空的集合，此函數會傳回空白值。  
  
 下表描述**聚合**函數如何與不同的彙總函式搭配運作。  
  
|彙總運算子|結果|  
|--------------------------|------------|  
|Sum|傳回集合上的值總和。|  
|Count|傳回集合上的值計數。|  
|最大值|傳回集合上的最大值。|  
|最小值|傳回集合上的最小值。|  
|局部加總彙總函式|將形狀投射到時間座標軸後，傳回在集合上局部加總行為的計算。|  
|Distinct Count|當 Slicer 座標軸包含一個集合時，彙總提供給 Subcube 的事實資料。<br /><br /> 傳回集合中每個成員的相異計數。 結果相依於所彙總之資料格的安全性，而非計算所需之資料格的安全性。 集合上的資料格安全性會產生錯誤；指定集合之資料粒度以下的資料格安全性會被忽略。 集合上的計算會產生錯誤。 資料的資料粒度以下的計算會被忽略。 相異計數含成員及其一個或多個子系的集合，會傳回提供給子成員之事實的相異計數。|  
|無法彙總的屬性。|傳回值的總和。|  
|混合的彙總函式。|不支援，而且會引發錯誤。|  
|一元運算子|不接受；值是藉由加總進行彙總。|  
|導出量值|解決集合順序，以確保導出量值適用。|  
|導出成員|一般規則適用，即最後一個求解順序優先使用。|  
|指派|指派是根據量值彙總函式進行彙總。 如果量值彙總函式是相異計數，則指派是加總的。|  
  
## <a name="examples"></a>範例  
 下列範例會從「**艾德公司**」 `Measures.[Order Quantity]` cube 中傳回成員的總和（在`Date`維度中包含的前八2003個月內）。  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 下列範例會彙總 2003 日曆年度下半年度的前 2 個月。  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Semester],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 下列範例會根據使用彙總函式評估之使用者選取的 State-Province 成員值，傳回上一個時間週期銷售值衰退的轉售商計數。 **Hierarchize**和**DrillDownLevel**函數是用來傳回 product 維度中產品類別目錄的拒絕銷售值。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS   
   Count(  
      Filter(  
         Existing(Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
            )  
         )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate (   
      {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
         )  
SELECT NON EMPTY Hierarchize (  
   AddCalculatedMembers (  
      {DrillDownLevel({[Product].[All Products]})}  
         )  
   )  
        DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
    [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
    [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>另請參閱  
 [PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md)   
 [&#40;MDX&#41;的子系](../mdx/children-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [&#40;&#41; &#40;MDX&#41;設定計數](../mdx/count-set-mdx.md)   
 [篩選 &#40;MDX&#41;](../mdx/filter-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX&#41;的屬性 &#40;](../mdx/properties-mdx.md)   
 [PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
