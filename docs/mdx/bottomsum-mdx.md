---
description: BottomSum (MDX)
title: BottomSum (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 51be20fdd7378b361cd8d962941e55532503e4e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494961"
---
# <a name="bottomsum-mdx"></a>BottomSum (MDX)


  以遞增的順序排序指定集合，並傳回數值最低的 Tuple 集合，此集合的總和等於或小於指定的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
BottomSum(Set_Expression, Value, Numeric_Expression)  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *值*  
 有效的數值運算式，會指定用來與每個 Tuple 比較的值。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **BottomSum**函式會計算指定之量值的總和，並針對指定的集合進行評估，並以遞增順序排序集合。 然後，函數會傳回最低值的元素，這些元素之指定數值運算式的總計至少是指定值 (sum)。 這個函數會傳回累計總計至少是指定值之集合的最小子集。 從最小至最大排序傳回的元素。  
  
> [!IMPORTANT]  
>  **BottomSum**函式（例如[TopSum](../mdx/topsum-mdx.md)函數）一律會中斷階層。  
  
## <a name="examples"></a>範例  
 下列範例會針對 Bike 類別目錄傳回 2003 會計年度 Geography 維度內 Geography 階層中 City 層級之成員的最小集合，此集合的累計總計使用 Reseller Sales Amount 量值計算至少 50,000 的總和 (從此集合中最小銷售數的成員開始)：  
  
 `SELECT`  
  
 `[Product].[Product Categories].Bikes ON 0,`  
  
 `BottomSum`  
  
 `({[Geography].[Geography].[City].Members}`  
  
 `, 50000`  
  
 `, ([Measures].[Reseller Sales Amount],[Product].[Product Categories].Bikes)`  
  
 `) ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Measures].[Reseller Sales Amount],[Date].[Fiscal].[Fiscal Year].[FY 2003])`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
