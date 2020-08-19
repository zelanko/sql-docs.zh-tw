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
ms.openlocfilehash: 719a647f42c66e73b9bd55ed0a7476dfb95934e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441590"
---
# <a name="value-property-ado"></a>Value 屬性 (ADO)

表示指派給 [欄位](../../../ado/reference/ado-api/field-object.md)、 [參數](../../../ado/reference/ado-api/parameter-object.md)或 [屬性](../../../ado/reference/ado-api/property-object-ado.md) 物件的值。
  
## <a name="settings-and-return-values"></a>設定和傳回值

設定或傳回 **Variant** 值，指出物件的值。 預設值取決於 [Type](../../../ado/reference/ado-api/type-property-ado.md) 屬性。
  
## <a name="remarks"></a>備註

您可以使用 **Value** 屬性來設定或傳回 **欄位** 物件中的資料、使用 **參數** 物件來設定或傳回參數值，或是使用 **屬性** 物件來設定或傳回屬性設定。 **Value**屬性是否為讀取/寫入或唯讀，取決於許多因素。 如需詳細資訊，請參閱個別的物件主題。

ADO 允許使用 **Value** 屬性來設定和傳回長二進位資料。
  
> [!NOTE]
> 針對 **參數** 物件，ADO 只會從提供者讀取 **值** 屬性一次。 如果命令包含的 **參數** 的 **Value** 屬性是空的，而且您從命令建立 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) ，請確定先關閉 **記錄集** ，然後再抓取 **value** 屬性。 否則，對於某些提供者， **Value** 屬性可能是空的，而且不會包含正確的值。
> 
> 針對附加至[Record](../../../ado/reference/ado-api/record-object-ado.md)物件之[Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合的新**欄位**物件，必須先設定**Value**屬性，才能指定任何其他**欄位**屬性。 首先，必須已指派**value**屬性的特定值，並在呼叫的**Fields**集合上[更新](../../../ado/reference/ado-api/update-method.md)。 然後，可以存取其他屬性，例如 [類型](../../../ado/reference/ado-api/type-property-ado.md) 或 [屬性](../../../ado/reference/ado-api/attributes-property-ado.md) 。
  
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

[值屬性範例 (VB) ](../../../ado/reference/ado-api/value-property-example-vb.md) 
[值屬性範例 (VC + +) ](../../../ado/reference/ado-api/value-property-example-vc.md) 
