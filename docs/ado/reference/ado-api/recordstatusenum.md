---
title: RecordStatusEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordStatusEnum
helpviewer_keywords:
- RecordStatusEnum enumeration [ADO]
ms.assetid: 506fdd70-4452-4e83-95d5-c94311988dfa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 233b2f84b6a60c7b5162edce6c1b76b63946ae81
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931289"
---
# <a name="recordstatusenum"></a>RecordStatusEnum
指定有關批次更新和其他大量作業的記錄[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|表示未儲存記錄，因為作業已取消。|  
|**adRecCantRelease**|0x400|表示未儲存新的記錄，因為現有的記錄已鎖定。|  
|**adRecConcurrencyViolation**|0x800|表示記錄未儲存，因為開放式平行存取已在使用中。|  
|**adRecDBDeleted**|0x40000|表示已從資料來源中刪除記錄。|  
|**adRecDeleted**|0x4|表示已刪除記錄。|  
|**adRecIntegrityViolation**|0x1000|表示記錄未儲存，因為使用者違反完整性條件約束。|  
|**adRecInvalid**|0x10|表示記錄未儲存，因為它的書簽無效。|  
|**adRecMaxChangesExceeded**|0x2000|表示記錄未儲存，因為有太多暫止的變更。|  
|**adRecModified**|0x2|表示已修改記錄。|  
|**adRecMultipleChanges**|0x40|表示記錄未儲存，因為它會影響多筆記錄。|  
|**adRecNew**|0x1|表示記錄是新的。|  
|**adRecObjectOpen**|0x4000|表示記錄未儲存，因為與開啟的儲存物件發生衝突。|  
|**adRecOK**|0|表示已成功更新記錄。|  
|**adRecOutOfMemory**|0x8000|表示記錄未儲存，因為電腦的記憶體用盡。|  
|**adRecPendingChanges**|0x80|表示記錄未儲存，因為它參考了暫止的插入。|  
|**adRecPermissionDenied**|0x10000|表示記錄未儲存，因為使用者沒有足夠的許可權。|  
|**adRecSchemaViolation**|0x20000|表示記錄未儲存，因為它違反基礎資料庫的結構。|  
|**adRecUnmodified**|0x8|表示未修改記錄。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 AdoEnums.RecordStatus.  
  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. RecordStatus. 已取消|  
|AdoEnums.RecordStatus.CANTRELEASE|  
|AdoEnums. RecordStatus. CONCURRENCYVIOLATION|  
|AdoEnums.RecordStatus.DBDELETED|  
|AdoEnums. RecordStatus. 已刪除|  
|AdoEnums.RecordStatus.INTEGRITYVIOLATION|  
|AdoEnums. RecordStatus 無效|  
|AdoEnums.RecordStatus.MAXCHANGESEXCEEDED|  
|AdoEnums. RecordStatus. 已修改|  
|AdoEnums.RecordStatus.MULTIPLECHANGES|  
|AdoEnums. RecordStatus. NEW|  
|AdoEnums.RecordStatus.OBJECTOPEN|  
|AdoEnums. RecordStatus. OK|  
|AdoEnums. RecordStatus. OUTOFMEMORY|  
|AdoEnums. RecordStatus. PENDINGCHANGES|  
|AdoEnums.RecordStatus.PERMISSIONDENIED|  
|AdoEnums.RecordStatus.SCHEMAVIOLATION|  
|AdoEnums. RecordStatus. 未修改|  
  
## <a name="applies-to"></a>套用至  
 [Status 屬性 (ADO Recordset)](../../../ado/reference/ado-api/status-property-ado-recordset.md)
