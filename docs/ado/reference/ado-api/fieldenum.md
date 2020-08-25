---
description: FieldEnum
title: FieldEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
author: rothja
ms.author: jroth
ms.openlocfilehash: cad540a13fbad480f795049df0d0150188df4283
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775447"
---
# <a name="fieldenum"></a>FieldEnum
指定 [記錄](./record-object-ado.md) 物件的 [fields](./fields-collection-ado.md) 集合中參考的特殊欄位。  
  
## <a name="remarks"></a>備註  
 這些常數會提供「快捷方式」來存取與 **記錄**相關聯的特殊欄位。 從**Fields**集合取出[field](./field-object.md)物件，然後使用**Field**物件的[Value](./value-property-ado.md)屬性取得其內容。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|參考包含與**記錄**相關聯之預設[資料流程](./stream-object-ado.md)物件的欄位。|  
|**adRecordURL**|-2|參考包含目前 **記錄**之絕對 URL 字串的欄位。|