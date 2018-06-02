---
title: DistinctCount (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0a1b844e6f50f4eb75c4418e71b7b9aaead518fc
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580520"
---
# <a name="distinctcount-mdx"></a>DistinctCount (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回集合中相異 (Distinct) Tuple、非空白 Turple 的數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
DistinctCount(Set_Expression)  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **DistinctCount**函數即相當於`Count(Distinct(Set_Expression), EXCLUDEEMPTY)`。  
  
## <a name="examples"></a>範例  
 下列查詢會示範如何使用 DistinctCount 函數：  
  
 `WITH SET MySet AS`  
  
 `{[Customer].[Customer Geography].[Country].&[Australia],[Customer].[Customer Geography].[Country].&[Australia],`  
  
 `[Customer].[Customer Geography].[Country].&[Canada],[Customer].[Customer Geography].[Country].&[France],`  
  
 `[Customer].[Customer Geography].[Country].&[United Kingdom],[Customer].[Customer Geography].[Country].&[United Kingdom]}`  
  
 `*`  
  
 `{([Date].[Calendar].[Date].&[20010701],[Measures].[Internet Sales Amount] )}`  
  
 `//Returns the value 3 because Internet Sales Amount is null`  
  
 `//for the UK on the date specified`  
  
 `MEMBER MEASURES.SETDISTINCTCOUNT AS`  
  
 `DISTINCTCOUNT(MySet)`  
  
 `SELECT {MEASURES.SETDISTINCTCOUNT} ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [計數&#40;設定&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
