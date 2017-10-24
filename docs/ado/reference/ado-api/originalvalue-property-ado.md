---
title: "OriginalValue 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::OriginalValue
helpviewer_keywords:
- OriginalValue property [ADO]
ms.assetid: 6e33c6ec-14d9-4b1d-ba9b-cb99862e7bac
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 018f07a06e96f9284d0a8e63742a5abebca925e1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="originalvalue-property-ado"></a>OriginalValue 屬性 (ADO)
值會指出[欄位](../../../ado/reference/ado-api/field-object.md)，存在於記錄中進行任何變更之前。  
  
## <a name="return-value"></a>傳回值  
 傳回**Variant**值，表示之前的任何變更欄位的值。  
  
## <a name="remarks"></a>備註  
 使用**OriginalValue**屬性，以傳回與目前記錄的原始欄位值的欄位。  
  
 在*立即更新模式*(在其中提供者將變更寫入基礎資料來源之後，您呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法)，則**OriginalValue**屬性會傳回任何變更前存在的欄位值 (也就是從上次**更新**方法呼叫)。 這是相同值， [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法會使用取代[值](../../../ado/reference/ado-api/value-property-ado.md)屬性。  
  
 在*批次更新模式*(其中提供者會快取多個變更，並將它們寫入基礎資料來源，只有當您呼叫[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法)，則**OriginalValue**屬性會傳回任何變更前存在的欄位值 (也就是從上次**UpdateBatch**方法呼叫)。 這是相同值， [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法會使用取代**值**屬性。 當您使用這個屬性與[UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)屬性，您可以解決所發生的批次更新衝突。  
  
## <a name="record"></a>記錄  
 如[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件**OriginalValue**屬性會是空的欄位前面加上[更新](../../../ado/reference/ado-api/update-method.md)呼叫。  
  
## <a name="applies-to"></a>適用於  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [OriginalValue 和 UnderlyingValue 屬性範例 (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 和 UnderlyingValue 屬性範例 （VC + +）](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [UnderlyingValue 屬性](../../../ado/reference/ado-api/underlyingvalue-property.md)

