---
title: SetToStr (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1a6cd7d87e0eb582c06a402a98a2294996ac12c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581580"
---
# <a name="settostr-mdx"></a>SetToStr (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回對應至指定集合的多維度運算式 (MDX) 格式化字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
SetToStr(Set_Expression)  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 這個函數是用來將集合的字串表示傳送至外部函數，以進行剖析。 所傳回的字串括在大括弧{}，每個項目以逗號分隔集合中。  
  
## <a name="example"></a>範例  
 下列範例會傳回包含 Geography.Country 屬性階層之所有成員的字串。  
  
```  
WITH MEMBER Measures.x AS SetToStr (Geography.Geography.Children)  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
