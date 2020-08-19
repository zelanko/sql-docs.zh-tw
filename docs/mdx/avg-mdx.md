---
description: Avg (MDX)
title: Avg (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e5cac19b597139274502d455fb5f8f4e5087c8a2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477060"
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
 如果指定了一組空的元組或空的集合， **Avg** 函數會傳回空值。  
  
 **Avg**函數會先計算指定集合中資料格的值總和，然後將計算的總和除以指定集合中非空白資料格的計數，藉以計算指定集合中資料格非空白值的平均值。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在計算數字集合中的平均值時會忽略 Null。  
  
 如果特定的數值運算式 (通常未指定量值) ， **Avg** 函數會將目前查詢內容中的每個量值平均。 如果有提供特定量值， **Avg** 函數會先評估集合上的量值，然後函數會根據指定的量值計算平均值。  
  
> [!NOTE]  
>  在匯出成員語句中使用 **CurrentMember** 函數時，您必須指定數值運算式，因為這類查詢內容中目前的座標沒有預設量值存在。  
  
 若要強制包含空的資料格，應用程式必須使用 [CoalesceEmpty](../mdx/coalesceempty-mdx.md) 函數或指定有效的 *Numeric_Expression* ，以提供零 (0) 的空白值。 如需有關空的資料格的詳細資訊，請參閱 OLE DB 文件集。  
  
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
  
 下列範例會傳回每日平均量值的平均值，其計算方式是在 `Measures.[Gross Profit Margin]` 2003 會計年度的每個月天數內，從「 **艾德作品** 」 cube 計算。 **Avg**函數會計算階層中每個月所包含的一組天數的平均值 `[Ship Date].[Fiscal Time]` 。 第一個計算版本會顯示 Avg 從平均值中排除並未記錄任何銷售量之天數的預設行為，而第二個版本則顯示如何在平均值中包含沒有銷售量的天數。  
  
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
  
 下列範例會傳回每日平均量值的平均值，其計算方式是在 `Measures.[Gross Profit Margin]` 2003 會計年度的每半年度天數內，從「發件工作」 cube 算 **起** 。  
  
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
  
  
