---
title: XOR （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1657d9e58a0ae729a67e179602cd9a886ae923b1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125794"
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
 布林值，如果只有一個引數評估為**true**，則傳回**true** ;否則**為 false**。  
  
## <a name="remarks"></a>備註  
 **XOR**運算子會在運算子執行邏輯排除之前，將兩個參數視為布林值（零、0、為**false**，否則為**true**）。 下表說明**XOR**運算子如何執行邏輯排除。  
  
|*Expression1*|*Expression2*|傳回值|  
|-------------------|-------------------|------------------|  
|**真正**|**真正**|**false**|  
|**真正**|**false**|**真正**|  
|**false**|**真正**|**真正**|  
|**false**|**false**|**false**|  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
