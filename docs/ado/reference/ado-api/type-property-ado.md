---
description: Type 屬性 (ADO)
title: Type 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Type
- Field20::Type
helpviewer_keywords:
- Type property [ADO]
ms.assetid: 8a4c079f-9f4f-4545-801d-85983b8db71e
author: rothja
ms.author: jroth
ms.openlocfilehash: de97e62a8152e7d14d1442cc1da9b5138ddc39fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441740"
---
# <a name="type-property-ado"></a>Type 屬性 (ADO)
指出 [參數](../../../ado/reference/ado-api/parameter-object.md)、 [欄位](../../../ado/reference/ado-api/field-object.md)或 [屬性](../../../ado/reference/ado-api/property-object-ado.md) 物件的操作類型或資料類型。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 值。  
  
## <a name="remarks"></a>備註  
 針對 **參數** 物件， **Type** 屬性為 read/write。 針對附加至[記錄](../../../ado/reference/ado-api/record-object-ado.md)之[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合的新**欄位**物件，只有在已指定**欄位**的[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性，而且資料提供者已透過呼叫**Fields**集合的[Update](../../../ado/reference/ado-api/update-method.md)方法成功加入新**欄位**之後，才可讀取/寫入**型**別。  
  
 對於所有其他物件而言， **Type** 屬性是唯讀的。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Field 物件](../../../ado/reference/ado-api/field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)  
    :::column-end:::
    :::column:::
        [Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [Type 屬性範例 (欄位)  (VB) ](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [Type 屬性範例 (屬性)  (VC + +) ](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [ (ADO) 的 RecordType 屬性 ](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 屬性 (ADO Stream)](../../../ado/reference/ado-api/type-property-ado-stream.md)
