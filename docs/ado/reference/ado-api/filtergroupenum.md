---
description: FilterGroupEnum
title: FilterGroupEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1d9fdf420ee3b550bebfe394bf6722623307384a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88972989"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
指定要從 [記錄集](./recordset-object-ado.md)篩選的記錄群組。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|僅用於查看由上次 [刪除](./delete-method-ado-recordset.md)、重新 [同步](./resync-method.md)、 [UpdateBatch](./updatebatch-method.md)或 [CancelBatch](./cancelbatch-method-ado.md) 呼叫所影響之記錄的篩選準則。|  
|**adFilterConflictingRecords**|5|用來查看上次批次更新失敗記錄的篩選準則。|  
|**adFilterFetchedRecords**|3|用來查看目前快取中記錄的篩選器，也就是上次呼叫從資料庫取出記錄的結果。|  
|**adFilterNone**|0|移除目前的篩選，並還原所有記錄以進行查看。|  
|**adFilterPendingRecords**|1|僅用於查看已變更但尚未傳送至伺服器之記錄的篩選準則。 僅適用于批次更新模式。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.FilterGroup.AFFECTEDRECORDS|  
|AdoEnums.FilterGroup.CONFLICTINGRECORDS|  
|AdoEnums.FilterGroup.FETCHEDRECORDS|  
|AdoEnums. FilterGroup。無|  
|AdoEnums.FilterGroup.PENDINGRECORDS|  
  
## <a name="applies-to"></a>套用至  
 [Filter 屬性](./filter-property.md)