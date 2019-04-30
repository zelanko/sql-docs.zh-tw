---
title: NOT (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3b70068562ff24e8a1619b85fe091ab3e17da173
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278500"
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
 布林值，傳回**假**如果引數評估為 **，則為 true**，否則 **，則為 true**。  
  
## <a name="remarks"></a>備註  
 **不**運算子會將運算式視為布林值 (零 （0) 作為**false**，否則**true**) 運算子執行邏輯否定之前。 下表將說明如何**不**運算子執行邏輯否定。  
  
|*Expression1*|傳回值|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
