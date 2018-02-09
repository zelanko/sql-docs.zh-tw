---
title: FilterGroupEnum | Microsoft Docs
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
- FilterGroupEnum
helpviewer_keywords:
- FilterGroupEnum enumeration [ADO]
ms.assetid: b22e725e-84bd-4286-a070-290c278c3783
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 64a9701680876231d0051789aec0fc43be4c0ad3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="filtergroupenum"></a>FilterGroupEnum
指定要從篩選的記錄群組[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|篩選器來檢視記錄，最後會受到[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)，[重新同步處理](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)呼叫。|  
|**adFilterConflictingRecords**|5|檢視失敗，最後一個批次更新記錄的篩選條件。|  
|**adFilterFetchedRecords**|3|在目前的快取中檢視記錄的篩選器 — 也就是從資料庫擷取記錄的最後一個呼叫的結果。|  
|**adFilterNone**|0|移除目前的篩選條件，並還原所有記錄的檢視。|  
|**adFilterPendingRecords**|1|篩選器來檢視只記錄已變更但尚未傳送到伺服器。 僅適用於批次更新模式。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 Package: **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.FilterGroup.AFFECTEDRECORDS|  
|AdoEnums.FilterGroup.CONFLICTINGRECORDS|  
|AdoEnums.FilterGroup.FETCHEDRECORDS|  
|AdoEnums.FilterGroup.NONE|  
|AdoEnums.FilterGroup.PENDINGRECORDS|  
  
## <a name="applies-to"></a>適用於  
 [Filter 屬性](../../../ado/reference/ado-api/filter-property.md)
