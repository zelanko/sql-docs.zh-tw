---
title: MemberToStr (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ff7ffb1b57c8af38e1b2eeebc64f2a3e753fc5b3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278491"
---
# <a name="membertostr-mdx"></a>MemberToStr (MDX)


  傳回多維度運算式 (MDX） 格式化的字串，對應至指定的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
MemberToStr(Member_Expression)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 這個函數會傳回包含成員 uniquename 的字串。 它通常用來將成員 uniquename 傳遞至外部函數。  
  
## <a name="example"></a>範例  
 下列範例會傳回 [Geography] 的字串。[Geography]。[國家/地區]。 （& s) [United States]:  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
