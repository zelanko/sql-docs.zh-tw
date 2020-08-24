---
description: GetSchemaObject 方法 (ADO MD)
title: " (ADO MD) 的 GetSchemaObject 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords:
- GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
author: rothja
ms.author: jroth
ms.openlocfilehash: b0a54b02cf748d8ff1144e50e3531295dbfe8c55
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778117"
---
# <a name="getschemaobject-method-ado-md"></a>GetSchemaObject 方法 (ADO MD)
依[UniqueName](./uniquename-property-ado-md.md) ([維度](./dimension-object-ado-md.md)、階層、[層級](./level-object-ado-md.md)或[成員](./member-object-ado-md.md) [) ，抓取](./hierarchy-object-ado-md.md)ADO MD 的架構物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>參數  
 *ObjType*  
 [SchemaObjectTypeEnum](./schemaobjecttypeenum.md)值，指定要取出 (維度、階層、層級或成員) 的架構物件類型。  
  
 *UniqueName*  
 **字串**，指定要取得之物件的**UniqueName**屬性值。  
  
## <a name="remarks"></a>備註  
 **GetSchemaObject** 會使用其唯一的名稱來抓取物件，如 **UniqueName** 屬性所指定。 父物件的名稱不需要是已知的，且不需要填入父集合來取出架構物件。  
  
## <a name="applies-to"></a>套用至  
 [CubeDef 物件 (ADO MD)](./cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 物件 (ADO MD)](./cubedef-object-ado-md.md)