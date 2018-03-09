---
title: LockTypeEnum | Microsoft Docs
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
- LockTypeEnum
helpviewer_keywords:
- LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f9fe62c251092eb182925de0fa7b6d70c359a25d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="locktypeenum"></a>LockTypeEnum
指定在編輯期間鎖定記錄類型。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|表示開放式批次更新。 所需的批次更新模式。|  
|**adLockOptimistic**|3|表示開放式鎖定、 記錄。 提供者會使用開放式鎖定，鎖定資料錄，只有當您呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法。|  
|**adLockPessimistic**|2|指出封閉式鎖定、 記錄。 提供者沒有什麼是為了確保成功編輯記錄，通常藉由編輯之後，立即鎖定記錄在資料來源。|  
|**adLockReadOnly**|1|表示唯讀的記錄。 您無法變更資料。|  
|**adLockUnspecified**|-1|未指定鎖定的類型。 複製程式碼，是使用相同的鎖定類型與原始建立複製。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 Package: **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums.LockType.OPTIMISTIC|  
|AdoEnums.LockType.PESSIMISTIC|  
|AdoEnums.LockType.READONLY|  
|AdoEnums.LockType.UNSPECIFIED|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Clone 方法 (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)|[LockType 屬性 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)|  
|[Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[WillExecute 事件 (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|
