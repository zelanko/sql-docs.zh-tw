---
title: Avg (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aa8817e35a589def4631bd455637d05fc62d3a0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017008"
---
# <a name="avg-mdx"></a>Avg (MDX)


  評估集合，並且在集合上的量值或指定量值平均後，傳回集合中資料格的非空值平均。  
  
## <a name="syntax"></a>語法  
  
```  
  
Avg( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果指定一組空的 tuple 或空的集合，則**Avg**函式會傳回空值。  
  
 **Avg**函式會先計算在指定集合中的資料格的 值的總和，然後再將導出的總和除以非空白資料格中的計數來計算指定集合中的儲存格的非空白值的平均值指定的集合。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在計算數字集合中的平均值時會忽略 Null。  
  
 如果未指定特定的數值運算式 （通常是量值）， **Avg**函式會計算目前查詢內容中的每個量值的平均值。 如果提供特定量值，則**Avg**函式會先評估量值集合，然後函式會計算指定量值的平均值。  
  
> [!NOTE]  
>  使用時**CurrentMember**函式中的導出的成員陳述式中，您必須指定數值運算式，因為有這樣的查詢內容中的目前座標沒有預設量值。  
  
 若要強制納入空白資料格，應用程式必須使用[CoalesceEmpty](../mdx/coalesceempty-mdx.md)函式，或指定有效*Numeric_Expression* ，提供空白值零 (0) 的值。 如需有關空的資料格的詳細資訊，請參閱 OLE DB 文件集。  
  
## <a name="examples"></a>範例  
 下列範例會傳回指定之集合中量值的平均值。 請注意，指定的量值可以是指定之集合成員的預設量值或是指定量值。  
  
 `WITH SET [NW Region] AS`  
  
 `{[Geography].[State-Province].[Washington]`  
  
 `, [Geography].[State-Province].[Oregon]`  
  
 `, [Geography].[State-Province].[Idaho]}`  
  
 `MEMBER [Geography].[Geography].[NW Region Avg] AS`  
  
 `AVG ([NW Region]`  
  
 `--Uncomment the line below to get an average by Reseller Gross Profit Margin`  
  
 `--otherwise the average will be by whatever the default measure is in the cube,`  
  
 `--or whatever measure is specified in the query`  
  
 `--, [Measures].[Reseller Gross Profit Margin]`  
  
 `)`  
  
 `SELECT [Date].[Calendar Year].[Calendar Year].Members ON 0`  
  
 `FROM [Adventure Works]`  
  
 `WHERE ([Geography].[Geography].[NW Region Avg])`  
  
 下列範例會傳回每日平均`Measures.[Gross Profit Margin]`量值，計算出的 2003年會計年度，每個月的天數**Adventure Works** cube。 **Avg**函式會計算內的每個月的天數集合的平均值`[Ship Date].[Fiscal Time]`階層。 第一個計算版本會顯示 Avg 從平均值中排除並未記錄任何銷售量之天數的預設行為，而第二個版本則顯示如何在平均值中包含沒有銷售量的天數。  
  
 `WITH MEMBER Measures.[Avg Gross Profit Margin] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `Measures.[Gross Profit Margin]`  
  
 `), format_String='percent'`  
  
 `MEMBER Measures.[Avg Gross Profit Margin Including Empty Days] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `CoalesceEmpty(Measures.[Gross Profit Margin],0)`  
  
 `), Format_String='percent'`  
  
 `SELECT`  
  
 `{Measures.[Avg Gross Profit Margin],Measures.[Avg Gross Profit Margin Including Empty Days]} ON COLUMNS,`  
  
 `[Ship Date].[Fiscal].[Fiscal Year].Members ON ROWS`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Product].&[344])`  
  
 下列範例會傳回每日平均`Measures.[Gross Profit Margin]`量值，計算出的 2003年會計年度每半年度**Adventure Works** cube。  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS  
   Avg(  
      Descendants(  
         [Ship Date].[Fiscal].CurrentMember,   
            [Ship Date].[Fiscal].[Date]  
      ),   
      Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
      [Ship Date].[Fiscal].[Fiscal Year].[FY 2003].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
