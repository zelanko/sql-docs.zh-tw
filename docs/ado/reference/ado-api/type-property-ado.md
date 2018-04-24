---
title: 型別屬性 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Type
- Field20::Type
helpviewer_keywords:
- Type property [ADO]
ms.assetid: 8a4c079f-9f4f-4545-801d-85983b8db71e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7a0557dff957b71c601acbfbe0776fe39d979856
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="type-property-ado"></a>型別屬性 (ADO)
表示作業的類型或資料類型的[參數](../../../ado/reference/ado-api/parameter-object.md)，[欄位](../../../ado/reference/ado-api/field-object.md)，或[屬性](../../../ado/reference/ado-api/property-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值。  
  
## <a name="remarks"></a>備註  
 如**參數**物件**類型**屬性是讀取/寫入。 對於新**欄位**已附加至的物件[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)，**類型**之後，才是讀取/寫入[值](../../../ado/reference/ado-api/value-property-ado.md)屬性**欄位**已指定與此資料提供者已成功地加入新**欄位**藉由呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法**欄位**集合。  
  
 所有其他物件，**類型**屬性是唯讀的。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Field 物件](../../../ado/reference/ado-api/field-object.md)|[Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)|[Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [型別屬性範例 （欄位） (VB)](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [型別屬性範例 （屬性） （VC + +）](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [RecordType 屬性 (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 屬性 (ADO Stream)](../../../ado/reference/ado-api/type-property-ado-stream.md)
