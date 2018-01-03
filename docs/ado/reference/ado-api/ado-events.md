---
title: "ADO 事件 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- events [ADO]
- ADO, events
ms.assetid: 0ded5ad9-8f83-4224-95af-38512783b972
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dec529bcbc7130ea29fac793a82a5979974f396e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="ado-events"></a>ADO 事件
|||  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|之後呼叫**BeginTrans**作業。|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|之後呼叫**CommitTrans**作業。|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|連接啟動之後呼叫。|  
|[中斷連接](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|連線結束後呼叫。|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|嘗試將移到超過結尾的資料列時呼叫**資料錄集**。|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|命令已完成執行之後呼叫。|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|呼叫長時間的非同步作業中的所有記錄到都擷取之後**資料錄集**。|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|在冗長的非同步作業，以回報到目前已擷取多少資料列期間定期呼叫**資料錄集**。|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|一或多個值之後呼叫**欄位**物件已變更。|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|每當期間發生警告呼叫**ConnectionEvent**作業。|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|中的目前位置之後呼叫**資料錄集**變更。|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|呼叫之後變更一個或多個記錄。|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|之後呼叫**資料錄集**已變更。|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|之後呼叫**RollbackTrans**作業。|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|暫止作業的一或多個值的變更之前呼叫**欄位**中的物件**資料錄集**。|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|前一個或多個記錄 （列） 呼叫**資料錄集**變更。|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|變更暫止作業之前，呼叫**資料錄集**。|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|啟動連接之前呼叫。|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|暫止命令此連接上執行，並提供使用者有機會檢查和修改暫止執行參數之前呼叫。|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|**WillMove**事件呼叫*之前*暫止的作業變更的目前位置**資料錄集**。|  
  
## <a name="see-also"></a>請參閱  
 [ADO 應用程式開發介面參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 列舉常數](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附錄 b: ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [處理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 物件與介面](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 屬性](../../../ado/reference/ado-api/ado-properties.md)
