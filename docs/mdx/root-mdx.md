---
title: Root (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c2301f44cbdac4505bef95d590ce206c8b6b509
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150242"
---
# <a name="root-mdx"></a>Root (MDX)


  傳回組成的 tuple**所有**cube、 維度或 tuple 中目前的範圍內的每個屬性階層的成員。 如需有關範圍的詳細資訊，請參閱 < [SCOPE 陳述式&#40;MDX&#41;](../mdx/mdx-scripting-scope.md)。  
  
> [!NOTE]  
>  如果屬性階層沒有**所有**成員、 tuple 包含該階層的預設成員。  
  
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
 如果指定不是維度名稱，也不是 tuple 運算式，則**根**函式會傳回 tuple，其中包含**所有**成員 (或預設成員如果**所有**成員不存在） 的每個屬性階層在 cube 中。 Tuple 內的成員順序是根據 Cube 內定義的屬性階層順序來排序。  
  
 如果指定的維度名稱，則**根**函式會傳回 tuple，其中包含**所有**成員 (或預設成員如果**所有**成員不存在) 從每個根據目前成員內容之指定維度中的屬性階層。 Tuple 內的成員順序是根據維度內定義的屬性階層順序來排序。  
  
> [!NOTE]  
>  如果指定階層名稱，則**Tuple**函式會挑選維度名稱，從指定的階層名稱。  
  
 如果指定 tuple 運算式，則**根**函式會傳回 tuple，其中包含指定之 tuple 的交集，**所有**未明確成員的所有其他維度的屬性包含在指定的 tuple。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 tuple，其中包含**所有**成員 (預設值或如果**所有**成員不存在) 的 Adventure Works cube 中每個階層。  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會傳回 tuple，其中包含**所有**成員 (預設值或如果**所有**成員不存在) 的 Adventure Works cube 和的值中的 [日期] 維度中每個階層指定的成員的量值維度成員集合交集與這些預設成員。  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 下列範例會傳回 tuple，其中包含指定的 tuple 成員 (July 1，2001，連同**所有**成員 (或預設值如果**所有**成員不存在) 中每個非指定階層日期維度 Adventure Works cube 中，與這些成員交集之 Measures 維度的指定成員的值。  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
