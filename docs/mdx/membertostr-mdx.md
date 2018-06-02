---
title: MemberToStr (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ac9998edcf11477a2a4aff1af951d2dc4a17cbbb
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581570"
---
# <a name="membertostr-mdx"></a>MemberToStr (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回多維度運算式 (MDX)–對應至指定成員的格式化字串。  
  
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
 下列範例會傳回 [Geography].[Geography].[Country].&[United States] 字串：  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
