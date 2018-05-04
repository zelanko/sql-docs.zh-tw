---
title: FieldEnum |Microsoft 文件
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
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6caaf8db2b8f2e19060f6e9766bb3650ac9b5400
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="fieldenum"></a>FieldEnum
指定特殊欄位中參考[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件的[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合。  
  
## <a name="remarks"></a>備註  
 這些常數會提供存取相關聯的特殊欄位的 「 捷徑 」**記錄**。 擷取[欄位](../../../ado/reference/ado-api/field-object.md)物件從**欄位**集合，然後取得其內容與**欄位**物件的[值](../../../ado/reference/ado-api/value-property-ado.md)屬性。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|參考這個欄位包含預設[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件相關聯**記錄**。|  
|**adRecordURL**|-2|參考包含在目前的絕對 URL 字串欄位**記錄**。|
