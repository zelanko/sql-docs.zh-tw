---
title: Item （成員） (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7cb7c3825f2a319282788c222a7ebb46cec2b532
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578830"
---
# <a name="item-member-mdx"></a>Item (成員) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回一個來自指定 Tuple 的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Tuple_Expression.Item( Index )  
```  
  
## <a name="arguments"></a>引數  
 *Tuple_Expression*  
 傳回 Tuple 的有效多維度運算式 (MDX) 運算式。  
  
 *Index*  
 有效的數值運算式，會依所要傳回之 Tuple 中的位置指定特定的成員。  
  
## <a name="remarks"></a>備註  
 **項目**函式會傳回指定 tuple 成員。 函式會傳回所指定的以零為起始位置，請參閱*索引*。  
  
## <a name="example"></a>範例  
 下列範例會傳回成員 `[2003]` - 在資料行上 `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).` Tuple 的第一個項目。  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
