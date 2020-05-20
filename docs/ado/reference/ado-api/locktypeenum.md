---
title: LockTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- LockTypeEnum
helpviewer_keywords:
- LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
author: rothja
ms.author: jroth
ms.openlocfilehash: d3fd3c1ffea99abf859a4a328e21da288bc9378a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762529"
---
# <a name="locktypeenum"></a>LockTypeEnum
指定在編輯期間放置在記錄上的鎖定類型。  
  
|持續性|值|說明|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|表示開放式批次更新。 批次更新模式的必要參數。|  
|**adLockOptimistic**|3|表示開放式鎖定，依記錄記錄。 提供者會使用開放式鎖定，只有在您呼叫[Update](../../../ado/reference/ado-api/update-method.md)方法時，才會鎖定記錄。|  
|**adLockPessimistic**|2|表示封閉式鎖定，依記錄記錄。 提供者會執行必要的動作，以確保成功編輯記錄，通常是在編輯之後立即鎖定資料來源的記錄。|  
|**adLockReadOnly**|1|表示唯讀記錄。 您不能改變數據。|  
|**adLockUnspecified**|-1|未指定鎖定的類型。 若為複製，則會使用與原始相同的鎖定類型來建立複製。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. LockType. BATCHOPTIMISTIC|  
|AdoEnums. LockType. 開放式|  
|AdoEnums. LockType。封閉式|  
|AdoEnums. LockType READONLY|  
|AdoEnums. LockType。未指定|  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[Clone 方法 (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)|[LockType 屬性 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)|  
|[Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[WillExecute 事件 (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|
