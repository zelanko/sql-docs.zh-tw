---
title: "ExecuteComplete 事件 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords: ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 327eee8b19a0d1b9ad4d67c45c90ccd2c632622a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="executecomplete-event-ado"></a>ExecuteComplete 事件 (ADO)
**ExecuteComplete**命令已完成執行之後，會呼叫事件。  
  
## <a name="syntax"></a>語法  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *RecordsAffected*  
 A**長**值，指出受到該命令的記錄數目。  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它描述如果發生之錯誤的值**adStatus**是**adStatusErrorsOccurred**; 否則它不會設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。 當呼叫這個事件時，這個參數會設定為**adStatusOK**如果造成事件的作業成功，或**adStatusErrorsOccurred**作業失敗。  
  
 這個事件會傳回之前，請將此參數設定為**adStatusUnwantedEvent**以避免後續的通知。  
  
 *pCommand*  
 [命令](../../../ado/reference/ado-api/command-object-ado.md)上次執行所執行的物件。 包含**命令**物件呼叫，即使**Connection.Execute**或**Recordset.Open**而不需要明確建立**命令**在哪些情況下**命令**物件由 ADO 在內部建立。  
  
 *pRecordset*  
 A[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)所執行的命令的結果物件。 這**資料錄集**可能是空的。 您應該永遠不會終結資料錄集物件從這個事件處理常式內。 這樣會導致存取違規，當 ADO 嘗試存取不存在的物件。  
  
 *pConnection*  
 A[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。 作業已執行的連接。  
  
## <a name="remarks"></a>備註  
 **ExecuteComplete**事件可能會發生因為**連線。**[執行](../../../ado/reference/ado-api/execute-method-ado-connection.md)，**命令。**[執行](../../../ado/reference/ado-api/execute-method-ado-command.md)，**資料錄集。**[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)，**資料錄集。**[Requery](../../../ado/reference/ado-api/requery-method.md)，或**資料錄集。**[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)方法。  
  
## <a name="see-also"></a>請參閱＜  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
