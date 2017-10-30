---
title: "是 (MDX) |Microsoft 文件"
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
- IS
dev_langs:
- kbMDX
helpviewer_keywords:
- IS operator
ms.assetid: dc8c0b91-3bb1-49e5-8d70-57545baaa8e0
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 97183b67350b6d3db613bb8bc8e957642bf5bb76
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="is-mdx"></a>IS (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在兩個物件運算式上執行邏輯比較。  
  
## <a name="syntax"></a>語法  
  
```  
  
Expression1 IS ( Expression2 | NULL )  
```  
  
#### <a name="parameters"></a>參數  
 *Expression1*  
 傳回 MDX 物件參考的有效多維度運算式 (MDX) 運算式。  
  
 *Expression2*  
 傳回 MDX 物件參考的有效 MDX 運算式。  
  
## <a name="return-value"></a>傳回值  
 布林值，傳回**true**如果這兩個引數都參考相同的物件; 否則**false**。 如果**NULL**指定關鍵字，則運算子會傳回**true**如果*Expression1*是**null**，否則**false**。  
  
## <a name="remarks"></a>備註  
 **IS**運算子通常用來判定 tuple 及成員是否具有等冪性，這表示它們完全相同。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用**IS**運算子來檢查軸上的目前成員是否為特定的成員：  
  
 `With`  
  
 `//Returns TRUE if the currentmember is Bikes`  
  
 `Member [Measures].[IsBikes?] AS`  
  
 `[Product].[Category].CurrentMember IS [Product].[Category].&[1]`  
  
 `SELECT`  
  
 `{[Measures].[IsBikes?]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

