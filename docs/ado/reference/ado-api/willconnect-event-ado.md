---
description: WillConnect 事件 (ADO)
title: WillConnect 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords:
- WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
author: rothja
ms.author: jroth
ms.openlocfilehash: d7c9bc68b33e9a8ed8878e153b5fb2eb11d27ba2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441480"
---
# <a name="willconnect-event-ado"></a>WillConnect 事件 (ADO)
在開始連接之前，會呼叫 **WillConnect** 事件。  
  
 **適用于：** [ (ADO) 的連線物件 ](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 包含暫止連接之連接資訊的 **字串** 。  
  
 *UserID*  
 包含暫止連接之使用者名稱的 **字串** 。  
  
 *密碼*  
 **字串**，其中包含暫止連接的密碼。  
  
 *選項*  
 **Long**值，指出提供者應該如何評估*ConnectionString*。 您唯一的選項是 **adAsyncOpen**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 呼叫這個事件時，預設會將此參數設為 **adStatusOK** 。 如果事件無法要求取消暫止的作業，則會設為 **adStatusCantDeny** 。  
  
 在此事件傳回之前，請將此參數設定為 **adStatusUnwantedEvent** ，以防止後續的通知。 將此參數設定為 **adStatusCancel** ，以要求導致取消此通知的連接作業。  
  
 *pConnection*  
 適用此事件通知的 [連接](../../../ado/reference/ado-api/connection-object-ado.md) 物件。 **WillConnect**事件處理常式對**連接**的參數所做的變更不會影響到**連接**。  
  
## <a name="remarks"></a>備註  
 當呼叫 **WillConnect** 時， *ConnectionString*、 *UserID*、 *Password*和 *Options* 參數會設定為作業所建立的值，這會造成此事件 (擱置的連接) ，而且可以在事件傳回之前變更。 **WillConnect** 可能會傳回暫止連接取消的要求。  
  
 當此事件取消時，會呼叫 **ConnectComplete** ，並將其 *adStatus* 參數設定為 **adStatusErrorsOccurred**。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 (VC + +) ](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
