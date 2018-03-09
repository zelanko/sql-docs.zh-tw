---
title: "WillExecute 事件 (ADO) |Microsoft 文件"
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
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dafc71b9f9da6dde5cf9ef7acf7909236441f656
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="willexecute-event-ado"></a>WillExecute 事件 (ADO)
**WillExecute**事件被呼叫之前暫止命令的連接上執行。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 A**字串**，其中包含 SQL 命令或預存程序名稱。  
  
 *CursorType*  
 A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) ，其中包含的資料指標的類型**資料錄集**，將會開啟。 使用這個參數，您可以將游標變更期間的任何型別**資料錄集**[Open 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)作業。 *CursorType*將忽略任何其他作業。  
  
 *LockType*  
 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) ，其中包含的鎖定類型**資料錄集**，將會開啟。 使用這個參數，您可以變更鎖定期間的任何型別為**RecordsetOpen**作業。 *LockType*將忽略任何其他作業。  
  
 *選項。*  
 A**長**值，指出選項，可用來執行命令或開啟**資料錄集**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)可能的狀態值**adStatusCantDeny**或**adStatusOK**會呼叫這個事件。 如果是**adStatusCantDeny**，此事件可能不會要求取消的暫止的作業。  
  
 *pCommand*  
 [命令 Object (ADO)](../../../ado/reference/ado-api/command-object-ado.md)套用此事件通知的物件。  
  
 *pRecordset*  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)套用此事件通知的物件。  
  
 *pConnection*  
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)套用此事件通知的物件。  
  
## <a name="remarks"></a>備註  
 A **WillExecute**因為連線可能會發生事件。  [Execute 方法 （ADO 連接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)， [Execute Method （ADO 命令中）](../../../ado/reference/ado-api/execute-method-ado-command.md)，或[Open 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法*pConnection*參數應該永遠包含有效的參考**連接**物件。 如果事件的原因是**Connection.Execute**、 *pRecordset*和*pCommand*參數已設為**Nothing**。 如果事件的原因是**Recordset.Open**、 *pRecordset*參數會參考**資料錄集**物件和*pCommand*參數設定為**Nothing**。 如果事件的原因是**Command.Execute**、 *pCommand*參數會參考**命令**物件和*pRecordset*參數設定為**Nothing**。  
  
 **WillExecute**可讓您檢查並修改暫止執行的參數。 此事件可能會傳回取消暫止命令的要求。  
  
> [!NOTE]
>  如果原始來源**命令**是所指定的資料流[CommandStream 屬性 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性，指派新字串給 **WillExecute * * * 來源*參數會變更的來源**命令**。 **CommandStream**會清除屬性和[CommandText 屬性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性將會更新與新的來源。 所指定的原始資料流**CommandStream**就會發行並無法存取。  
  
 如果新的來源字串的方言與不同的原始設定[方言屬性](../../../ado/reference/ado-api/dialect-property.md)屬性 (其對應到**CommandStream**)，您必須指定正確的方言設定**方言**屬性所參考的命令物件*pCommand*。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
