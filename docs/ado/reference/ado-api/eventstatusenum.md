---
description: EventStatusEnum
title: EventStatusEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventStatusEnum
helpviewer_keywords:
- EventStatusEnum enumeration [ADO]
ms.assetid: ebfd4cda-4017-4873-9d28-38b1c7db12a8
author: rothja
ms.author: jroth
ms.openlocfilehash: 3d696d7b971b5f6624a85addb3f023f2090ac90d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443900"
---
# <a name="eventstatusenum"></a>EventStatusEnum
指定事件執行的目前狀態。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adStatusCancel**|4|要求取消導致發生事件的作業。|  
|**adStatusCantDeny**|3|指出作業無法要求取消暫止的作業。|  
|**adStatusErrorsOccurred**|2|指出造成事件的作業因錯誤或錯誤而失敗。|  
|**adStatusOK**|1|指出造成事件的作業已成功。|  
|**adStatusUnwantedEvent**|5|在事件方法執行完成之前，防止後續的通知。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums. EventStatus. CANCEL|  
|AdoEnums. EventStatus. CANTDENY|  
|AdoEnums. EventStatus. ERRORSOCCURRED|  
|AdoEnums. EventStatus. 確定|  
|AdoEnums. EventStatus. UNWANTEDEVENT|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [BeginTransComplete、CommitTransComplete 和 RollbackTransComplete 事件 (ADO) ](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)  

        [ConnectComplete 和 Disconnect 事件 (ADO)](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)  

        [EndOfRecordset 事件 (ADO)](../../../ado/reference/ado-api/endofrecordset-event-ado.md)  

        [ExecuteComplete 事件 (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)  
    :::column-end:::
    :::column:::
        [FetchComplete 事件 (ADO)](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)  

        [InfoMessage 事件 (ADO)](../../../ado/reference/ado-api/infomessage-event-ado.md)  

        [WillChangeField 和 FieldChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)  

        [WillChangeRecord 和 RecordChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)  
    :::column-end:::
    :::column:::
        [WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)  

        [WillConnect 事件 (ADO)](../../../ado/reference/ado-api/willconnect-event-ado.md)  

        [WillExecute 事件 (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)  

        [WillMove 和 MoveComplete 事件 (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)  
    :::column-end:::
:::row-end:::
