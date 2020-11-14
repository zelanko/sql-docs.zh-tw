---
description: DistinctCount (MDX)
title: DistinctCount (MDX) |Microsoft Docs
ms.date: 11/12/2020
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 28807d1a24f97a6b197ad56d0434399ab53cd742
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584845"
---
# <a name="distinctcount-mdx"></a>DistinctCount (MDX)


  傳回集合中相異 (Distinct) Tuple、非空白 Turple 的數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
DistinctCount(Set_Expression)  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **DistinctCount** 函數相當於 `Count(Distinct(Set_Expression), EXCLUDEEMPTY)` 。  
  
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
 
DistinctCount 函數會傳回集合中的相異專案數;在此範例中，選擇性的第二個參數是用來排除沒有指定元組值的專案。 在此案例中，第一個參數的集合中有四個不同的專案，但此函式會傳回三個，因為只有澳大利亞、加拿大和法國的資料有7月 1 2001 日的網際網路銷售量。
 
## <a name="see-also"></a>另請參閱  
 [&#40;設定&#41; &#40;MDX&#41;的計數 ](../mdx/count-set-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
