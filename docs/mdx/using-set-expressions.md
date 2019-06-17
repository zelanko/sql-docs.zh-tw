---
title: 使用集合運算式 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 012a2946ff931e1326dcd3fa6321472761d67c56
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62861702"
---
# <a name="using-set-expressions"></a>使用集合運算式


  零個或多個 Tuple 之排序清單所組成的集合。 未包含任何 Tuple 的集合稱為空集合。  
  
 由零個或多個明確指定的 Tuple 而構成之集合的完整運算式 (嵌在大括號中)：  
  
 {[{ *Tuple_expression* | *Member_expression* } [，{ *Tuple_expression* | *Member_expression* } ] ... ]}  
  
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
  
 {([Product]。[產品類別目錄]。[Category]。 [4] 和 [日期]。[行事曆]。[Calendar Year]。 & [2004])，  
  
 ([Product]。[產品類別目錄]。[Category]。 [1] 和 [日期]。[行事曆]。[Calendar Year]。 & [2003])，  
  
 ([Product]。[產品類別目錄]。[Category]。 [3] 與 [日期]。[行事曆]。[Calendar Year]。 year.&[2004])}  
  
 是由三個 tuple 所組成，每一個 tuple 都包含 Product 維度之 Product Category 階層上之成員及 Date 維度之 Calendar 階層上之成員的兩個明確參考。  
  
 例如，傳回集合的函式的詳細資訊，請參閱[使用成員、 Tuple 和集合&#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)。  
  
## <a name="see-also"></a>另請參閱  
 [運算式&#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
