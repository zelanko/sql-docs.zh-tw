---
title: 同層級 (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9f292a67116fad324a3a4b2706698febc7713f59
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582220"
---
# <a name="siblings-mdx"></a>Siblings (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回成員的同層級 (Sibling)，包括成員本身。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.Siblings   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
### <a name="example"></a>範例  
 下列範例會傳回 March 2003 之同層級的預設量值，也就是 January 2003 和 February 2003，並且包括 March 2003 本身。  
  
```  
SELECT [Date].[Calendar].[Month].[March 2003].Siblings ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
