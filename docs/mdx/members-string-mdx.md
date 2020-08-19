---
description: Members (字串) (MDX)
title: 成員 (字串)  (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 95e90f488f4b9182fc237045b570bc9da02f47e6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483821"
---
# <a name="members-string-mdx"></a>Members (字串) (MDX)


  傳回由字串運算式指定的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Members(Member_Name)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Name*  
 指定成員名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 **成員 (字串) **函數會傳回已指定名稱的單一成員。 一般而言，您會使用 ** (字串) ** 函式的成員搭配外部函式，為 **成員提供 (字串) ** 函式以識別成員的字串，而 **成員 (字串) ** 函數會傳回這個指定成員的值。  
  
## <a name="example"></a>範例  
 下列範例會使用 ** (String) ** 函數的成員將指定的字串轉換成有效的成員，然後傳回字串中所指定之成員的預設量值。 指定的字串前後要加上單引號。 預設量值是「轉售商銷售數量」量值。  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
