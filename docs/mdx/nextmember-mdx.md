---
title: NextMember (MDX) |Microsoft 文件
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4535b837d81db10f41f1445a7051678ce4fdd688
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742177"
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
 **NextMember**函式會傳回下一個成員的相同層級中，包含指定的成員。  
  
## <a name="example"></a>範例  
 下列範例會傳回 August 2001 成員，做為 July 2001 成員的下一個成員。  
  
```  
SELECT [Date].[Calendar].[Month].[July 2001].NextMember ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
