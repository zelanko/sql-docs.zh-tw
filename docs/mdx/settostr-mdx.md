---
title: SetToStr (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SETTOSTR
dev_langs:
- kbMDX
helpviewer_keywords:
- SetToStr function
ms.assetid: b761e002-26cd-460e-b424-fb8e306746fa
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1443875129e9376210032e3431c4f77b70b35c8c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
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
 這個函數是用來將集合的字串表示傳送至外部函數，以進行剖析。 所傳回的字串以大括號 {} 括住並以逗號分隔集合中的每個項目。  
  
## <a name="example"></a>範例  
 下列範例會傳回包含 Geography.Country 屬性階層之所有成員的字串。  
  
```  
WITH MEMBER Measures.x AS SetToStr (Geography.Geography.Children)  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
