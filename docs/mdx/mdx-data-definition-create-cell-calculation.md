---
description: MDX 資料定義 - CREATE CELL CALCULATION
title: CREATE CELL CALCULATION 語句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 94f2a2286b72aac5a8698fad7ba0085f2a6ad8d0
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196995"
---
# <a name="mdx-data-definition---create-cell-calculation"></a>MDX 資料定義 - CREATE CELL CALCULATION


  在 Cube 內指定的 Tuple 集合上，建立評估多維度運算式 (MDX) 運算式的計算。  
  
## <a name="syntax"></a>語法  
  
```  
  
[WITH <CELL CALCULATION clause> Calculation_Name  
   [,WITH <CELL CALCULATION clause> Calculation_Name...n]  
CREATE CELL CALCULATION CURRENTCUBE | Cube_Name.Calculation_Name   
  
<CELL CALCULATION clause> ::=  
   FOR Set_Expression AS 'MDX_Expression'   
      [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 提供 Cube 名稱的有效字串。  
  
 *Calculation_Name*  
 提供資料格計算名稱的有效字串。  
  
 *Set_Expression*  
 傳回集合的有效 MDX 運算式。  
  
 *String*  
 有效的字串值。  
  
 *MDX_Expression*  
 有效的 MDX 運算式。  
  
 *Logical_Expression*  
 有效的 MDX 邏輯運算式。  
  
 *整數*  
 有效的整數值。  
  
 *Calculation_Name*  
 提供資料格計算屬性名稱的有效字串。  
  
 *Scalar_Expression*  
 有效的 MDX 純量運算式。  
  
## <a name="remarks"></a>備註  
 在自訂積存公式或導出成員的情況下，使用導出資料格，用戶端應用程式就可以指定特定資料格集的積存值，而非整個資料格集的積存值。 例如，可以指定由 `{[Canada],[Time].[2000]}` 定義的集合內，任何資料格都可以包含由公式定義的值。 此集合以外的其他資料格，則會正常進行運算。  
  
> [!NOTE]  
>  為了回溯相容性，會將 `{*(<comment> | <whitespace> | <newline>)}` 的巴克斯格式 (Backus-Naur Form，BNF) 剖析為 `{*}`。  
  
## <a name="see-also"></a>另請參閱  
 [建立 Session-Scoped 計算儲存格](/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells)   
 [&#40;MDX&#41;建立 Query-Scoped 資料格計算 ](/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations)   
 [在 MDX 中建立資料格計算 &#40;MDX&#41;](/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations)   
 [使用資料格屬性 &#40;MDX&#41;](/analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties)   
 [FORMAT_STRING 的內容 &#40;MDX&#41;](/analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents)   
 [FORE_COLOR 和 BACK_COLOR 內容 &#40;MDX&#41;](/analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents)   
 [Mdx 資料定義語句 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
