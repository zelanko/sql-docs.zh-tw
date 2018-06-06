---
title: '* （交叉聯集）(MDX) |Microsoft 文件'
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 03a229dd7ab766a858967eb8c4891edadaaa6b92
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577630"
---
# <a name="crossjoin----mdx-operator-reference"></a>交叉聯結的 MDX 運算子參考
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  執行集合運算，傳回兩個集合的交叉乘積。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set_Expression * Set_Expression  
```  
  
## <a name="parameter"></a>參數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="return-value"></a>傳回值  
 包含兩個指定參數的交叉乘積的集合。  
  
## <a name="remarks"></a>備註  
 **\* (Crossjoin)** 運算子在功能上等於[Crossjoin](../mdx/crossjoin-mdx.md)函式。  
  
## <a name="examples"></a>範例  
 以下範例示範此運算子的用法。  
  
```  
-- This query returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
