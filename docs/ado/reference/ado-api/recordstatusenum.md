---
title: "RecordStatusEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- RecordStatusEnum
helpviewer_keywords:
- RecordStatusEnum enumeration [ADO]
ms.assetid: 506fdd70-4452-4e83-95d5-c94311988dfa
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bf2413bed1bbdf96b83b7e805aac90529a721c9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="recordstatusenum"></a>RecordStatusEnum
指定[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)的批次更新和其他的大量作業的記錄。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|表示記錄已不會儲存因為操作已經取消。|  
|**adRecCantRelease**|0x400|表示因為現有的記錄已鎖定，已不會儲存新的記錄。|  
|**adRecConcurrencyViolation**|0x800|表示記錄已不會儲存因為開放式並行存取正在使用中。|  
|**adRecDBDeleted**|0x40000|指出將記錄從資料來源中已經被刪除。|  
|**adRecDeleted**|0x4|表示記錄已刪除。|  
|**adRecIntegrityViolation**|0x1000|表示記錄已不會儲存因為使用者違反完整性條件約束。|  
|**adRecInvalid**|0x10|表示記錄已不會儲存因為它的書籤不正確。|  
|**adRecMaxChangesExceeded**|0x2000|表示記錄已不會儲存因為有太多暫止的變更。|  
|**adRecModified**|0x2|表示記錄已修改。|  
|**adRecMultipleChanges**|0x40|指出，記錄不儲存，因為它會影響多筆記錄。|  
|**adRecNew**|0x1|表示記錄是新的。|  
|**adRecObjectOpen**|0x4000|指出因為與開啟的儲存體物件發生衝突而不儲存記錄。|  
|**adRecOK**|0|表示已成功更新記錄。|  
|**adRecOutOfMemory**|0x8000|表示記錄已不會儲存因為電腦已用完記憶體。|  
|**adRecPendingChanges**|0x80|表示記錄已不會儲存因為它參考到暫止的插入。|  
|**adRecPermissionDenied**|0x10000|表示記錄已不會儲存因為使用者沒有足夠權限。|  
|**adRecSchemaViolation**|0x20000|表示記錄已不會儲存因為它違反基礎資料庫的結構。|  
|**adRecUnmodified**|0x8|表示記錄已修改。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 AdoEnums.RecordStatus。  
  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.RecordStatus.CANCELED|  
|AdoEnums.RecordStatus.CANTRELEASE|  
|AdoEnums.RecordStatus.CONCURRENCYVIOLATION|  
|AdoEnums.RecordStatus.DBDELETED|  
|AdoEnums.RecordStatus.DELETED|  
|AdoEnums.RecordStatus.INTEGRITYVIOLATION|  
|AdoEnums.RecordStatus.INVALID|  
|AdoEnums.RecordStatus.MAXCHANGESEXCEEDED|  
|AdoEnums.RecordStatus.MODIFIED|  
|AdoEnums.RecordStatus.MULTIPLECHANGES|  
|AdoEnums.RecordStatus.NEW|  
|AdoEnums.RecordStatus.OBJECTOPEN|  
|AdoEnums.RecordStatus.OK|  
|AdoEnums.RecordStatus.OUTOFMEMORY|  
|AdoEnums.RecordStatus.PENDINGCHANGES|  
|AdoEnums.RecordStatus.PERMISSIONDENIED|  
|AdoEnums.RecordStatus.SCHEMAVIOLATION|  
|AdoEnums.RecordStatus.UNMODIFIED|  
  
## <a name="applies-to"></a>適用於  
 [Status 屬性 （ADO 資料錄集）](../../../ado/reference/ado-api/status-property-ado-recordset.md)
