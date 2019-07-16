---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8883679a85d1e134b1759c90cde524bb97995130
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932861"
---
# <a name="eventstatusenum"></a>EventStatusEnum
指定的事件執行的目前狀態。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adStatusCancel**|4|要求取消作業，導致發生此事件。|  
|**adStatusCantDeny**|3|指出此作業無法要求取消暫止的作業。|  
|**adStatusErrorsOccurred**|2|表示造成事件的作業失敗，因為發生錯誤或錯誤。|  
|**adStatusOK**|1|表示造成事件的作業已順利完成。|  
|**adStatusUnwantedEvent**|5|事件的方法完成執行之前，可防止後續的通知。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.EventStatus.CANCEL|  
|AdoEnums.EventStatus.CANTDENY|  
|AdoEnums.EventStatus.ERRORSOCCURRED|  
|AdoEnums.EventStatus.OK|  
|AdoEnums.EventStatus.UNWANTEDEVENT|  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[BeginTransComplete、 CommitTransComplete 和 RollbackTransComplete 事件 (ADO)](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|[ConnectComplete 和 Disconnect 事件 (ADO)](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|[EndOfRecordset 事件 (ADO)](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|  
|[ExecuteComplete 事件 (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)|[FetchComplete 事件 (ADO)](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|[InfoMessage 事件 (ADO)](../../../ado/reference/ado-api/infomessage-event-ado.md)|  
|[WillChangeField 和 FieldChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|[WillChangeRecord 和 RecordChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[WillConnect 事件 (ADO)](../../../ado/reference/ado-api/willconnect-event-ado.md)|[WillExecute 事件 (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|[WillMove 和 MoveComplete 事件 (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|
