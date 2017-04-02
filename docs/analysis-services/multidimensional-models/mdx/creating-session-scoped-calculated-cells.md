---
title: "建立工作階段範圍導出資料格 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "工作階段範圍導出成員 [MDX]"
ms.assetid: f2d14a89-6286-4e74-9afb-091076f93f21
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 建立工作階段範圍導出資料格
    
> [!IMPORTANT]  
>  此語法已經被取代。 您應該改用 MDX 指派。 如需指派的詳細資訊，請參閱[基本 MDX 指令碼 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)。  
  
 若要建立可供相同工作階段的所有查詢使用的導出資料格，您可以使用 [CREATE CELL CALCULATION](../Topic/CREATE%20CELL%20CALCULATION%20Statement%20\(MDX\).md) 陳述式或 [ALTER CUBE](../Topic/ALTER%20CUBE%20Statement%20\(MDX\).md) 陳述式。 兩個陳述式會有相同的結果。  
  
## CREATE CELL CALCULATION 語法  
  
> [!IMPORTANT]  
>  此語法已經被取代。 您應該改用 MDX 指派。 如需指派的詳細資訊，請參閱[基本 MDX 指令碼 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)。  
  
 請使用下列語法以使用 CREATE CELL CALCULATION 陳述式，定義工作階段範圍導出資料格：  
  
```  
CREATE CELL CALCULATION Cube_Expression.<CREATE CELL CALCULATION body clause>  
  
<CREATE CELL CALCULATION body clause> ::=CellCalc_Identifier FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
## ALTER CUBE 語法  
  
> [!IMPORTANT]  
>  此語法已經被取代。 您應該改用 MDX 指派。 如需指派的詳細資訊，請參閱[基本 MDX 指令碼 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)。  
  
 請使用下列語法以使用 ALTER CUBE 述式，定義工作階段範圍導出資料格：  
  
```  
ALTER CUBE Cube_Identifier CREATE CELL CALCULATION  
FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
 `String_Expression` 值包含正交、一維的 MDX 集合運算式的清單，其中的每一項都必須解析成下表列出集合的其中一個類別目錄  
  
|類別目錄|說明|  
|--------------|-----------------|  
|空集合|解析成空集合的 MDX 命名集運算式。 在此情況下，導出資料格的範圍是整個 Cube。|  
|單一成員集合|解析成單一成員集合的 MDX 命名集運算式。|  
|單一層級成員|解析成單一層級成員的 MDX 命名集運算式。 *Level_Expression*.**Members** MDX 函數即為一例。 若要包括導出成員，請使用 *Level_Expression*.**AllMembers** MDX 函數。<br /><br /> 如需詳細資訊，請參閱 [AllMembers &#40;MDX&#41;](../../../mdx/allmembers-mdx.md)。|  
|下階集合|解析為指定成員之下階的 MDX 集合運算式。 **Descendants**(*Member_Expression*, *Level_Expression*, *Desc_Flag*) MDX 函數即為一例。<br /><br /> 如需詳細資訊，請參閱 [Descendants &#40;MDX&#41;](../../../mdx/descendants-mdx.md)。|  
  
## 請參閱＜  
 [在 MDX 中建立資料格計算 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-cell-calculations-in-mdx-mdx.md)  
  
  