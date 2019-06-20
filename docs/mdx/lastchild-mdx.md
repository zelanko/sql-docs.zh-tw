---
title: LastChild (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 77c8d0c3f1332b222a028747619ce792915dbe87
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62797896"
---
# <a name="lastchild-mdx"></a>LastChild (MDX)


  傳回指定成員的最後一個子系。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.LastChild   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
### <a name="example"></a>範例  
 下列範例會傳回 September 2001 的值，這是 2002 會計年度第一個會計季度的最後一個子系。  
  
```  
SELECT [Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002].LastChild ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [FirstChild &#40;MDX&#41;](../mdx/firstchild-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
