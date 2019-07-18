---
title: Members （字串） (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 05df2d0a846af30d46e702c1d5489945d57c9115
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001499"
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
 **Members （字串）** 函式會傳回其名稱指定的單一成員。 一般而言，您可以使用**Members （字串）** 函數搭配外部函數，提供給**Members （字串）** 函式識別成員的字串和**Members （字串）** 函式會在該指定成員的傳回值。  
  
## <a name="example"></a>範例  
 下列範例會使用**Members （字串）** 函式，將指定的字串轉換成有效的成員，並接著會傳回字串中指定成員的預設量值。 指定的字串前後要加上單引號。 預設量值是「轉售商銷售數量」量值。  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
