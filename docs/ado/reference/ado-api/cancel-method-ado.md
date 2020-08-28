---
description: Cancel 方法 (ADO)
title: " (ADO) 的 Cancel 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 75829400fbb1beb838b9254acf7db129980046c3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975649"
---
# <a name="cancel-method-ado"></a>Cancel 方法 (ADO)
取消執行暫止的非同步方法呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Cancel  
```  
  
## <a name="remarks"></a>備註  
 使用 **Cancel** 方法來終止非同步方法呼叫的執行：也就是使用 **adAsyncConnect**、 **adAsyncExecute**或 **adAsyncFetch** 選項叫用的方法。  
  
 下表顯示當您針對特定類型的物件使用 **Cancel** 方法時，會終止的工作。  
  
|如果 *物件* 為|此方法的最後非同步呼叫已終止|  
|----------------------|-------------------------------------------------------------|  
|[命令](./command-object-ado.md)|[執行](./execute-method-ado-command.md)|  
|[[連接]](./connection-object-ado.md)|[執行](./execute-method-ado-connection.md) 或 [開啟](./open-method-ado-connection.md)|  
|[記錄](./record-object-ado.md)|[CopyRecord](./copyrecord-method-ado.md)、 [DeleteRecord](./deleterecord-method-ado.md)、 [MoveRecord](./moverecord-method-ado.md)或 [Open](./open-method-ado-record.md)|  
|[Recordset](./recordset-object-ado.md)|[開啟](./open-method-ado-recordset.md)|  
|[資料流](./stream-object-ado.md)|[開啟](./open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Command 物件 (ADO)](./command-object-ado.md)  
        [Connection 物件 (ADO)](./connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Record 物件 (ADO)](./record-object-ado.md)  
        [Recordset 物件 (ADO)](./recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [Stream 物件 (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [Cancel 方法範例 (VB) ](./cancel-method-example-vb.md)   
 [Cancel 方法範例 (VBScript) ](../rds-api/cancel-method-example-vbscript.md)   
 [Cancel 方法範例 (VC + +) ](./cancel-method-example-vc.md)   
 [ (RDS) 的 Cancel 方法 ](../rds-api/cancel-method-rds.md)   
 [ (ADO) 的 CancelBatch 方法 ](./cancelbatch-method-ado.md)   
 [ (ADO) 的 CancelUpdate 方法 ](./cancelupdate-method-ado.md)   
 [RDS)  (CancelUpdate 方法 ](../rds-api/cancelupdate-method-rds.md)   
 [ (ADO 命令的 Execute 方法) ](./execute-method-ado-command.md)   
 [ (ADO 連接) 的 Execute 方法 ](./execute-method-ado-connection.md)   
 [ (ADO Connection) 的 Open 方法 ](./open-method-ado-connection.md)   
 [Open 方法 (ADO Recordset)](./open-method-ado-recordset.md)