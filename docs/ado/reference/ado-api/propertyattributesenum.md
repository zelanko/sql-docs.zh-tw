---
description: PropertyAttributesEnum
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
ms.openlocfilehash: 823505aae912c64c2fd7d3375b3426cb6428bcdd
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88772867"
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
指定 [屬性](./property-object-ado.md) 物件的屬性。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|指出提供者不支援此屬性。|  
|**adPropRequired**|1|指出使用者必須在初始化資料來源之前，指定這個屬性的值。|  
|**adPropOptional**|2|指出使用者在初始化資料來源之前，不需要指定這個屬性的值。|  
|**adPropRead**|512|指出使用者可以讀取屬性。|  
|**adPropWrite**|1024|指出使用者可以設定屬性。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.PropertyAttributes.NOTSUPPORTED|  
|AdoEnums. PropertyAttributes。必要|  
|AdoEnums.PropertyAttributes.OPTIONAL|  
|AdoEnums.PropertyAttributes.READ|  
|AdoEnums.PropertyAttributes.WRITE|  
  
## <a name="applies-to"></a>套用至  
 [Attributes 屬性 (ADO)](./attributes-property-ado.md)