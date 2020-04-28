---
title: '* 交叉（MDX） |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2f8377acec8f213c423de5d19d8859c8b3d93a06
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68047146"
---
# <a name="crossjoin----mdx-operator-reference"></a>交叉聯結-MDX 運算子參考


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
 ** \* （交叉聯結）** 運算子的功能等同于[交叉](../mdx/crossjoin-mdx.md)聯結函數。  
  
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
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
