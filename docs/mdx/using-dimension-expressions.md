---
title: 使用維度運算式 |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- expressions [MDX], dimensions
- dimensions [Analysis Services], MDX
ms.assetid: 1d40cffb-e88f-4284-93cf-d62ab4f08395
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1417fd747df92c84fe66e2c69996f57ab51875e1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="using-dimension-expressions"></a>使用維度運算式
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  當您在多維度運算式 (MDX) 中傳遞參數給函數時，您通常會使用維度和階層運算式來傳回階層中的成員、集合或 tuple。  
  
 維度運算式只能是簡單運算式，因為它們是物件識別碼。 請參閱[運算式 &#40;MDX &#41;](../mdx/expressions-mdx.md)取得簡單和複雜運算式的說明。  
  
## <a name="dimension-expressions"></a>維度運算式  
 維度運算式包含維度識別碼或維度函數。  
  
 維度運算式很少單獨使用。 您通常會想要在維度上指定階層， 唯一的例外是當您使用沒有任何階層的 Measures 維度時。  
  
 下表顯示使用運算式 [Measures] 連同 .Members 和 Count() 函數的導出成員，以傳回 Measures 維度上的成員數目：  
  
 `WITH MEMBER [Measures].[MeasureCount] AS`  
  
 `COUNT([Measures].MEMBERS)`  
  
 `SELECT [Measures].[MeasureCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 維度識別碼會顯示為*Dimension_Name*中用來描述 MDX 陳述式的 BNF 標記法。  
  
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
  
 階層識別碼會以*Dimension_Name**。**Hierarchy_Name*中用來描述 MDX 陳述式的 BNF 標記法。  
  
## <a name="see-also"></a>請參閱  
 [運算式 &#40;MDX &#41;](../mdx/expressions-mdx.md)  
  
  
