---
title: IsLeaf （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 400c55cdfcea35ae60859fb66489384870172744
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905939"
---
# <a name="isleaf-mdx"></a>IsLeaf (MDX)


  傳回指定的成員是否為分葉成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
IsLeaf(Member_Expression)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果指定的成員是分葉成員，則**IsLeaf**函數會傳回**true** 。 否則，函數會傳回**false**。  
  
## <a name="example"></a>範例  
 如果 [Date].[Fiscal].CurrentMember 是分葉成員，下列範例會傳回 TRUE：  
  
 `WITH MEMBER MEASURES.ISLEAFDEMO AS`  
  
 `IsLeaf([Date].[Fiscal].CURRENTMEMBER)`  
  
 `SELECT {MEASURES.ISLEAFDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
