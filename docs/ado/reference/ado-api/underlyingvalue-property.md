---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 582d0b87edd4729ce54cc2a7323b0a63443cab82
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938851"
---
# <a name="underlyingvalue-property"></a>UnderlyingValue 屬性
表示資料庫中[Field](../../../ado/reference/ado-api/field-object.md)物件的目前值。  
  
## <a name="return-value"></a>傳回值  
 傳回表示**欄位**值的**變數**值。  
  
## <a name="remarks"></a>備註  
 使用**UnderlyingValue**屬性，從資料庫傳回目前的域值。 **UnderlyingValue**屬性中的域值是您的交易可見的值，可能是由另一筆交易的最近更新所產生的結果。 這可能與[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)屬性不同，它會反映原先傳回至[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的值。  
  
 這類似于使用[Resync](../../../ado/reference/ado-api/resync-method.md)方法，但**UnderlyingValue**屬性只會傳回目前記錄中特定欄位的值。 這是重新[同步](../../../ado/reference/ado-api/resync-method.md)處理方法用來取代[value](../../../ado/reference/ado-api/value-property-ado.md)屬性的相同值。  
  
 當您使用這個屬性搭配**OriginalValue**屬性時，您可以解決批次更新所引發的衝突。  
  
## <a name="record"></a>Record  
 針對[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件，在呼叫[Update](../../../ado/reference/ado-api/update-method.md)之前新增的欄位，此屬性會是空的。  
  
## <a name="applies-to"></a>套用至  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [OriginalValue 和 UnderlyingValue 屬性範例（VB）](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 和 UnderlyingValue 屬性範例（VC + +）](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [OriginalValue 屬性（ADO）](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Resync 方法](../../../ado/reference/ado-api/resync-method.md)
