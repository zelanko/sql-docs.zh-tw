---
title: DefaultMember （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a0b5039ae62eac25d698442d4aeb92ad3c4ebc3a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68892904"
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
 下列範例會使用**DefaultMember**函式搭配**Name**函式，以傳回「艾德作品」 cube 中目的地貨幣維度的預設成員。 此範例會傳回**US 美元**。 **Name**函數是用來傳回量值的名稱，而不是量值的預設屬性，也就是**value**。  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [定義預設成員](https://docs.microsoft.com/analysis-services/multidimensional-models/attribute-properties-define-a-default-member)  
  
  
