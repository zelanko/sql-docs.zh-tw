---
description: Intersect (MDX)
title: Intersect (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9216b334caf67191e231c3ec0389da3fb7493b24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471840"
---
# <a name="intersect-mdx"></a>Intersect (MDX)


  傳回兩個輸入集合的交叉部分，選擇性保留重複部分。  
  
## <a name="syntax"></a>語法  
  
```  
  
Intersect(Set_Expression1 , Set_Expression2 [ , ALL ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression1*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Set_Expression2*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **Intersect**函數會傳回兩個集合的交集。 根據預設，交叉兩個集合之前，此函數會將兩個集合內的重複項移除。 這兩個指定的集合必須具有相同的維度性。  
  
 選擇性的 **ALL** 旗標會保留重複專案。 如果指定 **ALL** ， **Intersect** 函式會像往常一樣交集 nonduplicated 元素，而且也會與第一個集合中的每個重複專案交集，而第二個集合中有相符的重複專案。 這兩個指定的集合必須具有相同的維度性。  
  
## <a name="example"></a>範例  
 下列查詢會傳回同時出現在指定的兩個集合中的成員，即 2003 和 2004 年這兩項：  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001], [Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003]}`  
  
 `, {[Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 下列查詢將會失敗，因為指定的兩個集合包含來自不同階層的成員：  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001]}`  
  
 `, {[Customer].[City].&[Abingdon]&[ENG]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
