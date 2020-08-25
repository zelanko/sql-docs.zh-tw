---
description: OriginalValue 屬性 (ADO)
title: " (ADO) 的 OriginalValue 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::OriginalValue
helpviewer_keywords:
- OriginalValue property [ADO]
ms.assetid: 6e33c6ec-14d9-4b1d-ba9b-cb99862e7bac
author: rothja
ms.author: jroth
ms.openlocfilehash: 5aedfa688b2d29a80eb0bc2e06d113e908e122c2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773567"
---
# <a name="originalvalue-property-ado"></a>OriginalValue 屬性 (ADO)
表示在進行任何變更之前，存在於記錄中的 [域](./field-object.md) 值。  
  
## <a name="return-value"></a>傳回值  
 傳回 **Variant** 值，表示在任何變更之前的域值。  
  
## <a name="remarks"></a>備註  
 使用 **OriginalValue** 屬性，即可從目前的記錄傳回欄位的原始域值。  
  
 在 *立即更新模式* 中 (當您呼叫 [update](./update-method.md) 方法) 之後，提供者會將變更寫入基礎資料來源， **OriginalValue** 屬性會傳回任何變更之前存在的域值 (也就是自上次 **update** 方法呼叫) 為止。 這與 [CancelUpdate](./cancelupdate-method-ado.md) 方法用來取代 [value](./value-property-ado.md) 屬性的值相同。  
  
 在 *批次更新模式* (中，提供者會快取多個變更，並且只有當您) 呼叫 [UpdateBatch](./updatebatch-method.md) 方法時，才會將這些變更寫入基礎資料來源， **OriginalValue** 屬性會傳回任何變更之前存在的域值， (也就是自上次的 **UpdateBatch** 方法呼叫) 。 這與 [CancelBatch](./cancelbatch-method-ado.md) 方法用來取代 **value** 屬性的值相同。 當您搭配 [UnderlyingValue](./underlyingvalue-property.md) 屬性使用這個屬性時，您可以解決批次更新所引發的衝突。  
  
## <a name="record"></a>Record  
 對於[記錄](./record-object-ado.md)物件，在呼叫[Update](./update-method.md)之前加入的欄位， **OriginalValue**屬性會是空的。  
  
## <a name="applies-to"></a>套用至  
 [Field 物件](./field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [OriginalValue 和 UnderlyingValue 屬性範例 (VB) ](./originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 和 UnderlyingValue 屬性範例 (VC + +) ](./originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [UnderlyingValue 屬性](./underlyingvalue-property.md)