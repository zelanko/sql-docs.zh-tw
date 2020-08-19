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
ms.openlocfilehash: 13353013575db87f5ec30ceb8cf4a5aab6a06079
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443120"
---
# <a name="originalvalue-property-ado"></a>OriginalValue 屬性 (ADO)
表示在進行任何變更之前，存在於記錄中的 [域](../../../ado/reference/ado-api/field-object.md) 值。  
  
## <a name="return-value"></a>傳回值  
 傳回 **Variant** 值，表示在任何變更之前的域值。  
  
## <a name="remarks"></a>備註  
 使用 **OriginalValue** 屬性，即可從目前的記錄傳回欄位的原始域值。  
  
 在 *立即更新模式* 中 (當您呼叫 [update](../../../ado/reference/ado-api/update-method.md) 方法) 之後，提供者會將變更寫入基礎資料來源， **OriginalValue** 屬性會傳回任何變更之前存在的域值 (也就是自上次 **update** 方法呼叫) 為止。 這與 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 方法用來取代 [value](../../../ado/reference/ado-api/value-property-ado.md) 屬性的值相同。  
  
 在 *批次更新模式* (中，提供者會快取多個變更，並且只有當您) 呼叫 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 方法時，才會將這些變更寫入基礎資料來源， **OriginalValue** 屬性會傳回任何變更之前存在的域值， (也就是自上次的 **UpdateBatch** 方法呼叫) 。 這與 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 方法用來取代 **value** 屬性的值相同。 當您搭配 [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) 屬性使用這個屬性時，您可以解決批次更新所引發的衝突。  
  
## <a name="record"></a>Record  
 對於[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件，在呼叫[Update](../../../ado/reference/ado-api/update-method.md)之前加入的欄位， **OriginalValue**屬性會是空的。  
  
## <a name="applies-to"></a>套用至  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [OriginalValue 和 UnderlyingValue 屬性範例 (VB) ](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 和 UnderlyingValue 屬性範例 (VC + +) ](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [UnderlyingValue 屬性](../../../ado/reference/ado-api/underlyingvalue-property.md)
