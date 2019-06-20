---
title: OriginalValue 屬性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e9a576220d7771ed539765da2947f6a7cc750f64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66706923"
---
# <a name="originalvalue-property-ado"></a>OriginalValue 屬性 (ADO)
值會指出[欄位](../../../ado/reference/ado-api/field-object.md)，存在於記錄中進行任何變更之前。  
  
## <a name="return-value"></a>傳回值  
 傳回**Variant**值，表示之前的任何變更欄位的值。  
  
## <a name="remarks"></a>備註  
 使用**OriginalValue**從目前的記錄傳回欄位的原始欄位值的屬性。  
  
 在 *立即更新模式*(在其中提供者將變更寫入基礎資料來源之後，您呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法)，則**OriginalValue**屬性會傳回任何變更前存在的欄位值 (也就是自上次**更新**方法呼叫)。 這是相同值[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法會使用來取代[值](../../../ado/reference/ado-api/value-property-ado.md)屬性。  
  
 在 *批次更新模式*(提供者會快取的多項變更並將其寫入至基礎資料來源，只有當您呼叫時，才[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法)，則**OriginalValue**屬性傳回的任何變更前存在的欄位值 (也就是自上次**UpdateBatch**方法呼叫)。 這是相同值[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法會使用來取代**值**屬性。 當您使用此屬性與[UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)屬性，您可以解決衝突所引發的批次更新。  
  
## <a name="record"></a>記錄  
 針對[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件， **OriginalValue**屬性會是空的欄位前面加上[Update](../../../ado/reference/ado-api/update-method.md)呼叫。  
  
## <a name="applies-to"></a>適用於  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [OriginalValue 和 UnderlyingValue 屬性範例 (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 和 UnderlyingValue 屬性範例 （VC + +）](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [UnderlyingValue 屬性](../../../ado/reference/ado-api/underlyingvalue-property.md)
