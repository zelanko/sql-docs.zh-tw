---
title: WillExecute 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 234a0eeba57958063a6f2eedb8510486df8a53a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642515"
---
# <a name="willexecute-event-ado"></a>WillExecute 事件 (ADO)
**WillExecute**事件被呼叫之前暫止的命令執行的連接上。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 A**字串**，其中包含 SQL 命令或預存程序名稱。  
  
 *CursorType*  
 A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)所包含的資料指標類型**資料錄集**，將會開啟。 使用這個參數，您可以變更資料指標為期間的任何型別**Recordset**[Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)作業。 *CursorType*將會忽略任何其他作業。  
  
 *LockType*  
 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)所包含的鎖定類型**資料錄集**，將會開啟。 使用這個參數，您可以變更鎖定期間的任何型別的**RecordsetOpen**作業。 *LockType*將會忽略任何其他作業。  
  
 *選項。*  
 A**長**值，指出可以用來執行命令或開啟選項**資料錄集**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)可能的狀態值**adStatusCantDeny**或是**adStatusOK**會呼叫此事件。 如果它是**adStatusCantDeny**，此事件可能不會要求取消暫止的作業。  
  
 *pCommand*  
 [命令物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)物件套用此事件通知。  
  
 *pRecordset*  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)物件套用此事件通知。  
  
 *pConnection*  
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)物件套用此事件通知。  
  
## <a name="remarks"></a>備註  
 A **WillExecute**因為連線可能會發生事件。  [Execute 方法 (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)， [Execute 方法 (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)，或[Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法*pConnection*參數應該永遠包含有效的參考**連線**物件。 如果事件是因**Connection.Execute**，則*pRecordset*並*pCommand*參數會設定為**Nothing**。 如果事件是因**Recordset.Open**，則*pRecordset*參數會參考**資料錄集**物件而*pCommand*參數設定為**Nothing**。 如果事件是因**Command.Execute**，則*pCommand*參數會參考**命令**物件而*pRecordset*參數設定為**Nothing**。  
  
 **WillExecute**可讓您檢查並修改暫止執行的參數。 此事件可能會傳回取消暫止命令的要求。  
  
> [!NOTE]
>  如果原始來源**命令**是所指定的資料流[CommandStream 屬性 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性，指派新字串給**WillExecute** _來源_參數會變更的來源**命令**。 **CommandStream**屬性將會被清除並[CommandText 屬性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性將會更新與新的來源。 所指定的原始資料流**CommandStream**就會釋出，而且無法存取。  
  
 如果在新來源字串的方言與不同的原始設定[Dialect 屬性](../../../ado/reference/ado-api/dialect-property.md)屬性 (其對應到**CommandStream**)，必須指定正確的方言，藉由設定**方言**屬性所參考的命令物件*pCommand*。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
