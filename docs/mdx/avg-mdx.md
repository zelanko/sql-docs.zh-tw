---
title: "Avg (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: AVG
dev_langs: kbMDX
helpviewer_keywords: Avg function [MDX]
ms.assetid: efe61272-c3eb-4a33-b231-e00c30be16aa
caps.latest.revision: "42"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: df33d2f9cacf83c845722bbd99c102ada42b0019
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="avg-mdx"></a>Avg (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 如果指定了一組空的 tuple 或空的集合， **Avg**函式會傳回空值。  
  
 **Avg**函式的第一次計算中指定的集合，儲存格上的 值的總和，然後計算總和的指定集合中的非空白資料格計數計算指定集合中的資料格的非空白值的平均值。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在計算數字集合中的平均值時會忽略 Null。  
  
 如果未指定特定的數值運算式 （通常是量值）， **Avg**函式會計算目前查詢內容中的每個量值的平均值。 如果提供特定量值，則**Avg**函數會先評估量值集合，並再計算平均數根據指定的量值。  
  
> [!NOTE]  
>  當使用**CurrentMember**函式中的導出的成員陳述式中，您必須指定數值運算式，因為有這樣的查詢內容中的目前座標沒有預設量值。  
  
 若要強制納入空白資料格，應用程式必須使用[CoalesceEmpty](../mdx/coalesceempty-mdx.md)函式，或請指定有效的*Numeric_Expression*提供空的值為零 (0) 的值。 如需有關空的資料格的詳細資訊，請參閱 OLE DB 文件集。  
  
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
  
 下列範例會傳回每日平均`Measures.[Gross Profit Margin]`量值，從計算中 2003年會計年度的每個月的每一日**Adventure Works** cube。 **Avg**函式計算平均值的天的每個月中所包含的一組從`[Ship Date].[Fiscal Time]`階層。 第一個計算版本會顯示 Avg 從平均值中排除並未記錄任何銷售量之天數的預設行為，而第二個版本則顯示如何在平均值中包含沒有銷售量的天數。  
  
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
  
 下列範例會傳回每日平均`Measures.[Gross Profit Margin]`量值，從計算中 2003年會計年度每半年度的每一日**Adventure Works** cube。  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
