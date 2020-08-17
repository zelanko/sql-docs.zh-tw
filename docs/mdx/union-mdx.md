---
description: 'Union (MDX) '
title: Union (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b0b4240d6c646761c5d962e4b9fa1ca54e0dcc0e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341204"
---
# <a name="union--mdx"></a>Union (MDX) 


  傳回兩個集合的聯集而產生的集合，可選擇性地保留重複的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Standard syntax  
Union(Set_Expression1, Set_Expression2 [,...n][, ALL])  
  
Alternate syntax 1  
Set_Expression1 + Set_Expression2 [+...n]  
  
Alternate syntax 2  
{Set_Expression1 , Set_Expression2 [,...n]}  
```  
  
## <a name="arguments"></a>引數  
 *設定運算式1*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *集合運算式2*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 此函數會傳回兩個或多個指定集合的聯集。 使用標準語法和替代語法1時，預設會刪除重複項。 使用標準語法時，使用 **ALL** 旗標會在聯結的集合中保留重複專案。 從集合結尾刪除重複項。 使用替代語法 2 時，一律會保留重複項。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用每個語法來執行 **Union** 函數的行為。  
  
### <a name="standard-syntax-duplicates-eliminated"></a>標準語法，刪除重複項  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="standard-syntax-duplicates-retained"></a>標準語法，保留重複項  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   , ALL  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-1-duplicates-eliminated"></a>替代語法 1，刪除重複項  
  
```  
SELECT   
   [Date].[Calendar Year].children   
   + {[Date].[Calendar Year].[CY 2002]}   
   + {[Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-2-duplicates-retained"></a>替代語法 2，保留重複項  
  
```  
SELECT   
   {[Date].[Calendar Year].children  
   , [Date].[Calendar Year].[CY 2002]  
   , [Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [+ &#40;聯集&#41; &#40;MDX&#41;](../mdx/union-mdx-operator-reference.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
