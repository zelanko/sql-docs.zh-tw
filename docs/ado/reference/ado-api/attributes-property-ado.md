---
description: Attributes 屬性 (ADO)
title: 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Attributes
- Field20::Attributes
- _Parameter::Attributes
helpviewer_keywords:
- Attributes property [ADO]
ms.assetid: acc15d40-68a6-4ba9-85bd-12d331aecaa6
author: rothja
ms.author: jroth
ms.openlocfilehash: 43f374429d38cb4d3cb4516d640b6d05ef8e3efb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451200"
---
# <a name="attributes-property-ado"></a>Attributes 屬性 (ADO)
表示物件的一或多個特性。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **Long** 值。  
  
 若是 [連接](../../../ado/reference/ado-api/connection-object-ado.md) 物件，[ **屬性** ] 屬性為 [讀取/寫入]，而其值可以是一個或多個 [XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md) 值的總和。 預設為零 (0)。  
  
 針對 [參數](../../../ado/reference/ado-api/parameter-object.md) 物件， **屬性** （attribute）屬性（attribute）是讀取/寫入，而其值可以是任何一或多個 [ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md) 值的總和。 預設值為 **adParamSigned**。  
  
 若為 [Field](../../../ado/reference/ado-api/field-object.md) 物件， **屬性** （attribute）屬性（attribute）可以是一或多個 [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) 值的總和。 它通常是唯讀的。 不過，對於已附加至[記錄](../../../ado/reference/ado-api/record-object-ado.md)之[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合的新**欄位**物件，只有在指定**欄位**的[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性，並藉由呼叫**Fields**集合的[Update](../../../ado/reference/ado-api/update-method.md)方法，讓資料提供者成功加入新**欄位**之後，才會讀取/寫入**屬性**。  
  
 針對 [屬性](../../../ado/reference/ado-api/property-object-ado.md) 物件，屬性（attribute **）屬性（** attribute）是唯讀的，而且其值可以是任何一或多個 [PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md) 值的總和。  
  
## <a name="remarks"></a>備註  
 您可以使用 [ **屬性** ] 屬性來設定或傳回 **連接** 物件、 **參數** 物件、 **欄位** 物件或 **屬性** 物件的特性。  
  
 當您設定多個屬性時，您可以加總適當的常數。 如果您將屬性值設定為包含不相容常數的總和，就會發生錯誤。  
  
> [!NOTE]
>  **遠端資料服務使用量** 用戶端 **連接** 物件上無法使用這個屬性。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
        [Field 物件](../../../ado/reference/ado-api/field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)  
        [Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [屬性和名稱屬性範例 (VB) ](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [屬性和名稱屬性範例 (VC + +) ](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [ (ADO) 的 AppendChunk 方法 ](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [ (ADO) 的 BeginTrans、CommitTrans 和 RollbackTrans 方法 ](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [GetChunk 方法 (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
