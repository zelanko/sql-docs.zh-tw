---
title: "FilterGroupEnum |Microsoft 文件"
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
- FilterGroupEnum
helpviewer_keywords:
- FilterGroupEnum enumeration [ADO]
ms.assetid: b22e725e-84bd-4286-a070-290c278c3783
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 424bb4b32915c774778cfd32dab18c42c5e573a8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="filtergroupenum"></a>FilterGroupEnum
指定要從篩選的記錄群組[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|篩選器來檢視記錄，最後會受到[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)，[重新同步處理](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)呼叫。|  
|**adFilterConflictingRecords**|5|檢視失敗，最後一個批次更新記錄的篩選條件。|  
|**adFilterFetchedRecords**|3|在目前的快取中檢視記錄的篩選器 — 也就是從資料庫擷取記錄的最後一個呼叫的結果。|  
|**adFilterNone**|0|移除目前的篩選條件，並還原所有記錄的檢視。|  
|**adFilterPendingRecords**|1|篩選器來檢視只記錄已變更但尚未傳送到伺服器。 僅適用於批次更新模式。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.FilterGroup.AFFECTEDRECORDS|  
|AdoEnums.FilterGroup.CONFLICTINGRECORDS|  
|AdoEnums.FilterGroup.FETCHEDRECORDS|  
|AdoEnums.FilterGroup.NONE|  
|AdoEnums.FilterGroup.PENDINGRECORDS|  
  
## <a name="applies-to"></a>適用於  
 [篩選屬性](../../../ado/reference/ado-api/filter-property.md)

