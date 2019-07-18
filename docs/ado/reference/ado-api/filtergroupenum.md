---
title: FilterGroupEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FilterGroupEnum
helpviewer_keywords:
- FilterGroupEnum enumeration [ADO]
ms.assetid: b22e725e-84bd-4286-a070-290c278c3783
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97add08a1d656e8c163600bb0ea8dda7fca264b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932648"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
指定要從篩選的記錄群組[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|檢視上次所影響的記錄篩選[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)，[重新同步處理](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)呼叫。|  
|**adFilterConflictingRecords**|5|檢視失敗的最後一個批次更新記錄的篩選條件。|  
|**adFilterFetchedRecords**|3|檢視目前的快取中的記錄的篩選器-也就是從資料庫擷取記錄的最後一個呼叫的結果。|  
|**adFilterNone**|0|移除目前的篩選條件，並還原所有記錄進行檢視。|  
|**adFilterPendingRecords**|1|檢視只會記錄的篩選條件的已變更但尚未傳送至伺服器。 只適用於批次更新模式。|  
  
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
 [Filter 屬性](../../../ado/reference/ado-api/filter-property.md)
