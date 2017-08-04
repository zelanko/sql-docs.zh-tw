---
title: "Intersect (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INTERSECT
dev_langs:
- kbMDX
helpviewer_keywords:
- Intersect function
ms.assetid: 0de8fbb4-e2db-480c-86f1-2abbbcfdb1d8
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 07f59caff53819cb2ccea52d7f3372a4d3b97c65
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="intersect-mdx"></a>Intersect (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 **Intersect**函式會傳回兩個集合的交集。 根據預設，交叉兩個集合之前，此函數會將兩個集合內的重複項移除。 這兩個指定的集合必須具有相同的維度性。  
  
 選擇性**所有**旗標會保留重複項。 如果**所有**指定，則**Intersect**函式如往常般相交照常項目，而且也會交叉第二個集合中有相符重複第一個集合中的每個重複項目。 這兩個指定的集合必須具有相同的維度性。  
  
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
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

