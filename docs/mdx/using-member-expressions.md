---
title: 使用成員運算式 |Microsoft 文件
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
- members [MDX], expressions
- expressions [MDX], members
ms.assetid: 63c7af49-8bea-47c5-9566-a961f77d2a3d
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: bc1574fc06eeaa032fb68d395106721fc33ec699
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="using-member-expressions"></a>使用成員運算式
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  成員運算式包含成員識別碼、成員函數或可轉換為成員的運算式。  
  
 成員識別碼可以有許多不同格式。 最簡單的成員識別碼形式是由成員的名稱所組成。 例如：  
  
```  
SELECT Amount ON 0  
FROM [Adventure Works]  
  
```  
  
 例如，如果不同階層上有幾個同名的成員，並沒有任何方法可以判斷查詢將會傳回哪一個成員。 例如，下列查詢會要求 [CY 2004] 名稱之成員的資料。 此查詢會順利執行，但是 Adventure Works Cube 中至少有六個成員具有該名稱：  
  
```  
SELECT [CY 2004] ON 0  
FROM [Adventure Works]  
  
```  
  
 因此，最可靠的成員識別碼形式就是成員的唯一名稱，此名稱可保證能夠識別 Cube 內的特定成員。 Analysis Services 可透過幾種方式產生唯一名稱，但是唯一名稱至少是由兩個識別碼所組成：維度名稱，以及成員名稱或成員索引鍵。 唯一名稱會以下列格式出現：  
  
```  
  
Dimension_Name  
.[Hierarchy_Name.] [[{Member_Name | &Member_Key}.]... ] {Member_Name | &Member_Key}  
  
```  
  
 以下是 Adventure Works Cube 中成員唯一名稱的一些範例：  
  
```  
[Measures].[Amount]  
[Date].[Calendar Year].&[2004]  
[Date].[Calendar].[Calendar Quarter].&[2004]&[1]  
[Employee].[Employees].&[112]  
[Product].[Product Categories].[All Products]  
  
```  
  
 存在著許多會傳回成員的 MDX 函數。 如需完整清單，請參閱[MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
> [!NOTE]  
>  如需有關成員名稱及成員索引鍵的詳細資訊，請參閱[使用成員、 Tuple 及集合 &#40;MDX &#41;](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md).  
  
## <a name="see-also"></a>請參閱  
 [運算式 &#40;MDX &#41;](../mdx/expressions-mdx.md)  
  
  
