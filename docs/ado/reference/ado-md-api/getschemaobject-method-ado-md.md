---
title: "GetSchemaObject 方法 (ADO MD) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords:
- GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01142e27e03cd85dcdd59e92737ee46a3bb4cf09
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="getschemaobject-method-ado-md"></a>GetSchemaObject 方法 (ADO MD)
擷取的 ADO MD 結構描述物件 ([維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)，[階層](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)，[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)，或[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)) 由其[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>語法  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>參數  
 *ObjType*  
 A [SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md)指定何種結構描述物件 （維度、 階層、 層級或成員） 擷取的值。  
  
 *UniqueName*  
 A**字串**指定**UniqueName**要擷取之物件的屬性值。  
  
## <a name="remarks"></a>備註  
 **GetSchemaObject**擷取其唯一的名稱，使用所指定的物件**UniqueName**屬性。 父物件的名稱不需要為已知，而且不需要父集合擷取結構描述物件填入。  
  
## <a name="applies-to"></a>適用於  
 [CubeDef 物件 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 物件 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
