---
title: "建立工作階段範圍導出資料格 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: session-scoped calculated members [MDX]
ms.assetid: f2d14a89-6286-4e74-9afb-091076f93f21
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 766723fd1c3c05cfc556a39f7eea6ae3cb9a1141
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-cell-calculations---session-scoped-calculated-cells"></a>MDX 資料格計算工作階段範圍導出資料格
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
    
> [!IMPORTANT]  
>  此語法已經被取代。 您應該改用 MDX 指派。 如需指派的詳細資訊，請參閱[基本 MDX 指令碼 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)。  
  
 若要建立可供相同工作階段的所有查詢使用的導出資料格，您可以使用 [CREATE CELL CALCULATION](../../../mdx/mdx-data-definition-create-cell-calculation.md) 陳述式或 [ALTER CUBE](../../../mdx/mdx-data-definition-alter-cube.md) 陳述式。 兩個陳述式會有相同的結果。  
  
## <a name="create-cell-calculation-syntax"></a>CREATE CELL CALCULATION 語法  
  
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
  
## <a name="alter-cube-syntax"></a>ALTER CUBE 語法  
  
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
  
## <a name="see-also"></a>請參閱  
 [在 MDX 中建立資料格計算 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)  
  
  
