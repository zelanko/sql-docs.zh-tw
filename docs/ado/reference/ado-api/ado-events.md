---
description: ADO 事件
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
ms.openlocfilehash: 4644596d216bd459b19778607e309cb7713d6fc4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776657"
---
# <a name="ado-events"></a>ADO 事件

|事件|描述|  
|-|-|  
|[BeginTransComplete](./begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|在 **BeginTrans** 作業之後呼叫。|  
|[CommitTransComplete](./begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|在 **CommitTrans** 作業之後呼叫。|  
|[ConnectComplete](./connectcomplete-and-disconnect-events-ado.md)|在連接開始之後呼叫。|  
|[斷開](./connectcomplete-and-disconnect-events-ado.md)|在連接結束之後呼叫。|  
|[EndOfRecordset](./endofrecordset-event-ado.md)|嘗試移到 **記錄集**結尾之後的資料列時呼叫。|  
|[ExecuteComplete](./executecomplete-event-ado.md)|在命令完成執行之後呼叫。|  
|[FetchComplete](./fetchcomplete-event-ado.md)|在冗長的非同步作業中的所有記錄都被抓取到 **記錄集**之後呼叫。|  
|[FetchProgress](./fetchprogress-event-ado.md)|在冗長的非同步作業期間定期呼叫，以報告目前已抓取到 **記錄集**的資料列數目。|  
|[FieldChangeComplete](./willchangefield-and-fieldchangecomplete-events-ado.md)|在一或多個 **欄位** 物件的值變更之後呼叫。|  
|[InfoMessage](./infomessage-event-ado.md)|在 **ConnectionEvent** 作業期間發生警告時呼叫。|  
|[MoveComplete](./willmove-and-movecomplete-events-ado.md)|在 **記錄集** 的目前位置變更之後呼叫。|  
|[RecordChangeComplete](./willchangerecord-and-recordchangecomplete-events-ado.md)|在一或多筆記錄變更之後呼叫。|  
|[RecordsetChangeComplete](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|在 **記錄集** 變更之後呼叫。|  
|[RollbackTransComplete](./begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|在 **RollbackTrans** 作業之後呼叫。|  
|[WillChangeField](./willchangefield-and-fieldchangecomplete-events-ado.md)|在暫止的作業之前呼叫，會變更**記錄集中**一個或多個**欄位**物件的值。|  
|[WillChangeRecord](./willchangerecord-and-recordchangecomplete-events-ado.md)|在一或多筆記錄之前呼叫， (資料列集中) 的資料列 **集** 變更。|  
|[WillChangeRecordset](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|在暫止的作業變更 **記錄集**之前呼叫。|  
|[WillConnect](./willconnect-event-ado.md)|在連接開始之前呼叫。|  
|[WillExecute](./willexecute-event-ado.md)|在此連接上執行暫止命令之前呼叫，並讓使用者有機會檢查和修改暫止的執行參數。|  
|[WillMove](./willmove-and-movecomplete-events-ado.md)|在暫止的作業變更**記錄集**的目前位置*之前*，會呼叫**WillMove**事件。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](./ado-api-reference.md)   
 [ADO 集合](./ado-collections.md)   
 [ADO 動態屬性](./ado-dynamic-properties.md)   
 [ADO 列舉常數](./ado-enumerated-constants.md)   
 [附錄 B： ADO 錯誤](../../guide/appendixes/appendix-b-ado-errors.md)   
 [處理 ADO 事件](../../guide/data/handling-ado-events.md)   
 [ADO 方法](./ado-methods.md)   
 [ADO 物件模型](./ado-object-model.md)   
 [ADO 物件和介面](./ado-objects-and-interfaces.md)   
 [ADO 屬性](./ado-properties.md)