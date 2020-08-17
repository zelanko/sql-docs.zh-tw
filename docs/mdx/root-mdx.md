---
description: Root (MDX)
title: 根 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a408250de53e3d77750d6ea9a87aa679152a86d8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341304"
---
# <a name="root-mdx"></a>Root (MDX)


  傳回包含 cube、維度或元組中目前範圍內每個屬性階層之 **所有** 成員的元組。 如需範圍的詳細資訊，請參閱 [範圍語句 &#40;MDX&#41;](../mdx/mdx-scripting-scope.md)。  
  
> [!NOTE]  
>  如果屬性階層沒有 **All** 成員，元組會包含該階層的預設成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Cube syntax  
Root ()  
Dimension syntax  
Root( Dimension_Name )  
Tuple syntax  
Root( Tuple_Expression )  
```  
  
## <a name="arguments"></a>引數  
 *Dimension_Name*  
 指定維度名稱的有效字串運算式。  
  
 *Tuple_Expression*  
 傳回 Tuple 的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果未指定維度名稱或元組運算式， **根** 函數會傳回包含 **all** 成員 (或預設成員的元組，如果 cube 中的每個屬性階層) 都不存在 **all** 成員的話。 Tuple 內的成員順序是根據 Cube 內定義的屬性階層順序來排序。  
  
 如果指定了維度名稱， **根** 函數會傳回包含 **all** 成員 (或預設成員的元組，如果從指定維度的每個屬性階層架構中， **所有** 成員都不存在，則會根據目前成員的內容) 。 Tuple 內的成員順序是根據維度內定義的屬性階層順序來排序。  
  
> [!NOTE]  
>  如果指定階層名稱， **元組** 函數會從指定的階層名稱中挑選維度名稱。  
  
 如果指定了元組運算式， **根** 函數會傳回一個元組，其中包含指定之元組的交集，以及未明確包含在指定之元組中的所有其他維度屬性的 **所有** 成員。  
  
## <a name="examples"></a>範例  
 下列範例會傳回包含 **all** 成員的元組 (或預設值（如果 **所有** 成員都不存在於 [艾德作品] cube 中的每個階層) ）。  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會傳回包含 **all** 成員的元組 (或預設值，如果 **所有** 成員都不存在於 [艾德作品] cube 的 [日期] 維度中的每個階層) ，以及與這些預設成員交集之 [量值] 維度的指定值。  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 下列範例會傳回包含指定之元組成員的元組 (2001 年7月1日，以及 **所有** 成員 (或預設值（如果 **所有** 成員都不存在）) 從日期維度的 [艾德作品] cube 中的每個非指定階層，以及與這些成員交集之 [量值] 維度的 [值]。  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
