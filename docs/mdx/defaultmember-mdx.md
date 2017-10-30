---
title: "DefaultMember (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DefaultMember
dev_langs:
- kbMDX
helpviewer_keywords:
- DefaultMember function
ms.assetid: c1b53b3a-6e73-4c41-a4fe-9f5c96da5463
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 738d66b3c6486c51978d3a68f5fbca73598c0382
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="defaultmember-mdx"></a>DefaultMember (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [定義預設成員](../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  

