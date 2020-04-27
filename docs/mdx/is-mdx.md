---
title: IS （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aaf4151d8291ccd4249892c6ef8fce8a3d280f6b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905987"
---
# <a name="is-mdx"></a>IS (MDX)


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
 布林值，如果兩個引數都參考相同的物件，則傳回**true** ;否則**為 false**。 如果指定了**Null**關鍵字，則如果*運算式*1 為**null**，則運算子會傳回**true** ;否則**為 false**。  
  
## <a name="remarks"></a>備註  
 **Is**運算子通常用來判斷元組和成員是否為等冪，這表示它們是完全相同的。  
  
## <a name="examples"></a>範例  
 下列範例顯示如何使用**IS**運算子來檢查軸上的目前成員是否為特定成員：  
  
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
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
