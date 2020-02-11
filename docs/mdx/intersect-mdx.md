---
title: Intersect （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f253dad526c509edff5c837b61ae2faae07d5758
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68105362"
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
  
 選擇性的**ALL**旗標會保留重複的專案。 如果指定**ALL** ， **Intersect**函式會如往常地與 nonduplicated 專案相交，同時也會交集第一個集合中的每個重複專案，後者在第二個集合中具有相符的重複專案。 這兩個指定的集合必須具有相同的維度性。  
  
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
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
