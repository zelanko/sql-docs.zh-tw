---
description: '&lt; (小於)  (MDX) '
title: '&lt; (小於)  (MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 935b75d17db379d761641d994a06373c8503fffc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387294"
---
# <a name="lt-less-than-mdx"></a>&lt; (小於)  (MDX) 


  執行比對作業，判定某個多維度運算式 (MDX) 運算式的值是否小於另一個 MDX 運算式的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
MDX_Expression < MDX_Expression  
```  
  
#### <a name="parameters"></a>參數  
 *MDX_Expression*  
 有效的 MDX 運算式。  
  
## <a name="return-value"></a>傳回值  
 布林值根據以下條件而定：  
  
-   如果兩個參數都不是 null，而且第一個參數的值小於第二個參數的值，**則為 true** 。  
  
-   如果兩個參數都不是 null，而且第一個參數的值等於或大於第二個參數的值，則**為 false** 。  
  
-   Null，如果有一個參數或兩個參數都評估為 Null 值。  
  
## <a name="examples"></a>範例  
 以下範例示範此運算子的用法。  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for clothing sales where the GPM is less than 30%.  
With Member [Measures].[LowGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] < .3,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT NON EMPTY  
    [Sales Territory].[Sales Territory Country].Members ON 0,  
    [Product].[Category].[Clothing] ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[LowGPM])  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
