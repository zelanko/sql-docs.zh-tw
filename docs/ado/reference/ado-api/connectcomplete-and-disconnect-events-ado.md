---
description: ConnectComplete 和 Disconnect 事件 (ADO)
title: " (ADO) 的 ConnectComplete 和中斷線上活動 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Disconnect
- Connection::ConnectComplete
- ConnectComplete
- Connection::Disconnect
helpviewer_keywords:
- Disconnect event [ADO]
- ConnectComplete event [ADO]
ms.assetid: 568f5252-d069-4d99-a01b-2ada87ad1304
author: rothja
ms.author: jroth
ms.openlocfilehash: 47fa12ef5fe4d678107254923b6d6cfa569e0db2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776027"
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>ConnectComplete 和 Disconnect 事件 (ADO)
連接開始之後，就會呼叫 **ConnectComplete** 事件。 連接結束之後，會呼叫 **中斷** 連接事件。  
  
## <a name="syntax"></a>語法  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *pError*  
 [Error](./error-object.md)物件。 描述 *adStatus* 的值為 **adStatusErrorsOccurred**時所發生的錯誤;否則未設定。  
  
 *adStatus*  
 一律會傳回**adStatusOK**的[EventStatusEnum](./eventstatusenum.md)值。  
  
 當呼叫**ConnectComplete**時，如果**WillConnect**事件已要求解除擱置的連接，這個參數會設定為**adStatusCancel** 。  
  
 在任一事件傳回之前，請將此參數設定為 **adStatusUnwantedEvent** ，以防止後續的通知。 不過，關閉並重新開啟 [連接](./connection-object-ado.md) 會導致這些事件再次發生。  
  
 *pConnection*  
 適用于這個事件的 **連接** 物件。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 (VC + +) ](./ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../guide/data/ado-event-handler-summary.md)