---
title: 同輩（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9d8ba2dd26575ebd41f4a6c275a2668b1421dee6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036953"
---
# <a name="siblings-mdx"></a>Siblings (MDX)


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
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
