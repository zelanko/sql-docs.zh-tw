---
title: 根（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: be687d5cbfd4fdbb706ef5c10778a4f3e3f93197
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68037044"
---
# <a name="root-mdx"></a>Root (MDX)


  傳回由 cube、維度或元組中目前範圍內的每個屬性階層中的**所有**成員所組成的元組。 如需有關範圍的詳細資訊，請參閱[Scope 語句 &#40;MDX&#41;](../mdx/mdx-scripting-scope.md)。  
  
> [!NOTE]  
>  如果屬性階層沒有**All**成員，則元組會包含該階層的預設成員。  
  
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
 如果沒有指定維度名稱或元組運算式，**根**函數會傳回一個元組，其中包含 cube 中每個屬性階層的**all**成員（如果**所有**成員不存在，則為預設成員）。 Tuple 內的成員順序是根據 Cube 內定義的屬性階層順序來排序。  
  
 如果指定了維度名稱，**根**函式會根據目前成員的內容，從指定之維度的每個屬性階層中，傳回包含**all**成員（如果**所有**成員不存在，則為預設成員）的元組。 Tuple 內的成員順序是根據維度內定義的屬性階層順序來排序。  
  
> [!NOTE]  
>  如果指定了階層名稱，則**元組**函數會從指定的階層名稱中挑選維度名稱。  
  
 如果指定了元組運算式，**根**函數會傳回一個元組，其中包含指定之元組的交集，以及未明確包含在指定之元組中的所有其他維度屬性的**所有**成員。  
  
## <a name="examples"></a>範例  
 下列範例會從「艾德公司」 cube 中的每個階層傳回包含「**全部**」成員（如果「**全部**」成員不存在，則為預設值）的元組。  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會從「艾德作品」 cube 中的「日期」維度中的每個階層，以及與這些預設成員交集之「量值」維度之指定成員的值，傳回包含「**全部**」成員（或「**全部**」成員不存在的預設值）的元組。  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 下列範例會傳回包含指定之元組成員的元組（2001年7月1日，連同**all**成員（如果**所有**成員不存在則為預設值），從 Date 維度中的每個非指定階層，以及與這些成員交集之量值維度的指定成員值。  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
