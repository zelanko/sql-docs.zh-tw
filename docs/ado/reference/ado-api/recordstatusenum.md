---
description: RecordStatusEnum
title: RecordStatusEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e4d2ad74187ef6be146be04f63e634bbdf3de9f5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989669"
---
# <a name="recordstatusenum"></a>RecordStatusEnum
指定與批次更新和其他大量作業有關的記錄 [狀態](./status-property-ado-recordset.md) 。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|指出因為作業已取消，所以未儲存記錄。|  
|**adRecCantRelease**|0x400|指出因為現有的記錄已鎖定，所以不會儲存新的記錄。|  
|**adRecConcurrencyViolation**|0x800|指出未儲存記錄，因為正在使用開放式平行存取。|  
|**adRecDBDeleted**|0x40000|指出已經從資料來源中刪除記錄。|  
|**adRecDeleted**|0x4|指出已刪除記錄。|  
|**adRecIntegrityViolation**|0x1000|指出未儲存記錄，因為使用者違反了完整性條件約束。|  
|**adRecInvalid**|0x10|指出未儲存記錄，因為它的書簽無效。|  
|**adRecMaxChangesExceeded**|0x2000|指出未儲存記錄，因為有太多暫止的變更。|  
|**adRecModified**|0x2|表示已修改記錄。|  
|**adRecMultipleChanges**|0x40|指出記錄未儲存，因為它會影響多筆記錄。|  
|**adRecNew**|0x1|表示記錄是新的。|  
|**adRecObjectOpen**|0x4000|指出因為與開啟的儲存物件發生衝突，所以不會儲存記錄。|  
|**adRecOK**|0|表示已成功更新記錄。|  
|**adRecOutOfMemory**|0x8000|指出未儲存記錄，因為電腦已用盡記憶體。|  
|**adRecPendingChanges**|0x80|指出記錄未儲存，因為它參考暫止的插入。|  
|**adRecPermissionDenied**|0x10000|指出未儲存記錄，因為使用者的許可權不足。|  
|**adRecSchemaViolation**|0x20000|指出未儲存記錄，因為它違反基礎資料庫的結構。|  
|**adRecUnmodified**|0x8|指出未修改記錄。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 AdoEnums.RecordStatus.  
  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. RecordStatus。已取消|  
|AdoEnums.RecordStatus.CANTRELEASE|  
|AdoEnums. RecordStatus. CONCURRENCYVIOLATION|  
|AdoEnums.RecordStatus.DBDELETED|  
|AdoEnums. RecordStatus 刪除|  
|AdoEnums.RecordStatus.INTEGRITYVIOLATION|  
|AdoEnums. RecordStatus 無效|  
|AdoEnums.RecordStatus.MAXCHANGESEXCEEDED|  
|AdoEnums. RecordStatus 修改|  
|AdoEnums.RecordStatus.MULTIPLECHANGES|  
|AdoEnums. RecordStatus. NEW|  
|AdoEnums.RecordStatus.OBJECTOPEN|  
|AdoEnums. RecordStatus. 確定|  
|AdoEnums. RecordStatus. OUTOFMEMORY|  
|AdoEnums. RecordStatus. PENDINGCHANGES|  
|AdoEnums.RecordStatus.PERMISSIONDENIED|  
|AdoEnums.RecordStatus.SCHEMAVIOLATION|  
|AdoEnums. RecordStatus. 未修改|  
  
## <a name="applies-to"></a>套用至  
 [Status 屬性 (ADO Recordset)](./status-property-ado-recordset.md)