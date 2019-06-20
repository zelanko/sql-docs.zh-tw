---
title: DefaultMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3a0c11acadcbdcadfd9398baff09db9292c87eb2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248125"
---
# <a name="defaultmember-mdx"></a>DefaultMember (MDX)


  傳回階層的預設成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Hierarchy_Expression.DefaultMember  
```  
  
## <a name="arguments"></a>引數  
 *Hierarchy_Expression*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 當查詢中並未包含屬性時，會使用屬性的預設成員來評估運算式。  
  
## <a name="example"></a>範例  
 下列範例會使用**DefaultMember**函式，搭配**名稱**函式，傳回 Adventure Works cube 中的目的地貨幣維度的預設成員。 此範例會傳回**美元**。 **名稱**函式用來傳回量值的名稱，而不是量值，也就是預設屬性**值**。  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [定義預設成員](../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  
