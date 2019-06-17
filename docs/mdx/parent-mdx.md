---
title: 父 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 16de50e05bf139d590f90630e338fdb7cbb428e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63278430"
---
# <a name="parent-mdx"></a>Parent (MDX)


  傳回一個成員的父系。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.Parent   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **父**函式會傳回指定成員的父成員。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 July 1, 2001 成員的父系。 第一個範例在 Date 屬性階層的內容中指定這個成員，並且傳回 All Periods 成員。  
  
```  
SELECT [Date].[Date].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
 下列範例在 Calendar 階層的內容中指定 July 1, 2001 成員。  
  
```  
SELECT [Date].[Calendar].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
