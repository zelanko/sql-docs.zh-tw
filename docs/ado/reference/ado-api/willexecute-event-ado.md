---
description: WillExecute 事件 (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: dd217597018b4cb5aa4764955fdd1795371a040c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441470"
---
# <a name="willexecute-event-ado"></a>WillExecute 事件 (ADO)
**WillExecute**事件是在連接上執行暫止命令之前呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 包含 SQL 命令或預存程式名稱的 **字串** 。  
  
 *CursorType*  
 [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) ，其中包含將開啟之**記錄集**的資料指標類型。 使用這個參數，您可以在 **記錄集**[開啟方法 (ADO 記錄集) ](../../../ado/reference/ado-api/open-method-ado-recordset.md) 作業期間，將資料指標變更為任何類型。 任何其他作業將會忽略*CursorType* 。  
  
 *LockType*  
 [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) ，其中包含將開啟之**記錄集**的鎖定類型。 使用此參數，您可以在 **RecordsetOpen** 作業期間，將鎖定變更為任何類型。 任何其他作業將會忽略*LockType* 。  
  
 *選項*  
 **Long**值，表示可用來執行命令或開啟**記錄集**的選項。  
  
 *adStatus*  
 呼叫這個事件時，可能會是**adStatusCantDeny**或**adStatusOK**的[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。 如果 **adStatusCantDeny**，此事件可能不會要求取消暫止的作業。  
  
 *pCommand*  
 [命令物件 (](../../../ado/reference/ado-api/command-object-ado.md)適用此事件通知的 ADO) 物件。  
  
 *pRecordset*  
 [記錄集物件 (](../../../ado/reference/ado-api/recordset-object-ado.md)適用此事件通知的 ADO) 物件。  
  
 *pConnection*  
 此事件通知適用 [ (ADO) 物件的 Connection 物件 ](../../../ado/reference/ado-api/connection-object-ado.md) 。  
  
## <a name="remarks"></a>備註  
 **WillExecute**事件可能會因為連接而發生。  [Execute 方法 (Ado Connection) ](../../../ado/reference/ado-api/execute-method-ado-connection.md)、 [EXECUTE 方法 (ado 命令) ](../../../ado/reference/ado-api/execute-method-ado-command.md)，或 [ (Ado 記錄集) 方法的 Open 方法 ](../../../ado/reference/ado-api/open-method-ado-recordset.md) 。 *pConnection* 參數應一律包含 **連接** 物件的有效參考。 如果事件是因為Connection.Exe很 ** 刻意**， *pRecordset* 和 *PCommand* 參數會設定為 **Nothing**。 如果事件是因為 **記錄集**所造成，則 *pRecordset* 參數將參考 **記錄集** 物件，而 *pCommand* 參數則設定為 **Nothing**。 如果事件是因為 **Command.Exe**很好用，則 *pCommand* 參數將會參考 **命令** 物件，而且 *pRecordset* 參數會設定為 **Nothing**。  
  
 **WillExecute** 可讓您檢查和修改暫止的執行參數。 此事件可能會傳回擱置命令取消的要求。  
  
> [!NOTE]
>  如果 **命令** 的原始來源是 CommandStream 屬性所指定的資料流程 [ (ADO) ](../../../ado/reference/ado-api/commandstream-property-ado.md) 屬性，則將新字串指派給 **WillExecute**_來源_ 參數會變更 **命令**的來源。 將會清除 **CommandStream** 屬性，並將 [ [CommandText] 屬性 (ADO) ](../../../ado/reference/ado-api/commandtext-property-ado.md) 屬性更新為新的來源。 **CommandStream**所指定的原始資料流程將會釋出，而且無法存取。  
  
 如果新來源字串的方言與[方言屬性](../../../ado/reference/ado-api/dialect-property.md)屬性的原始設定不同 (對應至**CommandStream**) ，則必須藉由設定*pCommand*所參考命令物件的**方言**屬性來指定正確的方言。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 (VC + +) ](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
