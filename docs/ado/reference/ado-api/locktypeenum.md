---
title: "LockTypeEnum |Microsoft 文件"
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
- LockTypeEnum
helpviewer_keywords:
- LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d1918f82bfe2361a90ca6f2479934ae1deba7664
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="locktypeenum"></a>LockTypeEnum
指定在編輯期間鎖定記錄類型。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**Adlockpessimistic**|4|表示開放式批次更新。 所需的批次更新模式。|  
|**Adlockreadonly**|3|表示開放式鎖定、 記錄。 提供者會使用開放式鎖定，鎖定資料錄，只有當您呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法。|  
|**Locktype**|2|指出封閉式鎖定、 記錄。 提供者沒有什麼是為了確保成功編輯記錄，通常藉由編輯之後，立即鎖定記錄在資料來源。|  
|**Recordset**|1|表示唯讀的記錄。 您無法變更資料。|  
|**adLockUnspecified**|-1|未指定鎖定的類型。 複製程式碼，是使用相同的鎖定類型與原始建立複製。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
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
|[Open 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[WillExecute 事件 (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|

