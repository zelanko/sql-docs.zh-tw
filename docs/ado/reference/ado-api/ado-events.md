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
ms.openlocfilehash: 07ef1c379dcf59b386b86d5b9fce38f77c521e01
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451420"
---
# <a name="ado-events"></a>ADO 事件

|事件|描述|  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|在 **BeginTrans** 作業之後呼叫。|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|在 **CommitTrans** 作業之後呼叫。|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|在連接開始之後呼叫。|  
|[中斷連線](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|在連接結束之後呼叫。|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|嘗試移到 **記錄集**結尾之後的資料列時呼叫。|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|在命令完成執行之後呼叫。|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|在冗長的非同步作業中的所有記錄都被抓取到 **記錄集**之後呼叫。|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|在冗長的非同步作業期間定期呼叫，以報告目前已抓取到 **記錄集**的資料列數目。|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|在一或多個 **欄位** 物件的值變更之後呼叫。|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|在 **ConnectionEvent** 作業期間發生警告時呼叫。|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|在 **記錄集** 的目前位置變更之後呼叫。|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|在一或多筆記錄變更之後呼叫。|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|在 **記錄集** 變更之後呼叫。|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|在 **RollbackTrans** 作業之後呼叫。|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|在暫止的作業之前呼叫，會變更**記錄集中**一個或多個**欄位**物件的值。|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|在一或多筆記錄之前呼叫， (資料列集中) 的資料列 **集** 變更。|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|在暫止的作業變更 **記錄集**之前呼叫。|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|在連接開始之前呼叫。|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|在此連接上執行暫止命令之前呼叫，並讓使用者有機會檢查和修改暫止的執行參數。|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|在暫止的作業變更**記錄集**的目前位置*之前*，會呼叫**WillMove**事件。|  
  
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
