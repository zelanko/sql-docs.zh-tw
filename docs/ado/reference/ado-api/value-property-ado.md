---
title: Value 屬性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c7e4d42bc58321c5b650df5e8e842290094fcf4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043693"
---
# <a name="value-property-ado"></a>Value 屬性 (ADO)

指派給的值會指出[欄位](../../../ado/reference/ado-api/field-object.md)，[參數](../../../ado/reference/ado-api/parameter-object.md)，或[屬性](../../../ado/reference/ado-api/property-object-ado.md)物件。
  
## <a name="settings-and-return-values"></a>設定和傳回值

設定或傳回**Variant**值，指出物件的值。 預設值取決於[型別](../../../ado/reference/ado-api/type-property-ado.md)屬性。
  
## <a name="remarks"></a>備註

使用**值**屬性來設定或傳回資料來源**欄位**物件，來設定或傳回參數值**參數**物件，或要設定或傳回屬性設定**屬性**物件。 是否**值**屬性是可讀寫或唯讀狀態取決於許多因素。 請參閱個別的物件主題，如需詳細資訊。

設定和傳回長的二進位資料，可讓 ADO**值**屬性。
  
> [!NOTE]
> 針對**參數**物件、 ADO 讀取**值**一次從提供者的屬性。 如果命令包含**參數**其**值**屬性是空的而且您建立[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)命令，請確定先關閉**資料錄集**擷取前**值**屬性。 否則，對於某些提供者，**值**屬性可能是空的並不會包含正確的值。
> 
> 對新**欄位**附加到的物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件**值**屬性必須設定在任何其他**欄位**可以指定的屬性。 首先，為特定值如**值**必須獲指派的屬性和[更新](../../../ado/reference/ado-api/update-method.md)上**欄位**呼叫的集合。 然後，這類的其他屬性[型別](../../../ado/reference/ado-api/type-property-ado.md)或是[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)可以存取。
  
## <a name="applies-to"></a>適用於
  
||||  
|-|-|-|  
|[Field 物件](../../../ado/reference/ado-api/field-object.md)|[Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)|[Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|
  
## <a name="see-also"></a>另請參閱

[值屬性範例 (VB)](../../../ado/reference/ado-api/value-property-example-vb.md)
[值屬性範例 （VC + +）](../../../ado/reference/ado-api/value-property-example-vc.md) 
