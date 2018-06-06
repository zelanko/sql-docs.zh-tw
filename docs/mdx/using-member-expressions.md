---
title: 使用成員運算式 |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bdf16151dac1e55e6fe41d76078b5fc409fd36d3
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581530"
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
  
 存在著許多會傳回成員的 MDX 函數。 如需完整清單，請參閱[MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
> [!NOTE]  
>  如需有關成員名稱及成員索引鍵的詳細資訊，請參閱[使用成員、 Tuple 和集合&#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)。  
  
## <a name="see-also"></a>另請參閱  
 [運算式&#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
