---
title: "Cancel 方法 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d9dd6f6c62d9ee20f75dabc8b28831b7376fc00b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="cancel-method-ado"></a>Cancel 方法 (ADO)
取消暫止的非同步方法呼叫的執行。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Cancel  
```  
  
## <a name="remarks"></a>備註  
 使用**取消**來結束執行非同步方法呼叫的方法： 也就是叫用方法與**adAsyncConnect**， **adAsyncExecute**，或**adAsyncFetch**選項。  
  
 下表顯示當您使用時，會終止哪些工作**取消**特定類型的物件上的方法。  
  
|如果*物件*是|此方法的最後一個非同步呼叫已終止|  
|----------------------|-------------------------------------------------------------|  
|[Command](../../../ado/reference/ado-api/command-object-ado.md)|[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[連接](../../../ado/reference/ado-api/connection-object-ado.md)|[執行](../../../ado/reference/ado-api/execute-method-ado-connection.md)或[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)|  
|[Record](../../../ado/reference/ado-api/record-object-ado.md)|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)， [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)， [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)，或[開啟](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)|[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Stream](../../../ado/reference/ado-api/stream-object-ado.md)|[開啟](../../../ado/reference/ado-api/open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>另請參閱  
 [取消方法範例 (VB)](../../../ado/reference/ado-api/cancel-method-example-vb.md)   
 [取消方法範例 (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [取消方法的範例 （VC + +）](../../../ado/reference/ado-api/cancel-method-example-vc.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate 方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Execute 方法 （ADO 命令中）](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Execute 方法 （ADO 連接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Open 方法 （ADO 連接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)
