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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 28c64bbe66da1adf6ad4d3a0f9484789ee2a71dd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838227"
---
# <a name="ado-events"></a>ADO 事件
|||  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|之後呼叫**BeginTrans**作業。|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|之後呼叫**CommitTrans**作業。|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|連接啟動之後呼叫。|  
|[中斷連接](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|連線結束後呼叫。|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|嘗試移至結尾的資料列時，呼叫**資料錄集**。|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|命令已完成執行之後呼叫。|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|呼叫到擷取冗長的非同步作業中的所有記錄之後**資料錄集**。|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|在冗長的非同步作業，以報告目前到擷取多少資料列期間定期呼叫**資料錄集**。|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|一或多個值之後呼叫**欄位**物件已變更。|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|每當期間發生警告時呼叫**ConnectionEvent**作業。|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|中的目前位置之後，呼叫**資料錄集**變更。|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|呼叫之後變更一或多個記錄。|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|之後呼叫**資料錄集**已變更。|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|之後呼叫**RollbackTrans**作業。|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|暫止的作業會變更一或多個值之前呼叫**欄位**中的物件**資料錄集**。|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|一或多個資料錄 （資料列） 之前呼叫**資料錄集**變更。|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|呼叫之前暫止的作業會變更**資料錄集**。|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|連接啟動之前呼叫。|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|暫止命令這個連接上執行，並提供使用者有機會檢查和修改暫止執行參數時之前, 呼叫。|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|**WillMove**稱為事件*之前*暫止的作業變更的目前位置**資料錄集**。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 列舉常數](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附錄 B:ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [處理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 物件與介面](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 屬性](../../../ado/reference/ado-api/ado-properties.md)
