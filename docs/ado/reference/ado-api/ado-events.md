---
title: ADO 事件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
ms.assetid: 0ded5ad9-8f83-4224-95af-38512783b972
author: rothja
ms.author: jroth
ms.openlocfilehash: a93353be1737b38e7acb557a682e84cbb947c2a1
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242868"
---
# <a name="ado-events"></a>ADO 事件

|事件|描述|  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|在**BeginTrans**作業之後呼叫。|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|在**CommitTrans**作業之後呼叫。|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|在連接啟動之後呼叫。|  
|[取消](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|在連接結束後呼叫。|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|嘗試移至超過**記錄集**結尾的資料列時呼叫。|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|在命令完成執行之後呼叫。|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|在冗長非同步作業中的所有記錄都已抓取到**記錄集**後呼叫。|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|在冗長的非同步作業期間定期呼叫，以報告目前已抓取到**記錄集**的資料列數目。|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|在一或多個**欄位**物件的值已變更之後呼叫。|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|每當在**ConnectionEvent**作業期間發生警告時呼叫。|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|在**記錄集**的目前位置變更之後呼叫。|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|在一或多筆記錄變更後呼叫。|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|在**記錄集**變更後呼叫。|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|在**RollbackTrans**作業之後呼叫。|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|在暫止的作業變更**記錄集中**一個或多個**欄位**物件的值之前呼叫。|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|在**記錄集**的一或多筆記錄（資料列）變更之前呼叫。|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|在暫止的作業變更**記錄集**之前呼叫。|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|在連接開始之前呼叫。|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|在此連接上執行暫止的命令之前呼叫，並為使用者提供檢查和修改暫止執行參數的機會。|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|在暫止的作業變更**記錄集**內的目前位置*之前*，會呼叫**WillMove**事件。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 列舉常數](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附錄 B： ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [處理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 物件和介面](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 屬性](../../../ado/reference/ado-api/ado-properties.md)
