---
description: Item (成員) (MDX)
title: 專案 (成員)  (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a374d1fcc7f972828832c2f82375acf640d45fb2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483961"
---
# <a name="item-member-mdx"></a>Item (成員) (MDX)


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
 **Item**函數會從指定的元組傳回成員。 函數會傳回在 *索引*所指定之以零為基底的位置找到的成員。  
  
## <a name="example"></a>範例  
 下列範例會傳回成員 `[2003]` - 在資料行上 `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).` Tuple 的第一個項目。  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
