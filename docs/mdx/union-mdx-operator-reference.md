---
description: Union-MDX 運算子參考
title: +  (聯集)  (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 84e6bc2b6b8460b90013ade5f0981af7f0ed8432
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341187"
---
# <a name="union---mdx-operator-reference"></a>Union-MDX 運算子參考


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
 **+ (聯集) **運算子在功能上相當於[Union &#40;MDX&#41;](../mdx/union-mdx.md)函數。  
  
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
  
  
