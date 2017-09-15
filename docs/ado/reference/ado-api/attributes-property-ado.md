---
title: "屬性的屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::Attributes
- Field20::Attributes
- _Parameter::Attributes
helpviewer_keywords:
- Attributes property [ADO]
ms.assetid: acc15d40-68a6-4ba9-85bd-12d331aecaa6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bffe5215cbb93e24f6914d6d56a349c9d35f6b7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="attributes-property-ado"></a>屬性的內容 (ADO)
表示物件的一或多個特性。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**長**值。  
  
 如[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件**屬性**屬性是讀取/寫入，且其值可以是一或多個總和[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)值。 預設為零 (0)。  
  
 如[參數](../../../ado/reference/ado-api/parameter-object.md)物件**屬性**屬性是讀取/寫入，且其值可以是任何一或多個總和[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)值。 預設值是**adParamSigned**。  
  
 如[欄位](../../../ado/reference/ado-api/field-object.md)物件**屬性**屬性可以是一或多個總和[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)值。 它是通常是唯讀。 不過，對於新**欄位**已附加至的物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)，**屬性**是只讀取/寫入之後[值](../../../ado/reference/ado-api/value-property-ado.md)屬性**欄位**已指定與新**欄位**已成功加入的資料提供者藉由呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法**欄位**集合。  
  
 如[屬性](../../../ado/reference/ado-api/property-object-ado.md)物件**屬性**屬性是唯讀的且其值可以是任何一或多個總和[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)值。  
  
## <a name="remarks"></a>備註  
 使用**屬性**屬性來設定或傳回特性**連接**物件**參數**物件**欄位**物件，或**屬性**物件。  
  
 當您設定多個屬性時，您可以加總的適當常數。 如果您設定的屬性值總和，包括不相容的常數時，就會發生錯誤。  
  
> [!NOTE]
>  **遠端資料服務使用量**這個屬性並不適用於用戶端**連接**物件。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Field 物件](../../../ado/reference/ado-api/field-object.md)|  
|[參數物件](../../../ado/reference/ado-api/parameter-object.md)|[屬性物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [屬性和名稱屬性範例 (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [屬性和名稱屬性的範例 （VC + +）](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [AppendChunk 方法 (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [BeginTrans、 CommitTrans 和 RollbackTrans 方法 (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [GetChunk 方法 (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)

