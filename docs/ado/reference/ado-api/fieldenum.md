---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5fe89d90510e95468e18b0d744ff566f69654320
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932686"
---
# <a name="fieldenum"></a>FieldEnum
指定[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件的[fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合中所參考的特殊欄位。  
  
## <a name="remarks"></a>備註  
 這些常數會提供「快捷方式」來存取與**記錄**相關聯的特殊欄位。 從**Fields**集合取出[Field](../../../ado/reference/ado-api/field-object.md)物件，然後使用**Field**物件的[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性取得其內容。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|參考包含與**記錄**相關聯之預設[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件的欄位。|  
|**adRecordURL**|-2|參考包含目前**記錄**之絕對 URL 字串的欄位。|
