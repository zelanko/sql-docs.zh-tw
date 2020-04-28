---
title: IsGeneration （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 401a11a10f190cda8efeaffa04e1025ef7f4e681
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68105229"
---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)


  傳回指定的成員是否在指定的生成集內。  
  
## <a name="syntax"></a>語法  
  
```  
  
IsGeneration(Member_Expression, Generation_Number)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Generation_Number*  
 指定用來評估指定成員之生成集的有效數值運算式。  
  
## <a name="remarks"></a>備註  
 如果指定的成員是在指定的世代編號中， **IsGeneration**函數會傳回**true** 。 否則，函數會傳回**false**。 此外，如果指定的成員評估為空的成員，則**IsGeneration**函數會傳回**false**。  
  
 為了生成集索引用途，分葉成員是生成集索引 0。 如果是非分葉成員，首先從指定成員之所有子成員的聯集，取得最高生成集索引，然後在該索引加 1，決定其生成集索引。 因為已決定非分葉成員的生成集索引，所以特定非分葉成員能夠屬於一個以上的生成集。  
  
## <a name="example"></a>範例  
 如果 [Date].[Fiscal].CurrentMember 是第二個生成集的一部分，下列範例會傳回 TRUE：  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
