---
title: DefaultMember (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 04c99c0882bd71d1ad56c8d4f42bf3744756c81b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580240"
---
# <a name="defaultmember-mdx"></a>DefaultMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 下列範例會使用**DefaultMember**函數搭配**名稱**函數，傳回 Adventure Works cube 中 Destination Currency 維度的預設成員。 此範例會傳回**美元**。 **名稱**函式用來傳回量值的名稱，而不是預設屬性的量值，也就是**值**。  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [定義預設成員](../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  
