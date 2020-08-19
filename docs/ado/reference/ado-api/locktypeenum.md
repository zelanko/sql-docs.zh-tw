---
description: LockTypeEnum
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
ms.openlocfilehash: 52a6e4af75ac8887c23dd245a58981b1bbfb7eb2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443330"
---
# <a name="locktypeenum"></a>LockTypeEnum
指定在編輯期間放置於記錄的鎖定類型。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|表示開放式批次更新。 批次更新模式的必要參數。|  
|**adLockOptimistic**|3|表示開放式鎖定、依記錄記錄。 提供者會使用開放式鎖定，只在您呼叫 [Update](../../../ado/reference/ado-api/update-method.md) 方法時鎖定記錄。|  
|**adLockPessimistic**|2|指出封閉式鎖定、依記錄記錄。 提供者會執行必要的動作，以確保成功編輯記錄，通常是在編輯之後立即鎖定資料來源的記錄。|  
|**adLockReadOnly**|1|表示唯讀記錄。 您無法變更資料。|  
|**adLockUnspecified**|-1|未指定鎖定的類型。 若為複製，則會建立與原始的相同鎖定類型的複製。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums. LockType. 開放式|  
|AdoEnums. LockType|  
|AdoEnums. LockType READONLY|  
|AdoEnums. LockType。未指定|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Clone 方法 (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)  
        [LockType 屬性 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)  
    :::column-end:::
    :::column:::
        [Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)  
        [WillExecute 事件 (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)  
    :::column-end:::
:::row-end:::
