---
title: Sum （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb4e9d55ef2228404dd9113170066e4a3612a0a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036669"
---
# <a name="sum-mdx"></a>Sum (MDX)


  針對指定的集合進行評估之後，傳回數值運算式的總合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Sum( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 有效的多維度運算式 (MDX) 集合運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果有指定數值運算式，會使用該數值運算式評估集合，取得總合。 如果沒有指定數值運算式，則會在集合成員的目前內容中評估指定的集合，取得總合。 如果將 SUM 函數套用至非數值運算式，會產生未定義的結果。  
  
> [!NOTE]  
>  Analysis Services 在計算數字集合中的總和時會忽略 Null。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 2001 和 2002 日曆年度 Product.Category 屬性階層之所有成員的 Reseller Sales Amounts 總合。  
  
```  
WITH MEMBER Measures.x AS SUM  
   ( { [Date].[Calendar Year].&[2001]  
         , [Date].[Calendar Year].&[2002] }  
      , [Measures].[Reseller Sales Amount]  
    )  
SELECT Measures.x ON 0  
,[Product].[Category].Members ON 1  
FROM [Adventure Works]  
```  
  
 下列範例會傳回 2002 年 7 月初至 7 月 20 日網際網路銷售的運費成本總合。  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會使用 WITH MEMBER 關鍵字和**SUM**函數來定義量值維度中的匯出成員，其中包含 Geography 維度中 Country 屬性階層之加拿大和美國成員的「轉售商銷售量」量值總和。  
  
```  
WITH MEMBER Measures.NorthAmerica AS SUM   
      (  
         {[Geography].[Country].&[Canada]  
            , [Geography].[Country].&[United States]}  
       ,[Measures].[Reseller Sales Amount]  
      )  
SELECT {[Measures].[NorthAmerica]} ON 0,  
[Product].[Category].members ON 1  
FROM [Adventure Works]  
```  
  
 **SUM**函數通常會與**CURRENTMEMBER**函式搭配使用，而這類函數會傳回根據階層 CURRENTMEMBER 而**有所不同的集合**。 例如，下列查詢會傳回從日曆年度開始到 Rows 軸上所顯示日期之間所有日期的 Internet Sales Amount 量值總和。  
  
 `WITH MEMBER MEASURES.YTDSUM AS`  
  
 `SUM(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDSUM} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
