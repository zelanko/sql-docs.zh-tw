---
title: NOT （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4031b887eb0a42580d6ae8debf6c9177ff67efc3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088229"
---
# <a name="not-mdx"></a>NOT (MDX)


  在數值運算式上執行邏輯否定。  
  
## <a name="syntax"></a>語法  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>參數  
 *Expression1*  
 傳回數值的有效多維度運算式 (MDX) 運算式。  
  
## <a name="return-value"></a>傳回值  
 布林值，如果引數評估為**true**，則會傳回**false** ;否則**為 true**。  
  
## <a name="remarks"></a>備註  
 **NOT 運算子會**在運算子執行邏輯否定之前，將運算式視為布林值（零，0，為**false**; 否則為**true**）。 下表說明**NOT**運算子如何執行邏輯否定。  
  
|*Expression1*|傳回值|  
|-------------------|------------------|  
|**真正**|**false**|  
|**false**|**真正**|  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
