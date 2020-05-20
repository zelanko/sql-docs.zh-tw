---
title: Type 屬性（ADO） |Microsoft Docs
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
ms.openlocfilehash: 46718126ede409caa749b3a49dfaaffe118afc77
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761826"
---
# <a name="type-property-ado"></a>Type 屬性 (ADO)
表示[參數](../../../ado/reference/ado-api/parameter-object.md)、[欄位](../../../ado/reference/ado-api/field-object.md)或[屬性](../../../ado/reference/ado-api/property-object-ado.md)物件的操作類型或資料類型。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值。  
  
## <a name="remarks"></a>備註  
 針對**參數**物件，**類型**屬性為讀取/寫入。 對於已附加至[記錄](../../../ado/reference/ado-api/record-object-ado.md)之[Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合的新**欄位**物件，只有在指定**欄位**的[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性，且資料提供者已藉由呼叫**Fields**集合的[Update](../../../ado/reference/ado-api/update-method.md)方法來成功加入新**欄位**之後，**類型**才為讀取/寫入。  
  
 對於其他所有物件，**類型**屬性是唯讀的。  
  
## <a name="applies-to"></a>套用至  
  
||||  
|-|-|-|  
|[Field 物件](../../../ado/reference/ado-api/field-object.md)|[Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)|[Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Type 屬性範例（Field）（VB）](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [Type 屬性範例（Property）（VC + +）](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [RecordType 屬性（ADO）](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 屬性 (ADO Stream)](../../../ado/reference/ado-api/type-property-ado-stream.md)
