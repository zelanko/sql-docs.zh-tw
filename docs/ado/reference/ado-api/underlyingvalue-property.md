---
description: UnderlyingValue 屬性
title: UnderlyingValue 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::GetUnderlyingValue
- Field20::get_UnderlyingValue
- Field20::UnderlyingValue
helpviewer_keywords:
- UnderlyingValue property
ms.assetid: 00a0c8b8-8b63-433f-95b8-020ab05874a0
author: rothja
ms.author: jroth
ms.openlocfilehash: 12788438d7db4cf51df564ea7d262bb4e7ef693d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441700"
---
# <a name="underlyingvalue-property"></a>UnderlyingValue 屬性
表示資料庫中 [Field](../../../ado/reference/ado-api/field-object.md) 物件的目前值。  
  
## <a name="return-value"></a>傳回值  
 傳回表示**欄位**值的**變異**值。  
  
## <a name="remarks"></a>備註  
 您可以使用 **UnderlyingValue** 屬性，從資料庫傳回目前的域值。 **UnderlyingValue**屬性中的域值是您的交易可見的值，而且可能是由另一筆交易最近更新的結果。 這可能與 [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) 屬性不同，這會反映原先傳回給 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的值。  
  
 這類似于使用 [Resync](../../../ado/reference/ado-api/resync-method.md) 方法，但 **UnderlyingValue** 屬性只會傳回目前記錄中特定欄位的值。 這與 [Resync](../../../ado/reference/ado-api/resync-method.md) 方法用來取代 [value](../../../ado/reference/ado-api/value-property-ado.md) 屬性的值相同。  
  
 當您搭配 **OriginalValue** 屬性使用這個屬性時，您可以解決批次更新所引發的衝突。  
  
## <a name="record"></a>Record  
 對於 [記錄](../../../ado/reference/ado-api/record-object-ado.md) 物件，在呼叫 [Update](../../../ado/reference/ado-api/update-method.md) 之前加入的欄位，這個屬性會是空的。  
  
## <a name="applies-to"></a>套用至  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [OriginalValue 和 UnderlyingValue 屬性範例 (VB) ](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 和 UnderlyingValue 屬性範例 (VC + +) ](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [ (ADO) 的 OriginalValue 屬性 ](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Resync 方法](../../../ado/reference/ado-api/resync-method.md)
