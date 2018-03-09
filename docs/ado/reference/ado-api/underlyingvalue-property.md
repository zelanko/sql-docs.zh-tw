---
title: "UnderlyingValue 屬性 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::GetUnderlyingValue
- Field20::get_UnderlyingValue
- Field20::UnderlyingValue
helpviewer_keywords:
- UnderlyingValue property
ms.assetid: 00a0c8b8-8b63-433f-95b8-020ab05874a0
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 739852d4cbfa4aaf2cf45a59b81b60e23617597f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="underlyingvalue-property"></a>UnderlyingValue 屬性
指出目前的值[欄位](../../../ado/reference/ado-api/field-object.md)資料庫中的物件。  
  
## <a name="return-value"></a>傳回值  
 傳回**Variant**值，指出值**欄位**。  
  
## <a name="remarks"></a>備註  
 使用**UnderlyingValue**屬性，以從資料庫傳回目前的欄位值。 中的欄位值**UnderlyingValue**屬性是值，都可以看到您的交易，而且可能是新的更新由另一個交易的結果。 這可能會有所不同[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)屬性，會反映原始回到值[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
 這是類似於使用[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法，但**UnderlyingValue**屬性會傳回針對特定欄位的值與目前記錄。 這是相同值，[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法會使用取代[值](../../../ado/reference/ado-api/value-property-ado.md)屬性。  
  
 當您使用這個屬性與**OriginalValue**屬性，您可以解決所發生的批次更新衝突。  
  
## <a name="record"></a>記錄  
 如[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件，這個屬性會是空的欄位前面加上[更新](../../../ado/reference/ado-api/update-method.md)呼叫。  
  
## <a name="applies-to"></a>適用於  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [OriginalValue 和 UnderlyingValue 屬性範例 (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 和 UnderlyingValue 屬性範例 （VC + +）](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [OriginalValue 屬性 (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Resync 方法](../../../ado/reference/ado-api/resync-method.md)
