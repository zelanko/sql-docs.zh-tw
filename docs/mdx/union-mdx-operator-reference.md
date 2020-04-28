---
title: + 並（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cd352b95853cc5fe52857a080b6ca2e515f5c013
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097349"
---
# <a name="union---mdx-operator-reference"></a>聯集-MDX 運算子參考


  執行集合運算，傳回兩個集合的聯集、移除重複的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set_Expression + Set_Expression      
```  
  
#### <a name="parameters"></a>參數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="return-value"></a>傳回值  
 一個集合包含了兩個指定集合的成員。  
  
## <a name="remarks"></a>備註  
 **+ （聯集）** 運算子的功能等同于[&#40;MDX&#41;](../mdx/union-mdx.md)函數的聯集。  
  
## <a name="examples"></a>範例  
 以下範例示範此運算子的用法。  
  
```  
-- This member returns the gross profit margin for each year for North American countries.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members ON 0,  
    {[Sales Territory].[Sales Territory].[Country].[United States]} +  
     {[Sales Territory].[Sales Territory].[Country].[Canada]} ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
