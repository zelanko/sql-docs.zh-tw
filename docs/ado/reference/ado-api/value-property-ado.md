---
description: Value 屬性 (ADO)
title: " (ADO) 的 Value 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ab44fcbb8409cd866167d4fb58bebc1de906274
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776967"
---
# <a name="value-property-ado"></a>Value 屬性 (ADO)

表示指派給 [欄位](./field-object.md)、 [參數](./parameter-object.md)或 [屬性](./property-object-ado.md) 物件的值。
  
## <a name="settings-and-return-values"></a>設定和傳回值

設定或傳回 **Variant** 值，指出物件的值。 預設值取決於 [Type](./type-property-ado.md) 屬性。
  
## <a name="remarks"></a>備註

您可以使用 **Value** 屬性來設定或傳回 **欄位** 物件中的資料、使用 **參數** 物件來設定或傳回參數值，或是使用 **屬性** 物件來設定或傳回屬性設定。 **Value**屬性是否為讀取/寫入或唯讀，取決於許多因素。 如需詳細資訊，請參閱個別的物件主題。

ADO 允許使用 **Value** 屬性來設定和傳回長二進位資料。
  
> [!NOTE]
> 針對 **參數** 物件，ADO 只會從提供者讀取 **值** 屬性一次。 如果命令包含的 **參數** 的 **Value** 屬性是空的，而且您從命令建立 [記錄集](./recordset-object-ado.md) ，請確定先關閉 **記錄集** ，然後再抓取 **value** 屬性。 否則，對於某些提供者， **Value** 屬性可能是空的，而且不會包含正確的值。
> 
> 針對附加至[Record](./record-object-ado.md)物件之[Fields](./fields-collection-ado.md)集合的新**欄位**物件，必須先設定**Value**屬性，才能指定任何其他**欄位**屬性。 首先，必須已指派**value**屬性的特定值，並在呼叫的**Fields**集合上[更新](./update-method.md)。 然後，可以存取其他屬性，例如 [類型](./type-property-ado.md) 或 [屬性](./attributes-property-ado.md) 。
  
## <a name="applies-to"></a>套用至

:::row:::
    :::column:::
        [Field 物件](./field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter 物件](./parameter-object.md)  
    :::column-end:::
    :::column:::
        [Property 物件 (ADO)](./property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱

[值屬性範例 (VB) ](./value-property-example-vb.md) 
[值屬性範例 (VC + +) ](./value-property-example-vc.md)