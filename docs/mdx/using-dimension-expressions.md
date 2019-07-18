---
title: 使用維度運算式 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0373bbda2d0c97946f15e048b7cc49175ca66669
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097157"
---
# <a name="using-dimension-expressions"></a>使用維度運算式


  當您在多維度運算式 (MDX) 中傳遞參數給函數時，您通常會使用維度和階層運算式來傳回階層中的成員、集合或 tuple。  
  
 維度運算式只能是簡單運算式，因為它們是物件識別碼。 請參閱[運算式&#40;MDX&#41; ](../mdx/expressions-mdx.md)以了解簡單和複雜運算式。  
  
## <a name="dimension-expressions"></a>維度運算式  
 維度運算式包含維度識別碼或維度函數。  
  
 維度運算式很少單獨使用。 您通常會想要在維度上指定階層， 唯一的例外是當您使用沒有任何階層的 Measures 維度時。  
  
 下表顯示使用運算式 [Measures] 連同 .Members 和 Count() 函數的導出成員，以傳回 Measures 維度上的成員數目：  
  
 `WITH MEMBER [Measures].[MeasureCount] AS`  
  
 `COUNT([Measures].MEMBERS)`  
  
 `SELECT [Measures].[MeasureCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 維度識別碼會以*Dimension_Name*在 backus-naur form，BNF 標記法中用來描述 MDX 陳述式。  
  
## <a name="hierarchy-expressions"></a>階層運算式  
 同樣地，階層運算式包含階層識別碼或階層函數。 下列範例示範階層運算式 [Date].[Calendar] 連同 .Levels 和 .Count 函數的使用，以傳回 Date 維度之 Calendar 階層中的層級數目：  
  
 `WITH MEMBER [Measures].[CalendarLevelCount] AS`  
  
 `[Date].[Calendar].Levels.Count`  
  
 `SELECT [Measures].[CalendarLevelCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 使用階層運算式的最常見案例是搭配 .Members 函數使用來傳回階層上的所有成員。 下列範例會傳回資料列軸上 [Date].[Calendar] 的所有成員：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 階層識別碼會以*Dimension_Name.Hierarchy_Name*在 backus-naur form，BNF 標記法中用來描述 MDX 陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [運算式&#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
