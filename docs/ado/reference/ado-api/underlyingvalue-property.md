---
description: UnderlyingValue 屬性
title: UnderlyingValue 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: a96924a682a0c916da8c6834ea7b290b88b6f690
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988169"
---
# <a name="underlyingvalue-property"></a>UnderlyingValue 屬性
表示資料庫中 [Field](./field-object.md) 物件的目前值。  
  
## <a name="return-value"></a>傳回值  
 傳回表示**欄位**值的**變異**值。  
  
## <a name="remarks"></a>備註  
 您可以使用 **UnderlyingValue** 屬性，從資料庫傳回目前的域值。 **UnderlyingValue**屬性中的域值是您的交易可見的值，而且可能是由另一筆交易最近更新的結果。 這可能與 [OriginalValue](./originalvalue-property-ado.md) 屬性不同，這會反映原先傳回給 [記錄集](./recordset-object-ado.md)的值。  
  
 這類似于使用 [Resync](./resync-method.md) 方法，但 **UnderlyingValue** 屬性只會傳回目前記錄中特定欄位的值。 這與 [Resync](./resync-method.md) 方法用來取代 [value](./value-property-ado.md) 屬性的值相同。  
  
 當您搭配 **OriginalValue** 屬性使用這個屬性時，您可以解決批次更新所引發的衝突。  
  
## <a name="record"></a>Record  
 對於 [記錄](./record-object-ado.md) 物件，在呼叫 [Update](./update-method.md) 之前加入的欄位，這個屬性會是空的。  
  
## <a name="applies-to"></a>套用至  
 [Field 物件](./field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [OriginalValue 和 UnderlyingValue 屬性範例 (VB) ](./originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 和 UnderlyingValue 屬性範例 (VC + +) ](./originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [ (ADO) 的 OriginalValue 屬性 ](./originalvalue-property-ado.md)   
 [Resync 方法](./resync-method.md)