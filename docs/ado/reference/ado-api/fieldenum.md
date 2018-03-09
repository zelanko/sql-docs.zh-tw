---
title: FieldEnum | Microsoft Docs
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
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b00bf49dc7ee74c6da15b078e674af5e0472ec6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="fieldenum"></a>FieldEnum
指定特殊欄位中參考[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件的[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合。  
  
## <a name="remarks"></a>備註  
 這些常數會提供存取相關聯的特殊欄位的 「 捷徑 」**記錄**。 擷取[欄位](../../../ado/reference/ado-api/field-object.md)物件從**欄位**集合，然後取得其內容與**欄位**物件的[值](../../../ado/reference/ado-api/value-property-ado.md)屬性。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|參考這個欄位包含預設[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件相關聯**記錄**。|  
|**adRecordURL**|-2|參考包含在目前的絕對 URL 字串欄位**記錄**。|
