---
title: Cancel 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Cancel
- _Record::Cancel
- _Connection::Cancel
- Command25::Cancel
- _Stream::Cancel
helpviewer_keywords:
- Cancel method [ADO]
ms.assetid: e0db4e15-6787-41e2-8f13-9e9b524d620a
author: rothja
ms.author: jroth
ms.openlocfilehash: dd6fc7b58d49c788242e029fa004ec38534c8e38
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763539"
---
# <a name="cancel-method-ado"></a>Cancel 方法 (ADO)
取消執行暫止的非同步方法呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Cancel  
```  
  
## <a name="remarks"></a>備註  
 使用**Cancel**方法來終止非同步方法呼叫的執行：也就是使用**adAsyncConnect**、 **adAsyncExecute**或**adAsyncFetch**選項叫用的方法。  
  
 下表顯示當您在特定類型的物件上使用**Cancel**方法時，會終止哪些工作。  
  
|如果*物件*為|此方法的最後非同步呼叫已終止|  
|----------------------|-------------------------------------------------------------|  
|[命令](../../../ado/reference/ado-api/command-object-ado.md)|[執行](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[建立](../../../ado/reference/ado-api/connection-object-ado.md)|[執行](../../../ado/reference/ado-api/execute-method-ado-connection.md)或[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)|  
|[記錄](../../../ado/reference/ado-api/record-object-ado.md)|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)、 [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)、 [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)或[Open](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)|[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)|[開啟](../../../ado/reference/ado-api/open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>套用至  
  
||||  
|-|-|-|  
|[Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>另請參閱  
 [Cancel 方法範例（VB）](../../../ado/reference/ado-api/cancel-method-example-vb.md)   
 [Cancel 方法範例（VBScript）](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Cancel 方法範例（VC + +）](../../../ado/reference/ado-api/cancel-method-example-vc.md)   
 [Cancel 方法（RDS）](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch 方法（ADO）](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 方法（ADO）](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate 方法（RDS）](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Execute 方法（ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Execute 方法（ADO Connection）](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Open 方法（ADO Connection）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)
