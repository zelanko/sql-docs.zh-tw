---
title: 使用集合運算式 |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3b384bffc84140b966ea510834054c65986ba292
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581720"
---
# <a name="using-set-expressions"></a>使用集合運算式
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  零個或多個 Tuple 之排序清單所組成的集合。 未包含任何 Tuple 的集合稱為空集合。  
  
 由零個或多個明確指定的 Tuple 而構成之集合的完整運算式 (嵌在大括號中)：  
  
 {[{ *Tuple_expression* | *Member_expression* } [，{ *Tuple_expression* | *Member_expression* }]...]}  
  
 集合運算式中指定的成員運算式可轉換成單一成員 Tuple 運算式。  
  
## <a name="example"></a>範例  
 下列範例示範查詢的資料行軸和資料列軸上使用的兩個集合運算式：  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]} ON COLUMNS,`  
  
 `{([Product].[Product Categories].[Category].&[4], [Date].[Calendar].[Calendar Year].&[2004]),`  
  
 `([Product].[Product Categories].[Category].&[1], [Date].[Calendar].[Calendar Year].&[2003]),`  
  
 `([Product].[Product Categories].[Category].&[3], [Date].[Calendar].[Calendar Year].&[2004])}`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 在資料行軸上，  
  
 集合 {[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}  
  
 是由 Measures 維度中的兩個成員所組成。 在資料列軸上，  
  
 集合 {([Product].[Product Categories].[Category].&[4], [Date].[Calendar].[Calendar Year].&[2004]),  
  
 ([Product].[Product Categories].[Category].&[1], [Date].[Calendar].[Calendar Year].&[2003]),  
  
 ([Product].[Product Categories].[Category].&[3], [Date].[Calendar].[Calendar Year].&[2004])}  
  
 是由三個 tuple 所組成，每一個 tuple 都包含 Product 維度之 Product Category 階層上之成員及 Date 維度之 Calendar 階層上之成員的兩個明確參考。  
  
 如需傳回集合之函數的範例，請參閱[使用成員、 Tuple 和集合&#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)。  
  
## <a name="see-also"></a>另請參閱  
 [運算式&#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
