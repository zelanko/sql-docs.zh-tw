---
title: XOR (MDX) |Microsoft 文件
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f9115fc1e226e05c788206706d59a5435bfd1c5d
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743847"
---
# <a name="xor-mdx"></a>XOR (MDX)


  在兩個數值運算式上執行邏輯排除。  
  
## <a name="syntax"></a>語法  
  
```  
  
Expression1 XOR Expression2  
  
```  
  
#### <a name="parameters"></a>參數  
 *Expression1*  
 傳回數值的有效多維度運算式 (MDX) 運算式。  
  
 *Expression2*  
 傳回數值的有效 MDX 運算式。  
  
## <a name="return-value"></a>傳回值  
 布林值，傳回**true**如果只有一個引數評估為**true**，否則**false**。  
  
## <a name="remarks"></a>備註  
 **XOR**運算子會將這兩個參數視為布林值 (零 （0) 做為**false**，否則**true**) 運算子執行邏輯排除之前。 下表將說明如何**XOR**運算子執行邏輯排除。  
  
|*Expression1*|*Expression2*|傳回值|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**false**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
