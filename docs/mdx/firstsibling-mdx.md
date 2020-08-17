---
description: FirstSibling (MDX)
title: FirstSibling (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 265c3bce4ad873ec3c5d8ae0760455f87b1855f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387474"
---
# <a name="firstsibling-mdx"></a>FirstSibling (MDX)


  傳回成員父系的第一個子系。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.FirstSibling   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
### <a name="example"></a>範例  
 下列查詢會傳回 Fiscal 階層中 2003 會計年度的第一個同層級，也就是 Fiscal Year 2002。  
  
```  
SELECT [Date].[Fiscal].[Fiscal Year].&[2003].FirstSibling ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
