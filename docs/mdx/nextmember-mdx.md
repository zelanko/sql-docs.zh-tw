---
description: NextMember (MDX)
title: NextMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 33824ba605fc3acd0a994d0e0a6b411afdda2306
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483738"
---
# <a name="nextmember-mdx"></a>NextMember (MDX)


  傳回內含指定成員的層級中下一個成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.NextMember   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **NextMember**函式會傳回包含指定成員之相同層級中的下一個成員。  
  
## <a name="example"></a>範例  
 下列範例會傳回 August 2001 成員，做為 July 2001 成員的下一個成員。  
  
```  
SELECT [Date].[Calendar].[Month].[July 2001].NextMember ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
