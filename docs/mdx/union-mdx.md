---
title: 聯集（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 170e3764795e1bb6db3fc9589ecf1fe486078633
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097306"
---
# <a name="union--mdx"></a>聯集（MDX）


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
  
 *設定運算式2*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 此函數會傳回兩個或多個指定集合的聯集。 使用標準語法和替代語法1時，預設會刪除重複專案。 透過標準語法，使用**ALL**旗標會在聯結的集合中保留重複的專案。 從集合結尾刪除重複項。 使用替代語法 2 時，一律會保留重複項。  
  
## <a name="examples"></a>範例  
 下列範例會使用每個語法來示範**Union**函數的行為。  
  
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
  
  
