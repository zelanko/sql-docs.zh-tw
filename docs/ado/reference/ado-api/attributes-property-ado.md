---
title: Attributes 屬性（ADO） |Microsoft Docs
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
ms.openlocfilehash: 488fe5a46b994ed664c6355e24fe8d567d5ff11d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762905"
---
# <a name="attributes-property-ado"></a>Attributes 屬性 (ADO)
表示物件的一或多個特性。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**Long**值。  
  
 若為[Connection](../../../ado/reference/ado-api/connection-object-ado.md)物件， **Attributes**屬性會是讀取/寫入，而其值可以是一或多個[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)值的總和。 預設為零 (0)。  
  
 對於[參數](../../../ado/reference/ado-api/parameter-object.md)物件，**屬性**是可讀寫的，而其值可以是任何一個或多個[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)值的總和。 預設值為**adParamSigned**。  
  
 如果是[欄位](../../../ado/reference/ado-api/field-object.md)物件， **Attributes**屬性可以是一個或多個[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)值的總和。 它通常是唯讀的。 不過，對於附加至[記錄](../../../ado/reference/ado-api/record-object-ado.md)之[Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合的新**欄位**物件，只有在指定**欄位**的[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性，而且資料提供者已藉由呼叫**Fields**集合的[Update](../../../ado/reference/ado-api/update-method.md)方法成功加入新的**欄位**之後，才會讀取/寫入**屬性**。  
  
 對於[屬性](../../../ado/reference/ado-api/property-object-ado.md)物件而言，屬性（attribute **）屬性（** attribute）是唯讀的，而且其值可以是任何一個或多個[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)值的總和。  
  
## <a name="remarks"></a>備註  
 使用 [**屬性**] 屬性可設定或傳回**連接**物件、**參數**物件、**欄位**物件或**屬性**物件的特性。  
  
 當您設定多個屬性時，可以加總適當的常數。 如果您將屬性值設定為包含不相容常數的總和，就會發生錯誤。  
  
> [!NOTE]
>  **遠端資料服務使用量**用戶端**連接**物件上無法使用這個屬性。  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Field 物件](../../../ado/reference/ado-api/field-object.md)|  
|[Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)|[Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Attributes 和 Name 屬性範例（VB）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Attributes 和 Name 屬性範例（VC + +）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [AppendChunk 方法（ADO）](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [BeginTrans、CommitTrans 和 RollbackTrans 方法（ADO）](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [GetChunk 方法 (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
