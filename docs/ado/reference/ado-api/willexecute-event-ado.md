---
title: WillExecute 事件（ADO） |Microsoft Docs
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
ms.openlocfilehash: e0e7c29be102e9c5c7709816895a6647c95337c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67936618"
---
# <a name="willexecute-event-ado"></a>WillExecute 事件 (ADO)
在連接上執行暫止的命令之前，會呼叫**WillExecute**事件。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 包含 SQL 命令或預存程式名稱的**字串**。  
  
 *CursorType*  
 [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) ，其中包含要開啟之**記錄集**的資料指標類型。 使用此參數，您可以在**記錄集**[開放式方法（ADO 記錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)作業期間，將資料指標變更為任何類型。 任何其他作業將會忽略*CursorType* 。  
  
 *LockType*  
 [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) ，其中包含要開啟之**記錄集**的鎖定類型。 使用此參數，您可以在**RecordsetOpen**作業期間，將鎖定變更為任何類型。 任何其他作業將會忽略*LockType* 。  
  
 *選項*  
 **Long**值，指出可用來執行命令或開啟**記錄集**的選項。  
  
 *adStatus*  
 呼叫這個事件時，可能會**adStatusCantDeny**或**adStatusOK**的[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。 如果它是**adStatusCantDeny**，此事件可能不會要求取消暫止的作業。  
  
 *pCommand*  
 套用此事件通知的[命令物件（ADO）](../../../ado/reference/ado-api/command-object-ado.md)物件。  
  
 *pRecordset*  
 套用此事件通知的[Recordset 物件（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
 *pConnection*  
 套用此事件通知的[連線物件（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
## <a name="remarks"></a>備註  
 **WillExecute**事件可能是因為連接而發生。  [Execute 方法（Ado Connection）](../../../ado/reference/ado-api/execute-method-ado-connection.md)、 [EXECUTE 方法（ado Command）](../../../ado/reference/ado-api/execute-method-ado-command.md)或[Open 方法（Ado Recordset）](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法： *pConnection*參數應該一律包含**連接**物件的有效參考。 如果事件是由**連接**所造成，則*pRecordset*和*pCommand*參數會設定為 [**無**]。 如果事件是由**記錄集**所造成，則*pRecordset*參數會參考**記錄集**物件，而*pCommand*參數會設定為 [**無**]。 如果事件是因為**命令**所造成，則*pCommand*參數會參考**命令**物件，而*pRecordset*參數會設定為 [**無**]。  
  
 **WillExecute**可讓您檢查和修改暫止的執行參數。 此事件可能會傳回暫止命令取消的要求。  
  
> [!NOTE]
>  如果**命令**的原始來源是[COMMANDSTREAM 屬性（ADO）](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性所指定的資料流程，則將新字串指派給**WillExecute**_來源_參數會變更**命令**的來源。 **CommandStream**屬性將會清除，而且[COMMANDTEXT 屬性（ADO）](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性會以新的來源更新。 **CommandStream**所指定的原始資料流程將會釋出，而且無法存取。  
  
 如果新來源字串的方言與 [[方言] 屬性](../../../ado/reference/ado-api/dialect-property.md)屬性（雖然該值至**CommandStream**）的原始設定不同，則必須藉由設定*pCommand*所參考之命令物件的 [**方言**] 屬性來指定正確的方言。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
