---
title: ExecuteComplete 事件（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
author: rothja
ms.author: jroth
ms.openlocfilehash: ae8b426a0e4b95498cb0d4f9a4590c3aaf30196d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760134"
---
# <a name="executecomplete-event-ado"></a>ExecuteComplete 事件 (ADO)
在命令完成執行之後，會呼叫**ExecuteComplete**事件。  
  
## <a name="syntax"></a>語法  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *RecordsAffected*  
 **長**數值，指出受命令影響的記錄數目。  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它會描述**adStatus**的值為**adStatusErrorsOccurred**時所發生的錯誤。否則不會設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。 呼叫這個事件時，如果造成事件的作業成功，此參數會設定為**adStatusOK** ，如果作業失敗，則為**adStatusErrorsOccurred** 。  
  
 在此事件傳回之前，請將此參數設定為**adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pCommand*  
 已執行的[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。 包含**命令**物件，即使在呼叫**Connection. Execute**或 Recordset 時也一樣 **。開啟**時不明確建立**命令**，在此情況下，會在 ADO 內部建立**命令**物件。  
  
 *pRecordset*  
 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，這是執行命令的結果。 此**記錄集**可能是空的。 您絕對不應該從這個事件處理常式中摧毀此記錄集物件。 這麼做會導致在 ADO 嘗試存取已不存在的物件時，發生存取違規。  
  
 *pConnection*  
 [Connection](../../../ado/reference/ado-api/connection-object-ado.md)物件。 執行作業所用的連接。  
  
## <a name="remarks"></a>備註  
 **ExecuteComplete**事件可能因為連接而發生 **。**[執行](../../../ado/reference/ado-api/execute-method-ado-connection.md)，**命令。**[執行](../../../ado/reference/ado-api/execute-method-ado-command.md)、**記錄集。**[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)、**記錄集。** 重新[查詢](../../../ado/reference/ado-api/requery-method.md)或**記錄集。**[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)方法。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
