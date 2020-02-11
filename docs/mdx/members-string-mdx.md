---
title: 成員（字串）（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 05df2d0a846af30d46e702c1d5489945d57c9115
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
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
 **Members （String）** 函數會傳回其名稱已指定的單一成員。 一般來說，您會使用**members （string）** 函數搭配外部函式，並提供**成員（字串）** 函式識別成員的字串，而**members （string）** 函數會傳回這個指定成員的值。  
  
## <a name="example"></a>範例  
 下列範例會使用**Members （String）** 函數，將指定的字串轉換成有效的成員，然後傳回字串中所指定之成員的預設量值。 指定的字串前後要加上單引號。 預設量值是「轉售商銷售數量」量值。  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
