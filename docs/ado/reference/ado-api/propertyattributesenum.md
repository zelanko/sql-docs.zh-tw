---
title: PropertyAttributesEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PropertyAttributesEnum
helpviewer_keywords:
- PropertyAttributesEnum enumeration [ADO]
ms.assetid: 96a01955-a6b4-4cbf-9c73-52bcd1e9fb25
author: rothja
ms.author: jroth
ms.openlocfilehash: dcb17116d7332e9afb359a7dd47d69cb3eb75df4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759934"
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
指定[屬性](../../../ado/reference/ado-api/property-object-ado.md)物件的屬性。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|表示提供者不支援此屬性。|  
|**adPropRequired**|1|表示在初始化資料來源之前，使用者必須指定此屬性的值。|  
|**adPropOptional**|2|表示在初始化資料來源之前，使用者不需要指定這個屬性的值。|  
|**adPropRead**|512|表示使用者可以讀取屬性。|  
|**adPropWrite**|1024|表示使用者可以設定屬性。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.PropertyAttributes.NOTSUPPORTED|  
|AdoEnums. PropertyAttributes. 必要|  
|AdoEnums.PropertyAttributes.OPTIONAL|  
|AdoEnums.PropertyAttributes.READ|  
|AdoEnums.PropertyAttributes.WRITE|  
  
## <a name="applies-to"></a>套用至  
 [Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
