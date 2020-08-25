---
description: NumericScale 屬性 (ADO)
title: " (ADO) 的 NumericScale 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::NumericScale
- Field20::NumericScale
helpviewer_keywords:
- NumericScale property [ADO]
ms.assetid: 29a02992-64be-4fcd-be13-445cba205893
author: rothja
ms.author: jroth
ms.openlocfilehash: 57375b89595c6ed3e5c377692709deacd8f0ff28
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773967"
---
# <a name="numericscale-property-ado"></a>NumericScale 屬性 (ADO)
指出 [參數](./parameter-object.md) 或 [欄位](./field-object.md) 物件中數值的小數位數。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **位元組** 值，指出將解析數值的小數位數。  
  
## <a name="remarks"></a>備註  
 您可以使用 [ **NumericScale** ] 屬性來決定小數點右邊的位數將用來表示數值 **參數** 或 **欄位** 物件的值。  
  
 針對 **參數** 物件， **NumericScale** 屬性為 read/write。  
  
 若是 **Field**物件， **NumericScale** 通常是唯讀的。 不過，對於已附加至[記錄](./record-object-ado.md)之[Fields](./fields-collection-ado.md)集合的新**欄位**物件，只有在已指定**欄位**的[Value](./value-property-ado.md)屬性，而且資料提供者已透過呼叫[Fields](./fields-collection-ado.md)集合的[Update](./update-method.md)方法成功加入新**欄位**之後， **NumericScale**才會是 [讀取/寫入]。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Field 物件](./field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter 物件](./parameter-object.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [NumericScale 和 Precision 屬性範例 (VB) ](./numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 和 Precision 屬性範例 (VC + +) ](./numericscale-and-precision-properties-example-vc.md)   
 [Precision 屬性 (ADO)](./precision-property-ado.md)