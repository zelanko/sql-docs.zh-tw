---
title: ConnectComplete 和 Disconnect 事件（ADO） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 448270ddf0e8cd7efb5ec39a93d4ff993360730e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919562"
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>ConnectComplete 和 Disconnect 事件 (ADO)
連接啟動之後，會呼叫**ConnectComplete**事件。 **中斷**線上活動會在連接結束後呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它會描述*adStatus*的值為**adStatusErrorsOccurred**時所發生的錯誤。否則不會設定。  
  
 *adStatus*  
 一律會傳回**adStatusOK**的[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)值。  
  
 當呼叫**ConnectComplete**時，如果**WillConnect**事件要求取消暫止的連接，此參數會設定為**adStatusCancel** 。  
  
 在任一個事件傳回之前，請將此參數設定為**adStatusUnwantedEvent** ，以防止後續的通知。 不過，關閉並重新開啟[連接](../../../ado/reference/ado-api/connection-object-ado.md)會導致這些事件再次發生。  
  
 *pConnection*  
 套用此事件的**連接**物件。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
