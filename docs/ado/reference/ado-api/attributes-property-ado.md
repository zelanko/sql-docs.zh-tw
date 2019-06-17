---
title: 屬性的屬性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 91425029546402edbd5bde7df45586c77e38d83b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696390"
---
# <a name="attributes-property-ado"></a>Attributes 屬性 (ADO)
表示物件的一或多個特性。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**長**值。  
  
 針對[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件，**屬性**屬性是讀取/寫入，且其值可以是一或多個總和[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)值。 預設值為零 (0)。  
  
 針對[參數](../../../ado/reference/ado-api/parameter-object.md)物件，**屬性**屬性是讀取/寫入，且其值可以是任何一個或多個總和[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)值。 預設值是**adParamSigned**。  
  
 針對[欄位](../../../ado/reference/ado-api/field-object.md)物件，**屬性**屬性可以是一或多個總和[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)值。 它是通常是唯讀。 不過，對於新**欄位**附加到的物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)，**屬性**是只讀取/寫入之後[值](../../../ado/reference/ado-api/value-property-ado.md)屬性**欄位**已指定與新**欄位**已成功加入的資料提供者藉由呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法**欄位**集合。  
  
 針對[屬性](../../../ado/reference/ado-api/property-object-ado.md)物件，**屬性**屬性是唯讀的和其值可以是任何一個或多個總和[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)值。  
  
## <a name="remarks"></a>備註  
 使用**屬性**屬性來設定或傳回的特性**連線**物件**參數**物件**欄位**物件，或**屬性**物件。  
  
 當您設定多個屬性時，您可以加總適當的常數。 如果您設定的屬性值總和，包括不相容的常數時，就會發生錯誤。  
  
> [!NOTE]
>  **遠端資料服務使用量**這個屬性並不適用於用戶端**連線**物件。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Field 物件](../../../ado/reference/ado-api/field-object.md)|  
|[Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)|[Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Attributes 和 Name 屬性範例 (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Attributes 和 Name 屬性範例 （VC + +）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [AppendChunk 方法 (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [BeginTrans、 CommitTrans 和 RollbackTrans 方法 (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [GetChunk 方法 (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
