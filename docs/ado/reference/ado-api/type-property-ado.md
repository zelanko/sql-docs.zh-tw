---
title: 輸入屬性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02c5b9193b89c131095ccfec6ef185d5ff39f4d5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62910847"
---
# <a name="type-property-ado"></a>Type 屬性 (ADO)
表示作業的類型或資料類型的[參數](../../../ado/reference/ado-api/parameter-object.md)，[欄位](../../../ado/reference/ado-api/field-object.md)，或[屬性](../../../ado/reference/ado-api/property-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值。  
  
## <a name="remarks"></a>備註  
 針對**參數**物件，**型別**屬性是讀取/寫入。 對新**欄位**附加到的物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)，**類型**之後，才是讀取/寫入[值](../../../ado/reference/ado-api/value-property-ado.md)屬性**欄位**已指定與此資料提供者已成功地加入新**欄位**藉由呼叫[更新](../../../ado/reference/ado-api/update-method.md)的方法**欄位**集合。  
  
 對於所有其他物件，**型別**屬性是唯讀的。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Field 物件](../../../ado/reference/ado-api/field-object.md)|[Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)|[Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Type 屬性範例 (Field) (VB)](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [Type 屬性範例 (Property) （VC + +）](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [RecordType 屬性 (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 屬性 (ADO Stream)](../../../ado/reference/ado-api/type-property-ado-stream.md)
