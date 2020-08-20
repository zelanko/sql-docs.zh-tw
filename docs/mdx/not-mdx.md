---
description: NOT (MDX)
title: 不 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6c0cfa43896457397f2e2e08bac0b3de1d61e73f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471780"
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
 如果引數評估為**true**，則傳回**false**的布林值;否則**為 true**。  
  
## <a name="remarks"></a>備註  
 **NOT 運算子會**將運算式視為布林值 (零、0、為**false**;否則，在運算子執行邏輯否定之前，) **true** 。 下表說明 **NOT** 運算子如何執行邏輯否定。  
  
|*Expression1*|傳回值|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
