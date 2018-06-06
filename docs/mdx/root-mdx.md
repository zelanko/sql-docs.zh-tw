---
title: 根 (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8dd99d852ab33088d4af6df9bd06386b0e8877ab
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580730"
---
# <a name="root-mdx"></a>Root (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回 tuple 所組成，**所有**cube、 維度或 tuple 中目前的範圍內的每個屬性階層的成員。 如需範圍的詳細資訊，請參閱[SCOPE 陳述式&#40;MDX&#41;](../mdx/mdx-scripting-scope.md)。  
  
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
 如果指定維度名稱都是 tuple 運算式，則**根**函式會傳回 tuple，其中包含**所有**成員 (或預設成員如果**所有**成員不存在) 的每個屬性階層在 cube 中。 Tuple 內的成員順序是根據 Cube 內定義的屬性階層順序來排序。  
  
 如果指定維度名稱，則**根**函式會傳回 tuple，其中包含**所有**成員 (或預設成員如果**所有**成員不存在) 的每個屬性階層中指定之維度的目前成員內容為基礎。 Tuple 內的成員順序是根據維度內定義的屬性階層順序來排序。  
  
> [!NOTE]  
>  如果指定階層名稱，則**Tuple**函式將會挑選維度名稱，從指定的階層名稱。  
  
 如果指定了 tuple 運算式，**根**函式會傳回 tuple，其中包含指定之 tuple 的交集，**所有**未明確指定 tuple 中包含所有其他維度屬性的成員。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 tuple 包含**所有**成員 (預設值或如果**所有**成員不存在) 從 Adventure Works cube 中每個階層。  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會傳回 tuple 包含**所有**成員 (預設值或如果**所有**成員不存在) 與這些預設成員交集之 Measures 維度的指定成員值和 Adventure Works cube 中 Date 維度中每個階層。  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 下列範例會傳回包含指定的 tuple 成員的 tuple (2001 年 7 月 1 日，連同**所有**成員 (預設值或如果**所有**成員不存在) 中每個非指定階層的日期維度與這些成員交集之 Measures 維度的指定成員的 Adventure Works cube 和值。  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
