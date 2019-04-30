---
title: Item （成員） (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 92745085a408503a2b435eb160daf431c7fdaa32
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63272836"
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
 **項目**函式會傳回指定 tuple 的成員。 函式會傳回所指定的以零為起始的位置，請參閱*Index*。  
  
## <a name="example"></a>範例  
 下列範例會傳回成員 `[2003]` - 在資料行上 `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).` Tuple 的第一個項目。  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
