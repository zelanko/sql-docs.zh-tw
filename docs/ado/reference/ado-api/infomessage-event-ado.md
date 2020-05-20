---
title: InfoMessage 事件（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
author: rothja
ms.author: jroth
ms.openlocfilehash: c5fc0adfec791294bb6c680dab94078b8a63ec07
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758684"
---
# <a name="infomessage-event-ado"></a>InfoMessage 事件 (ADO)
每當**ConnectionEvent**操作期間發生警告時，就會呼叫**InfoMessage**事件。  
  
## <a name="syntax"></a>語法  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>參數  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 此參數包含傳回的任何錯誤。 如果傳回多個錯誤，請列舉**錯誤**集合來尋找它們。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。 如果發生警告， *adStatus*會設為**AdStatusOK** ，而*pError*會包含警告。  
  
 在此事件傳回之前，請將此參數設定為**adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pConnection*  
 [Connection](../../../ado/reference/ado-api/connection-object-ado.md)物件。 發生警告的連接。 例如，開啟**連接**物件或在**連接**上執行[命令](../../../ado/reference/ado-api/command-object-ado.md)時，可能會出現警告。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
