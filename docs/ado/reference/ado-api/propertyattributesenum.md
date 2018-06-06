---
title: PropertyAttributesEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PropertyAttributesEnum
helpviewer_keywords:
- PropertyAttributesEnum enumeration [ADO]
ms.assetid: 96a01955-a6b4-4cbf-9c73-52bcd1e9fb25
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db96074b46b31a826d8abc22da15f66d2af3a52f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
指定的屬性[屬性](../../../ado/reference/ado-api/property-object-ado.md)物件。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|指出提供者不支援屬性。|  
|**adPropRequired**|1|表示使用者在初始化資料來源之前，必須指定此屬性的值。|  
|**adPropOptional**|2|表示使用者不需要初始化資料來源之前，請指定此屬性的值。|  
|**adPropRead**|512|表示使用者可以讀取屬性。|  
|**adPropWrite**|1024|表示使用者可以設定屬性。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.PropertyAttributes.NOTSUPPORTED|  
|AdoEnums.PropertyAttributes.REQUIRED|  
|AdoEnums.PropertyAttributes.OPTIONAL|  
|AdoEnums.PropertyAttributes.READ|  
|AdoEnums.PropertyAttributes.WRITE|  
  
## <a name="applies-to"></a>適用於  
 [Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
