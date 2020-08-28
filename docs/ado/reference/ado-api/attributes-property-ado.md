---
description: Attributes 屬性 (ADO)
title: 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: ceb141b0ecdbc278e324f19f3bd4b3d7ed1b4eb6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975939"
---
# <a name="attributes-property-ado"></a>Attributes 屬性 (ADO)
表示物件的一或多個特性。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **Long** 值。  
  
 若是 [連接](./connection-object-ado.md) 物件，[ **屬性** ] 屬性為 [讀取/寫入]，而其值可以是一個或多個 [XactAttributeEnum](./xactattributeenum.md) 值的總和。 預設為零 (0)。  
  
 針對 [參數](./parameter-object.md) 物件， **屬性** （attribute）屬性（attribute）是讀取/寫入，而其值可以是任何一或多個 [ParameterAttributesEnum](./parameterattributesenum.md) 值的總和。 預設值為 **adParamSigned**。  
  
 若為 [Field](./field-object.md) 物件， **屬性** （attribute）屬性（attribute）可以是一或多個 [FieldAttributeEnum](./fieldattributeenum.md) 值的總和。 它通常是唯讀的。 不過，對於已附加至[記錄](./record-object-ado.md)之[欄位](./fields-collection-ado.md)集合的新**欄位**物件，只有在指定**欄位**的[Value](./value-property-ado.md)屬性，並藉由呼叫**Fields**集合的[Update](./update-method.md)方法，讓資料提供者成功加入新**欄位**之後，才會讀取/寫入**屬性**。  
  
 針對 [屬性](./property-object-ado.md) 物件，屬性（attribute **）屬性（** attribute）是唯讀的，而且其值可以是任何一或多個 [PropertyAttributesEnum](./propertyattributesenum.md) 值的總和。  
  
## <a name="remarks"></a>備註  
 您可以使用 [ **屬性** ] 屬性來設定或傳回 **連接** 物件、 **參數** 物件、 **欄位** 物件或 **屬性** 物件的特性。  
  
 當您設定多個屬性時，您可以加總適當的常數。 如果您將屬性值設定為包含不相容常數的總和，就會發生錯誤。  
  
> [!NOTE]
>  **遠端資料服務使用量** 用戶端 **連接** 物件上無法使用這個屬性。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Connection 物件 (ADO)](./connection-object-ado.md)  
        [Field 物件](./field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter 物件](./parameter-object.md)  
        [Property 物件 (ADO)](./property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [屬性和名稱屬性範例 (VB) ](./attributes-and-name-properties-example-vb.md)   
 [屬性和名稱屬性範例 (VC + +) ](./attributes-and-name-properties-example-vc.md)   
 [ (ADO) 的 AppendChunk 方法 ](./appendchunk-method-ado.md)   
 [ (ADO) 的 BeginTrans、CommitTrans 和 RollbackTrans 方法 ](./begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [GetChunk 方法 (ADO)](./getchunk-method-ado.md)